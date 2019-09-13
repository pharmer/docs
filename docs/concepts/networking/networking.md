---
title: Networking | Pharmer
description: Networking of Pharmer
menu:
  docs_{{ .version }}:
    identifier: networking-networking-concepts
    name: Networking
    parent: networking-concepts
    weight: 30
menu_name: docs_{{ .version }}
section_menu_id: concepts
---

# Pod Networking

Available network provider support in `pharmer`
* [calico](https://kubernetes.io/docs/concepts/cluster-administration/networking/#project-calico)
* [flannel](https://kubernetes.io/docs/concepts/cluster-administration/networking/#flannel)
* [weavenet](https://kubernetes.io/docs/concepts/cluster-administration/networking/#weave-net-from-weaveworks)

`pharmer` uses `calico` as a default network provider. If you want to change the default network provider, you can do that with the help of following flag.
`--networking=<provider-name>`