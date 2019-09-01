---
title: AKS Credentials
menu:
  docs_0.3.1:
    identifier: aks-readme-credentials
    name: Credentials
    parent: aks-credentials-aks
    weight: 10
menu_name: docs_0.3.1
section_menu_id: guides
---

# Azure Credential


## Before You Begin

You need to have tenant ID, subscription ID, client ID and client secret values

### Tenant ID:

From the Portal, if you click on the Help icon in the upper right and then choose `Show Diagnostics` you can find the tenant id in the diagnostic JSON.

You can also find TenantID from `Portal -> Azure Active Directory -> Proparties -> Directory ID`

### Subscriotion ID

From the Portal, if you click on the Help icon in the upper right and then choose `Show Diagnostics` you can find the subscription id in the diagnostic JSON.

You can also find Subscription id from `Portal -> Subscription -> Subscription ID`

### Client ID

- Log in to the Azure Portal
- Navigate to `Azure Active Directory`
- Click `App Registrations` from left sidebar
- If you have already registered app, you see list of registered app. From `Application (Client) ID` copy the value
- If you do not have any registered app, click `New Registration` from top bar
- Fill up `Name` and then click `Register`
- Navigate to `Overview` from left bar. You'll get `Application (client) ID`

### Client Secret

- Log in to Azure Portal
- Navigate to `Azure Active Directory`
- Click `App Registrations` from left sidebar
- Go to your registered application from the list
- Click `Certificates and secrets` from left sidebar
- Click `New client secret` to create a new secret


## Create credential

From command line, run

```console
$ pharmer create credential <credential-name>
```

select azure as cloud provider. You will be prompted to enter `Tenant ID`, `Subscription ID`, `Client ID` and `Client Secret`

You can also create credential from environment variables

```console
$ export AZURE_SUBSCRIPTION_ID=<subscription id>
$ export AZURE_TENANT_ID=<tenant id>
$ export AZURE_CLIENT_ID=<client id>
$ export AZURE_CLIENT_SECRET=<client secret>
$ pharmer create credential <credential-name> --provider azure --from-env
```

You can also create credentials from file. Create a file in this format

```json
{
  "tenantID": "your azure client id",
  "subscriptionID": "your azure subscriptino id",
  "clientID": "your azure client id",
  "clientSecret": "your azure client secret"
}
```

now run

```console
$ pharmer create credential <credential-name> --provider azure --from-file <path-to-file>
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
    clientID: your azure client id
    clientSecret: your azure client secret
    subscriptionID: your azure subscriptino id
    tenantID: your azure client id
  provider: azure
```

Here,
 - `spec.data.clientID` is the azure client id
 - `spec.data.clientSecret` is the secret
 - `spec.data.subscriptionID`  is the subscription id of azure account
 - `spec.data.tenantID` is tenant id that you provided which can be edited by following command:


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