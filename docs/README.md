---
title: Welcome | Pharmer
description: Welcome to Pharmer
menu:
  docs_{{ .version }}:
    identifier: readme
    name: Readme
    parent: welcome
    weight: -1
menu_name: docs_{{ .version }}
section_menu_id: welcome
url: /docs/{{ .version }}/welcome/
aliases:
  - /docs/{{ .version }}/
  - /docs/{{ .version }}/README/
---

# pharmer
<img src="https://raw.githubusercontent.com/cncf/artwork/master/projects/kubernetes/certified-kubernetes/1.13/color/certified-kubernetes-1.13-color.png" align="right" width="200px">Kubernetes Cluster Manager for [Kubeadm](https://github.com/kubernetes/kubeadm). Think `kops using kubeadm`!

This project is spread over 3 repositories:

- [pharmer/pharmer](https://github.com/pharmer/pharmer): A [Kops](https://github.com/kubernetes/kops) like cluster manager using `Kubeadm`. Supported cloud providers:
  - [Amazon Web Services](https://aws.amazon.com/)
  - [Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)
  - [DigitalOcean](https://www.digitalocean.com/)
  - [Google Cloud](https://cloud.google.com/compute/)
  - [Google Kubernetes Engine GKE](https://cloud.google.com/kubernetes-engine/)
  - [Linode](https://www.linode.com/)
  - [Microsoft Azure](https://azure.microsoft.com/en-us/)
  - [Azure Kubernetes Servic AKS](https://docs.microsoft.com/en-us/azure/aks/)
  - [Packet](https://www.packet.net/)

- [pharmer/pre-k](https://github.com/pharmer/pre-k): Contains [a set of handy commands](https://github.com/pharmer/pre-k/blob/master/docs/reference/pre-k.md) that you run before `kubeadm init`.

- [pharmer/cloud-controller-manager](https://github.com/pharmer/cloud-controller-manager): Implements Cloud Controller manager for following cloud providers:
  - [Packet](https://www.packet.net/)

## User Guide
 - [Create & manage a Kubernetes cluster in AWS EC2](/docs/guides/aws/)
 - [Create & manage a Kubernetes cluster in Amazon EKS](/docs/guides/eks/)
 - [Create & manage a Kubernetes cluster in Google Cloud](/docs/guides/gce/)
 - [Create & manage a Kubernetes cluster in Google Kubernetes Engine](/docs/guides/gke/)
 - [Create & manage a Kubernetes cluster in Microsoft Azure](/docs/guides/azure/)
 - [Create & manage a Kubernetes cluster in Azure Kubernetes Servic](/docs/guides/aks/)
 - [Create & manage a Kubernetes cluster in DigitalOcean](/docs/guides/digitalocean/)
 - [Create & manage a Kubernetes cluster in Linode](/docs/guides/linode/)
 - [Create & manage a Kubernetes cluster in Packet](/docs/guides/packet/)

## Supported Versions Matrix

| pharmer version | k8s 1.9.x | k8s 1.10.x | k8s 1.11.x | k8s 1.12.x | k8s 1.13.x | k8s 1.14.x
|-----------------|-----------|------------|------------|------------|---------|---------------
| 0.5.2           | &#10007;  | &#10007;   | &#10007;   |&#10007;    | &#10003;| &#10003;
| 0.3.1           | &#10007;  | &#10007;   | &#10007;   |&#10007;    | &#10003;| &#10003;
| 0.3.0           | &#10007;  | &#10007;   | &#10007;   |&#10007;    | &#10003;| &#10003;
| 0.2.0           | &#10007;  | &#10007;   | &#10007;   | &#10003;   | &#10003;| &#10007;
| 0.1.1           | &#10007;  | &#10007;   | &#10003;   | &#10003;   | &#10007;| &#10007;
| 0.1.0-rc.5      | &#10007;  | &#10003;   | &#10003;   | &#10007;   | &#10007;| &#10007;
| 0.1.0-rc.4      | &#10003;  | &#10003;   | &#10007;   | &#10007;   | &#10007;| &#10007;

## Contribution guidelines
Want to help improve Pharmer? Please start [here](/docs/CONTRIBUTING.md).

---

**Pharmer binaries collects anonymous usage statistics to help us learn how the software is being used and how we can improve it. To disable stats collection, run the operator with the flag** `--analytics=false`.

---

## Support
We use Slack for public discussions. To chit chat with us or the rest of the community, join us in the [Kubernetes Slack team](https://kubernetes.slack.com/messages/C81LSKMPE/details/) channel `#pharmer`. To sign up, use our [Slack inviter](http://slack.kubernetes.io/).

To receive product announcements, please join our [mailing list](https://groups.google.com/forum/#!forum/pharmer) or follow us on [Twitter](https://twitter.com/AppsCodeHQ). Our mailing list is also used to share design docs shared via Google docs.

If you have found a bug with Pharmer or want to request for new features, please [file an issue](https://github.com/pharmer/project/issues/new).
