---
title: DataStore | Pharmer
menu:
  docs_0.3.1:
    identifier: datastore-datastore-concepts
    name: DataStore
    parent: datastore-concepts
    weight: 20
menu_name: docs_0.3.1
section_menu_id: concepts
---

# Pharmer Datastore

To store your cluster  and credential resource, `pharmer` use [vfs](/docs/cli/vfs.md) as default storage
provider. There is another provider [postgres database](/docs/cli/xorm.md) available for storing resources.

Pharmer supports following storage provider

* [Vfs](vfs.md)
* [Postgres Database](xorm.md)