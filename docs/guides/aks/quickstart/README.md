---
title: AKS Quickstart
menu:
  docs_{{ .version }}:
    identifier: aks-readme-quickstart
    name: Quickstart
    parent: aks-quickstart-aks
    weight: 10
menu_name: docs_{{ .version }}
section_menu_id: guides
url: /docs/{{ .version }}/guides/aks/quickstart/
aliases:
  - /docs/{{ .version }}/guides/aks/quickstart/README/
---

# Running Kubernetes on Azure AKS

Following example will use `pharmer ` to create a Kubernetes cluster with 1 worker node server and a master server (i,e, 2 servers in you cluster) in [Azure AKS](https://azure.microsoft.com/).

## Before you start

As a prerequisite, you need to have `pharmer` installed.  To install `pharmer` use the [setup](/docs/setup/install.md) guide

## Pharmer storage

To store your cluster  and credential resource, you can configure pharmer to use local file system or postgres database. In this document we will use local file system ([vfs](/docs/concepts/datastore/vfs.md)) as a storage provider. To know more click [here](/docs/concepts/datastore/datastore.md)


## Credential Importing

You can create a credential named `azur` by running

```console
$ pharmer create credential azur
```

Follow this guide for more information [here](/docs/guides/aks/credentials/)


## Cluster provisioning

There are two steps to create a Kubernetes cluster using `pharmer`.
In first step `pharmer` create basic configuration file with user choice. Then in second step `pharmer` applies those
information to create cluster on specific provider.

Here, we discuss how to use `pharmer` to create a Kubernetes cluster on `azure aks`

### Create Cluster

We want to create a cluster with following information:
    - Provider: Azure
    - Cluster name: aksx
    - Location: eastus (Virginia)
    - Number of nodes: 1
    - Node sku: Standard_D1_v2 (cpu: 1, ram: 3.5, disk: 50)
    - Kubernetes version: 1.14.1
    - Credential name: [azur](#credential-importing)

For location code and sku details click [hrere](https://github.com/pharmer/cloud/blob/master/data/json/apis/cloud.pharmer.io/v1/cloudproviders/azure.json)

Available options in `pharmer` to create a cluster are:

```console
Create a Kubernetes cluster for a given cloud provider

Usage:
  pharmer create cluster [flags]

Aliases:
  cluster, clusters, Cluster

Examples:
pharmer create cluster demo-cluster

Flags:
      --credential-uid string       Use preconfigured cloud credential uid
  -h, --help                        help for cluster
      --kubernetes-version string   Kubernetes version
      --masters int                 Number of masters (default 1)
      --namespace string            Namespace (default "default")
      --network-provider string     Name of CNI plugin. Available options: calico, flannel, kubenet, weavenet (default "calico")
      --nodes stringToInt           Node set configuration (default [])
  -o, --owner string                Current user id
      --provider string             Provider name
      --zone string                 Cloud provider zone name

Global Flags:
      --alsologtostderr                  log to standard error as well as files
      --analytics                        Send analytical events to Google Guard (default true)
      --config-file string               Path to Pharmer config file
      --env string                       Environment used to enable debugging (default "prod")
      --kubeconfig string                Paths to a kubeconfig. Only required if out-of-cluster.
      --log-flush-frequency duration     Maximum number of seconds between log flushes (default 5s)
      --log_backtrace_at traceLocation   when logging hits line file:N, emit a stack trace (default :0)
      --log_dir string                   If non-empty, write log files in this directory
      --logtostderr                      log to standard error instead of files (default true)
      --master --kubeconfig              (Deprecated: switch to --kubeconfig) The address of the Kubernetes API server. Overrides any value in kubeconfig. Only required if out-of-cluster.
      --stderrthreshold severity         logs at or above this threshold go to stderr
  -v, --v Level                          log level for V logs
      --vmodule moduleSpec               comma-separated list of pattern=N settings for file-filtered logging
```

So, we need to run following command to create cluster with our information.

```console
$ pharmer create cluster aksx --v=4 --provider=aks --zone=eastus --nodes=Standard_D1_v2=1	--credential-uid=azur --kubernetes-version=1.14.1
I0626 15:29:31.675278    8568 create.go:24] [create-cluster] "level"=0 "msg"="creating cluster" "cluster-name"="aksx"
I0626 15:29:31.675516    8568 create.go:46] [create-cluster] "level"=2 "msg"="cluster doesn't exists, ignoring error" "cluster-name"="aksx" "error"="cluster `aksx` does not exist. Reason: not found"
I0626 15:29:32.724306    8568 create.go:75] [create-cluster] "level"=0 "msg"="successfully created cluster" "cluster-name"="aksx"
```

To know about [pod networks](https://kubernetes.io/docs/concepts/cluster-administration/networking/) supports in `pharmer` click [here](/docs/concepts/networking/networking.md)

The directory structure of the storage provider will be look like:

```console
$ tree ~/.pharmer/store.d/clusters/aksx
├──aksx
│   ├── machineset
│   │   └── standard-b2ms-pool.json
│   ├── pki
│   │   ├── ca.crt
│   │   ├── ca.key
│   │   ├── etcd
│   │   │   ├── ca.crt
│   │   │   └── ca.key
│   │   ├── front-proxy-ca.crt
│   │   ├── front-proxy-ca.key
│   │   ├── sa.crt
│   │   └── sa.key
│   └── ssh
│       ├── idaksx-sshkey
│       └── idaksx-sshkey.pub
└──aksx.json

5 directories, 12 files

```
Here,
- `aksx/machineset/`: contains the node groups information. [Check below](#cluster-scaling) for node group operations.You can see the node group list using following command.

```console
$ pharmer get nodegroups -k aksx
```

- `aksx/pki`: contains the cluster certificate information containing `ca` and `front-proxy-ca`.
- `aksx/ssh`: has the ssh credentials on cluster's nodes. With this key you can `ssh` into any node on a cluster
- `aksx.json`: contains the cluster resource information

You can view your cluster configuration file by following command.

```yaml
$ pharmer get cluster aksx -o yaml
apiVersion: v1alpha1
kind: Cluster
metadata:
  creationTimestamp: 2018-06-23T11:41:43Z
  generation: 1529754103043035047
  name: aksx
  uid: 668f8658-76da-11e8-bdc8-382c4a73a7c4
spec:
  api:
    advertiseAddress: ""
    bindPort: 0
  caCertName: ca
  cloud:
    azure:
      azureStorageAccountName: k8saksxjzvw2p
      resourceGroup: aksx
      rootPassword: GJersaT_NWi8b_If
      routeTableName: aksx-rt
      securityGroupName: aksx-nsg
      subnetCidr: 10.240.0.0/16
      subnetName: aksx-subnet
      vnetName: aksx-vnet
    cloudProvider: aks
    region: eastus
    sshKeyName: aksx-4wa6cz
    zone: eastus
  credentialName: azure
  frontProxyCACertName: front-proxy-ca
  kubernetesVersion: 1.10.3
  networking:
    networkProvider: calico
status:
  cloud: {}
  phase: Pending
```

Here,

* `metadata.name` refers the cluster name, which should be unique within your cluster list.
* `metadata.uid` is a unique ACID, which is generated by pharmer
* `spec.cloud` specifies the cloud provider information. pharmer uses `ubuntu-16-04-x64` image by default. don't change the instance images, otherwise cluster may not be working.
* `spc.cloud.sshKeyName` shows which ssh key added to cluster instance.
* `spec.kubernetesVersion` is the cluster server version. It can be modified.
* `spec.credentialName` is the credential name which is provider during cluster creation command.
* `status.phase` may be `Pending`, `Ready`, `Deleting`, `Deleted`, `Upgrading` depending on current cluster status.

You can modify this configuration by:

```console
$ pharmer edit cluster aksx
```

## Applying Cluster
If everything looks ok, we can now apply the resources. This actually creates resources on `Scaleway`.
Up to now we've only been working locally.

To apply run:

```console
$ pharmer apply aksx
```

Now, `pharmer` will apply that configuration, thus create a Kubernetes cluster. After completing task the configuration file of the cluster will be look like

```yaml
 $ pharmer get cluster aksx -o yaml
apiVersion: v1alpha1
kind: Cluster
metadata:
  creationTimestamp: 2018-06-23T11:41:43Z
  generation: 1529754103043035047
  name: aksx
  uid: 668f8658-76da-11e8-bdc8-382c4a73a7c4
spec:
  api:
    advertiseAddress: ""
    bindPort: 0
  caCertName: ca
  cloud:
    azure:
      azureStorageAccountName: k8saksxjzvw2p
      resourceGroup: aksx
      rootPassword: GJersaT_NWi8b_If
      routeTableName: aksx-rt
      securityGroupName: aksx-nsg
      subnetCidr: 10.240.0.0/16
      subnetName: aksx-subnet
      vnetName: aksx-vnet
    cloudProvider: aks
    region: eastus
    sshKeyName: aksx-4wa6cz
    zone: eastus
  credentialName: azure
  frontProxyCACertName: front-proxy-ca
  kubernetesVersion: 1.10.3
  networking:
    networkProvider: calico
status:
  cloud: {}
  phase: Ready
```

Here,`status.phase`: is ready. So, you can use your cluster from local machine.

To get the `kubectl` configuration file(kubeconfig) on your local filesystem run the following command.

```console
$ pharmer use cluster aksx
```

If you don't have `kubectl` installed click [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

Now you can run `kubectl get nodes` and verify that your kubernetes 1.9.0 is running.

```console
$ kubectl get nodes
NAME                        STATUS    AGE       VERSION
aks-sd1v2p-33941960-0   Ready     agent     35m       v1.10.3
```

## Cluster Scaling

Scaling a cluster refers following meanings:-

1. Increment the number of nodes of a certain node group
2. Decrement the number of nodes of a certain node group

To see the current node groups list, you need to run following command:

```console
$ pharmer get nodegroups -k aksx
NAME               Cluster   Node      SKU
Standard-D1-v2-pool   aksx      1         Standard_D1_v2
```

## Updating existing NG

For scenario 1 & 2 we need to update our existing node group. To update existing node group configuration run
the following command.

```yaml
$ pharmer edit nodegroup  Standard-D1-v2-pool -k aksx

# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1alpha1
kind: NodeGroup
metadata:
  clusterName: aksx
  creationTimestamp: 2018-06-23T11:41:43Z
  labels:
    node-role.kubernetes.io/node: ""
  name: Standard-D1-v2-pool
  uid: 66ffd7c3-76da-11e8-bdc8-382c4a73a7c4
spec:
  nodes: 1
  template:
    spec:
      sku: Standard_D1_v2
      type: regular
status:
  nodes: 0
```

Here,
* `metadata.name` refers the node group name, which is unique within a cluster.
* `metadata.labels` specifies the label of the nodegroup, which will be add to all nodes of following node group.
    * For master label will be `"node-role.kubernetes.io/master": ""`
    * For node label will be like `"node-role.kubernetes.io/node": ""`
* `metadata.clusterName` indicates the cluster, which has this node group.
* `spec.nodes` shows the number of nodes for this following group.
* `spec.template.sku` refers the size of the machine
* `status.node` shows the number of nodes that are really present on the current cluster while scaling

To update number of nodes for this nodegroup modify the `node` number under `spec` field.

After completing your change on the node groups, you need to apply that via `pharmer` so that changes will be applied
on provider cluster.

```console
$ pharmer apply aksx
```

This command will take care of your actions that you applied on the node groups recently.

```console
 $ pharmer get nodegroups -k aksx
NAME               Cluster   Node      SKU
Standard-D1-v2-pool   aksx      2         Standard_D1_v2
```

## Cluster Backup

To get a backup of your cluster run the following command:

```console
$ pharmer backup cluster --cluster aksx --backup-dir=aksx-backup
```

Here,
   `--backup-dir` is the flag for specifying your backup directory where phamer puts the backup file

After finishing task `pharmer` creates a `.tar.gz` file in your backup directory where you find the backup yaml of your cluster

### Cluster Upgrading

To upgrade your cluster firstly you need to check if there any update available for your cluster and latest kubernetes version.

To check run:

```console
$ pharmer describe cluster aksx
Name:		aksx
Version:	1.10.3
NodeGroup:
  Name                  Node
  ----                  ------
  Standard-D1-v2-pool   1
```

Then, if you decided to upgrade you cluster run the command that are showing on describe command.

```console
$ pharmer edit cluster aksx --kubernetes-version=1.10.4
cluster "aksx" updated
```

You can verify your changes by checking the yaml of the cluster.

```yaml
$ pharmer get cluster aksx -o yaml
apiVersion: v1alpha1
kind: Cluster
metadata:
  creationTimestamp: 2018-06-23T11:41:43Z
  generation: 1529758341849783579
  name: aksx
  uid: 668f8658-76da-11e8-bdc8-382c4a73a7c4
spec:
  api:
    advertiseAddress: ""
    bindPort: 0
  caCertName: ca
  cloud:
    azure:
      azureStorageAccountName: k8saksxjzvw2p
      resourceGroup: aksx
      rootPassword: GJersaT_NWi8b_If
      routeTableName: aksx-rt
      securityGroupName: aksx-nsg
      subnetCidr: 10.240.0.0/16
      subnetName: aksx-subnet
      vnetName: aksx-vnet
    cloudProvider: aks
    region: eastus
    sshKeyName: aksx-4wa6cz
    zone: eastus
  credentialName: azure
  frontProxyCACertName: front-proxy-ca
  kubernetesVersion: 1.10.4
  networking:
    networkProvider: calico
status:
  cloud: {}
  phase: Upgrading
```

Here, `spec.kubernetesVersion` is changed to `1.10.4` from `1.10.3`

If everything looks ok, then run:

```console
$ pharmer apply aksx
```

## Cluster Deleting

To delete your cluster run

```console
$ pharmer delete cluster aksx
```

Then, the yaml file looks like

```yaml
$ pharmer get cluster aksx -o yaml
apiVersion: v1alpha1
kind: Cluster
metadata:
  creationTimestamp: 2018-06-23T11:41:43Z
  deletionTimestamp: 2018-06-23T12:53:26Z
  generation: 1529758341849783579
  name: aksx
  uid: 668f8658-76da-11e8-bdc8-382c4a73a7c4
spec:
  api:
    advertiseAddress: ""
    bindPort: 0
  caCertName: ca
  cloud:
    azure:
      azureStorageAccountName: k8saksxjzvw2p
      resourceGroup: aksx
      rootPassword: GJersaT_NWi8b_If
      routeTableName: aksx-rt
      securityGroupName: aksx-nsg
      subnetCidr: 10.240.0.0/16
      subnetName: aksx-subnet
      vnetName: aksx-vnet
    cloudProvider: aks
    region: eastus
    sshKeyName: aksx-4wa6cz
    zone: eastus
  credentialName: azure
  frontProxyCACertName: front-proxy-ca
  kubernetesVersion: 1.10.4
  networking:
    networkProvider: calico
status:
  cloud: {}
  phase: Deleting
```

Here,

- `metadata.deletionTimestamp`: is set when cluster deletion command was applied.

Now, to apply delete on provider cluster run

```console
$ pharmer apply aksx
```

**Congratulations !!!** , you're an official `pharmer` user now.