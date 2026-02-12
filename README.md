# Helm chart for Versity S3 gateway <!-- omit in toc -->



![Version: 1.2.0](https://img.shields.io/badge/Version-1.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v1.2.0](https://img.shields.io/badge/AppVersion-v1.2.0-informational?style=flat-square) 

[Helm chart for Versity S3 gateway to a Posix backend](https://github.com/RobSlgm/versitygw)

This repository contains a Helm chart to install [The Versity S3 Gateway](https://github.com/versity/versitygw).

### Install the Chart

To install the chart with the release name my-release:

```shell
helm install my-release oci://ghcr.io/robslgm/charts/versitygw
```

### Uninstalling the Chart

To uninstall/delete the my-release deployment:

```shell
helm uninstall my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

# Configuration

Original [documentation](https://github.com/versity/versitygw/wiki/Global-Options) of global options.

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

Add option to your `values.yaml`, as example

~~~yaml
versitygw:
    config:
        VGV_META_NONE: "true"        
~~~

All items under `versitygw.config` are passed as enviroment variables with following exceptions:

| key | description |
| --- | ----------- |
| VGW_VERSIONING_DIR | Set by enabling the `persistence.versioning` |
| VGW_IAM_DIR | Set by enabling the `persistence.iam` |
| VGW_HEALTH | Set by default |
| VGW_VIRTUAL_DOMAIN | Set by `versitygw.virtualDomain` |
| ROOT_ACCESS_KEY_ID | Set by `versitygw.admin` |
| ROOT_SECRET_ACCESS_KEY | Set by `versitygw.admin` |


## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| fullnameOverride | string | `""` |  |
| httpRoute | object | {} | Expose the service via gateway-api HTTPRoute Requires Gateway API resources and suitable controller installed within the cluster (see: https://gateway-api.sigs.k8s.io/guides/) |
| httpRoute.enabled | bool | `false` | use either ingress or HTTPRoute (gateway API) |
| httpRoute.hostnames | list | `["chart-example.local"]` | Hostnames matching HTTP header. |
| httpRoute.parentRefs | list | `[{"name":"gateway","sectionName":"http"}]` | Which Gateways this Route is attached to. |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"versity/versitygw"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` | use either ingress or HTTPRoute (gateway API) |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/health"` |  |
| livenessProbe.httpGet.port | string | `"s3"` |  |
| livenessProbe.periodSeconds | int | `30` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence | object | {} | Volumes for Versity GW. Required if enabled in the configuration. |
| persistence.data | object | `{"enabled":true,"size":"1Gi","storageClass":"default"}` | Versity GW data |
| persistence.iam | object | `{"enabled":false,"size":"1Gi","storageClass":""}` | IAM |
| persistence.meta | object | `{"enabled":false,"size":"1Gi","storageClass":""}` | Metadata |
| persistence.versioning | object | `{"enabled":false,"size":"1Gi","storageClass":""}` | Versioning |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| readinessProbe.httpGet.path | string | `"/health"` |  |
| readinessProbe.httpGet.port | string | `"s3"` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automount | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |
| versitygw | object | {} | Versity GW configuration |
| versitygw.admin | object | {}   | Admin credentials |
| versitygw.admin.s3Credentials | object | {} | S3 Credentials (supply as secret, by default ) |
| versitygw.admin.s3Credentials.accessKeyId | object | {} | S3 admin username |
| versitygw.admin.s3Credentials.accessKeyId.key | string | `"ACCESS_KEY_ID"` | key in secret |
| versitygw.admin.s3Credentials.accessKeyId.name | string | `"versitygw-admin-secret"` | name of secret |
| versitygw.admin.s3Credentials.region | object | {} | S3 admin region |
| versitygw.admin.s3Credentials.region.key | string | `"S3_REGION"` | key in secret |
| versitygw.admin.s3Credentials.region.name | string | `"versitygw-admin-secret"` | name of secret |
| versitygw.admin.s3Credentials.secretAccessKey | object | {} | S3 admin access key |
| versitygw.admin.s3Credentials.secretAccessKey.key | string | `"ACCESS_SECRET_KEY"` | key in secret |
| versitygw.admin.s3Credentials.secretAccessKey.name | string | `"versitygw-admin-secret"` | name of secret |
| versitygw.config | object | `{}` | Versity configuration options (see above) |
| webui | Experimental | {} | Webui |
| webui.httpRoute.enabled | bool | `false` | use either ingress or HTTPRoute (gateway API) |
| webui.httpRoute.hostnames | list | `["chart-example-explorer.local"]` | Hostnames matching HTTP header. |
| webui.httpRoute.parentRefs | list | `[{"name":"gateway","sectionName":"http"}]` | Which Gateways this Route is attached to. |
| webui.ingress.enabled | bool | `false` | use either ingress or HTTPRoute (gateway API) |



## Source Code

* <https://github.com/RobSlgm/versitygw>
* <https://github.com/versity/versitygw>


----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)