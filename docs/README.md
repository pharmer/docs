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

<img src="https://raw.githubusercontent.com/cncf/artwork/master/projects/kubernetes/certified-kubernetes/1.13/color/certified-kubernetes-1.13-color.png" align="right" width="200px">A [Kops](https://github.com/kubernetes/kops) like Kubernetes Cluster Manager for [Kubeadm](https://github.com/kubernetes/kubeadm). Think `kops using kubeadm`!

Supported cloud providers are:

- [Amazon Web Services](guides/aws)
- [Amazon EKS](guides/eks)
- [DigitalOcean](guides/digitalocean)
- [Google Cloud](guides/gce)
- [Google Kubernetes Engine GKE](guides/gke)
- [Linode](guides/linode)
- [Microsoft Azure](guides/azure)
- [Azure Kubernetes Servic AKS](guides/aks)
- [Packet](guides/packet)

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
