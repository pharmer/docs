---
title: DigitalOcean Credentials
menu:
  docs_0.3.1:
    identifier: digitalocean-readme-credentials
    name: Credentials
    parent: digitalocean-credentials-digitalocean
    weight: 10
menu_name: docs_0.3.1
section_menu_id: guides
url: /docs/0.3.1/guides/digitalocean/credentials/
aliases:
  - /docs/0.3.1/guides/digitalocean/credentials/README/
---

# DigitalOcean Credential

## Before You Begin
You need to have a digitalocean Personal Access Token

## Token
From digitalocean portal, Select `API > Generate New Token` to get a personal access token.

## Create Credential

From command line, run

```console
$ pharmer create credential <credential-name>
```

select digitalocean as cloud provider. You will be prompted to enter `Personal Access Token`

You can also create credential from environment variables

```console
$ export DIGITALOCEAN_TOKEN=<token>
$ pharmer create credential <credential-name> --provider digitalocean --from-env
```

You can also create credentials from file. Create a file in this format

```json
{
  "token": "your digitalocean token",
}
```

now run

```console
$ pharmer create credential <credential-name> --provider digitalocean --from-file <path-to-file>
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
    token: your digitalocean token
  provider: digitalocean
```

Here,
 - `spec.data.token` is the digitalocean token


## Edit credential

You can edit your created credential by running

```console
$ phrmer edit credential <credential-name>
```

## Delete credential

You can delete your credential by running

```console
$ pharmer delete credential <credential-name>
