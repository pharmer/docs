---
title: Data Store
menu:
  product_pharmer_0.3.1:
    identifier: datastore
    name: Data Store
    parent: cli
    weight: 20
product_name: pharmer
menu_name: product_pharmer_0.3.1
section_menu_id: cli
---

# Pharmer Datastore

To store your cluster  and credential resource, `pharmer` use [vfs](/docs/cli/vfs.md) as default storage
provider. There is another provider [postgres database](/docs/cli/xorm.md) available for storing resources.

Pharmer supports following storage provider

* [Vfs](vfs.md)
* [Postgres Database](xorm.md)