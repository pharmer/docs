---
title: AWS Credentials
menu:
  docs_{{ .version }}:
    identifier: aws-readme-credentials
    name: Credentials
    parent: aws-credentials-aws
    weight: 10
menu_name: docs_{{ .version }}
section_menu_id: guides
url: /docs/{{ .version }}/guides/aws/credentials/
aliases:
  - /docs/{{ .version }}/guides/aws/credentials/README/
---

# AWS Credential

## Before You Begin
You need to have AWS access key ID and AWS secret access key

### Access key ID & Secret Access Key
In order to create cluster within [AWS](https://aws.amazon.com/), `pharmer` needs a dedicated IAM user. `pharmer` use this user's API credential.
The `pharmer` user needs following permission to works properly.
![pharmer-iam](/docs/images/aws/pharmer-iam.png)

You can get the Access key ID and Secret Access key by following methods:

From the console, click your username. Then a list will appear. From the list select `My Security Credentials`.
Then click the button `create access key`.
Then you can copy the Access key ID and Secret Access key from there.

From aws cli,
If you have installed [aws cli](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) locally, then you can use the following
command to create `pharmer` IAM user.

```console
$ aws iam create-group --group-name pharmer

$ aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess --group-name pharmer
$ aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonRoute53FullAccess --group-name pharmer
$ aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/IAMFullAccess --group-name  pharmer
$ aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonVPCFullAccess --group-name pharmer
$ aws iam create-user --user-name pharmer

$ aws iam add-user-to-group --user-name pharmer --group-name pharmer
$ aws iam create-access-key --user-name pharmer
```

Use this access key while importing credentials on pharmer.

## Create credential

From command line, run the following command and paste the Access key ID & Secret Access Key.

```console
$ pharmer create credential aws
```

![aws-credential](/docs/images/aws/aws-credential.png)

Here, `aws` is the credential name, which must be unique within your storage.


You can also create credential from environment variables

```console
$ export AWS_ACCESS_KEY_ID=<aws access key ID>
$ export AWS_SECRET_ACCESS_KEY=<aws secret key>
$ pharmer create credential <credential-name> --provider aws --from-env
```

You can also create credentials from file. Create a file in this format

```json
{
  "accessKeyID": "your aws access key ID",
  "secretAccessKey": "your aws secret key",
}
```

now run

```console
$ pharmer create credential <credential-name> --provider aws --from-file <path-to-file>
```

## View Credential

You can view list of credentials you created by running

```console
$ pharmer get credentials
```

To view the credential you created, run

```yaml
$ pharmer get credentials aws -o yaml
apiVersion: v1beta1
kind: Credential
metadata:
  creationTimestamp: "2019-04-04T09:33:32Z"
  name: aws
spec:
  data:
    accessKeyID: <key-id>
    secretAccessKey: <access-key>
  provider: aws
```

Here,
 - `spec.data.accessKeyID` is the aws access key id
 - `spec.data.secretAccessKey` is the security access key


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