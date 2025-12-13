# Helm chart for Versity S3 gateway

This repository contains a Helm chart to install [The Versity S3 Gateway](https://github.com/versity/versitygw).

## Usage

### 1. Add the helm repository

```shell
helm repo add versitygw https://xxx/versitygw-helm
helm repo update
```

### 2. Install a Chart

To install a chart from this repository, use the following command:

```shell
helm install <release-name> versitygw/<chart-name>
```

### 3. Customize Installation

You can customize the installation by passing in custom values via the `--set` flag or by using a `values.yaml` file:

```shell
helm install <release-name> versitygw/<chart-name> --set key=value
```

or

```shell
helm install <release-name> versitygw/<chart-name> -f your-values.yaml
```

All options with an enviroment variable (usually `$VGW_`):

| option                   | description                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------------- |
| --chuid                  | chown newly created files and directories to client account UID (default: false) [$VGW_CHOWN_UID]         |
| --chgid                  | chown newly created files and directories to client account GID (default: false) [$VGW_CHOWN_GID]         |
| --bucketlinks            | allow symlinked directories at bucket level to be treated as buckets (default: false) [$VGW_BUCKET_LINKS] |
| --versioning-dir value   | the directory path to enable bucket versioning [$VGW_VERSIONING_DIR]                                      |
| --dir-perms value        | default directory permissions for new directories (default: 0755) [$VGW_DIR_PERMS]                        |
| --sidecar value          | use provided sidecar directory to store metadata [$VGW_META_SIDECAR]                                      |
| --nometa                 | disable metadata storage (default: false) [$VGW_META_NONE]                                                |
| --disableotmp            | disable O_TMPFILE support for new objects (default: false) [$VGW_DISABLE_OTMP]                            |
|                          | GLOBAL:                                                                                                   |
| --access value, -a value | root user access key [$ROOT_ACCESS_KEY_ID, $ROOT_ACCESS_KEY]                                              |
| --secret value, -s value | root user secret access key [$ROOT_SECRET_ACCESS_KEY, $ROOT_SECRET_KEY]                                   |
| --region value, -r value | s3 region string (default: "us-east-1") [$VGW_REGION]                                                     |
| --iam-dir value          | if defined, run internal iam service within this directory [$VGW_IAM_DIR]                                 |
| --health value           | health check endpoint path. Health endpoint will be configured on GET http method: GET \<health\>         |
|                          | NOTICE: the path has to be specified with '/'. e.g /health [$VGW_HEALTH]                                  |
