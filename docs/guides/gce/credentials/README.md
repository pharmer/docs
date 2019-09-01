---
title: GCE Credentials
menu:
  docs_0.3.1:
    identifier: gce-readme-credentials
    name: Credentials
    parent: gce-credentials-gce
    weight: 10
menu_name: docs_0.3.1
section_menu_id: guides
---

# GCE Credential

## Create Credential
From google cloud console, go to `IAM & admin > Service accounts > Create Service Account`.

Then create a service account. In the 3rd step (Grant users access to this service account) press the button create key.
Then download it in `json` format

After that run the following command.

```console
$ pharmer create credential <credential-name> --provider gce --from-file <path-to-the-json-file>
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
    projectID: your project id
    serviceAccount: your service account json
  provider: gce
```

Here,
 - `spec.data.projectID` is the project id
 - `spec.data.serviceAccount` is the service account


## Edit credential

You can edit your created credential by running

```console
$ pharmer edit credential <credential-name>
```

## Delete credential

You can delete your credential by running

```console
$ pharmer delete credential <credential-name>
