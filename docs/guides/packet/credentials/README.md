---
title: Linode Credentials
menu:
  docs_0.3.1:
    identifier: packet-readme-credentials
    name: Credentials
    parent: packet-credentials-packet
    weight: 10
menu_name: docs_0.3.1
section_menu_id: guides
url: /docs/0.3.1/guides/packet/credentials/
aliases:
  - /docs/0.3.1/guides/packet/credentials/README/
---

# Packet Credential


## Before You Begin
You need to have Project ID and API Key

## Project ID
From [packet](https://app.packet.net), Select `Project Settings`, You'll find the `Project ID` there.

## API key
From [packet](https://app.packet.net), Select your profile icon, Then Select `API Keys`. Then add new API key or use any existing one.

## Create Credential
From command line, run

```console
$ pharmer create credential <credential-name>
```
select packet as cloud provider. You will be prompted to enter `Project ID` and `API Key`

You can also create credential from environment variables

```console
$ export PACKET_API_KEY=<api key>
$ export PACKET_PROJECT_ID=<project id>
$ pharmer create credential <credential-name> --provider packet --from-env
```

You can also create credentials from file. Create a file in this format

```json
{
  "projectID": "your packet project id",
  "apiKey": "your packet api key"
}
```

now run

```console
$ pharmer create credential <credential-name> --provider packet --from-file <path-to-file>
```

## View Credential
You can view list of credentials you created by running

```console
$ pharmer get credentials
```

To view the credential you created, run

```yaml
$ pharmer get credential <credential-name> -o yaml
apiVersion: cloud.pharmer.io/v1
kind: Credential
metadata:
  creationTimestamp: "2019-06-26T08:55:54Z"
  name: <credential-name>
spec:
  data:
    projectID: your packet project id
    apiKey: your packet api key
  provider: packet
```

Here,
 - `spec.data.projectID` is the project id
 - `spec.data.apiKey` is the api key


## Edit credential

You can edit your created credential by running

```console
$ phrmer edit credential <credential-name>
```

## Delete credential

You can delete your credential by running

```console
$ pharmer delete credential <credential-name>
```
