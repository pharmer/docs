---
title: Install Kubeform
menu:
  docs_{{ .version }}:
    identifier: install-pharmer
    name: Install
    parent: setup
    weight: 10
menu_name: docs_{{ .version }}
section_menu_id: setup
---

> New to Pharmer? Please start [here](/docs/concepts/).

# Installation Guide

Download pre-built binaries:

- [Linux amd64](https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-linux-amd64)
- [Linux arm64](https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-linux-arm64)
- [Mac amd64](https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-darwin-amd64)


### Linux amd64

```console
$ curl -LO https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-linux-amd64
$ chmod +x pharmer-linux-amd64
$ sudo mv pharmer-linux-amd64 /usr/local/bin/pharmer
```

Feel free to leave off `sudo mv pharmer /usr/local/bin` if you would like to add pharmer to your path manually.

### Linux arm64

```console
$ curl -LO https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-linux-arm64
$ chmod +x pharmer-linux-arm64
$ sudo mv pharmer-linux-arm64 /usr/local/bin/pharmer
```
Feel free to leave off `sudo mv pharmer /usr/local/bin` if you would like to add pharmer to your path manually.

### OSX

```console
$ curl -LO https://github.com/pharmer/pharmer/releases/download/{{< param "info.version" >}}/pharmer-darwin-amd64
$ chmod +x pharmer-darwin-amd64
$ sudo mv pharmer-darwin-amd64 /usr/local/bin/pharmer
```

Feel free to leave off `sudo mv pharmer /usr/local/bin` if you would like to add pharmer to your path manually.
