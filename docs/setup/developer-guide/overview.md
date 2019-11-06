---
title: Developer Guide
menu:
  docs_{{ .version }}:
    identifier: developer-guide-readme
    name: Overview
    parent: developer-guide
    weight: 10
menu_name: docs_{{ .version }}
section_menu_id: setup
aliases:
  - /docs/{{ .version }}/setup/developer-guide/
---

## Development Guide
This document is intended to be the canonical source of truth for things like supported toolchain versions for building Pack.
If you find a requirement that this doc does not capture, please submit an issue on github.

This document is intended to be relative to the branch in which it is found. It is guaranteed that requirements will change over time
for the development branch, but release branches of Pharmer should not change.

### Build Pack
Some of the Pharmer development helper scripts rely on a fairly up-to-date GNU tools environment, so most recent Linux distros should
work just fine out-of-the-box.

#### Setup GO
Pharmer is written in Google's GO programming language. Currently, Pharmer is developed and tested on **go 1.12.12**. If you haven't set up a GO
development environment, please follow [these instructions](https://golang.org/doc/code.html) to install GO.

#### Download Source
Using `go get`

```console
$ go get -u github.com/pharmer/pharmer
$ cd $(go env GOPATH)/src/github.com/pharmer/pharmer
```

Using `git`

```console
$ git clone git@github.com:pharmer/pharmer.git $(go env GOPATH)/src/pharmer.dev/pharmer
$ cd $(go env GOPATH)/src/pharmer.dev/pharmer
```

#### Install Dev tools
You need to have docker and GNU-make installed

#### Build Binary

```console
$ make build
$ ./bin/linux_amd64/pharmer version
```

#### Update machine-controller image

Pharmer will look for environment variables  `MACHINE_CONTROLLER_IMAGE` for the machine controller image and falls back to using the image associated with the specifice release if this is unset. If you're building pharmer from local make sure run

```bash
$ make push REGISTRY=<your-docker-registry>
$ export MACHINE_CONTROLLER_IMAGE=<docker-image-pushed-from-above-command>
$ ./bin/linux_amd64/pharmer
```

#### Dependency management
Pharmer uses go modules to manage dependencies. Dependencies are already checked in the `vendor` folder.
If you want to update/add dependencies, run:

```console
$ go mod tidy
$ go mod vendor
```

#### Generate CLI Reference Docs

```console
$ ./hack/gendocs/make.sh
```
