# Linode Credential


## Before You Begin 
You need to have a Linode Personal Access Token

## Token
From linode portal, Select `My Profile > API Tokens > Add a Personal Access Token` to get a personal access token.

## Create Credential
From command line, run
```console
$ pharmer create credential <credential-name>
```
select linode as cloud provider. You will be prompted to enter `Token`

You can also create credential from environment variables
```console
$ export LINODE_TOKEN=<token>
$ pharmer create credential <credential-name> --provider linode --from-env
```

You can also create credentials from file. Create a file in this format
```json
{
  "token": "your linode token",
}
```

now run
```console
$ pharmer create credential <credential-name> --provider linode --from-file <path-to-file>
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
    token: your linode token
  provider: linode
```

Here,
 - `spec.data.token` is the linode token


## Edit credential
You can edit your created credential by running
```console
$ phrmer edit credential <credential-name>
```

## Delete credential
You can delete your credential by running
```console
$ pharmer delete credential <credential-name>
