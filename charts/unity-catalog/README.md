# unity-catalog

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A Helm chart for Kubernetes

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Pavan Kumar. | <emailtopavankumar.a@gmail.com> |  |

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://registry-1.docker.io/bitnamicharts | mysql | 12.x.x |
| oci://registry-1.docker.io/bitnamicharts | postgresql | 12.x.x |
| oci://registry-1.docker.io/bitnamicharts | postgresql-ha | 15.x.x |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| server.affinity | object | `{}` |  |
| server.autoscaling.enabled | bool | `false` |  |
| server.autoscaling.maxReplicas | int | `100` |  |
| server.autoscaling.minReplicas | int | `1` |  |
| server.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| server.conf.createCustomConfig | bool | `true` |  |
| server.conf.hibernate | string | `"hibernate.connection.driver_class=org.h2.Driver\nhibernate.connection.url=jdbc:h2:file:./etc/db/h2db;DB_CLOSE_DELAY=-1\nhibernate.hbm2ddl.auto=update\nhibernate.show_sql=false\nhibernate.archive.autodetection=class\nhibernate.use_sql_comments=true\norg.hibernate.SQL=INFO\norg.hibernate.type.descriptor.sql.BasicBinder=TRACE"` |  |
| server.conf.log4j2 | string | `"status = warn\nappenders = rollingFile\n\nappender.rollingFile.type = RollingFile\nappender.rollingFile.name = RollingFile\nappender.rollingFile.fileName = etc/logs/server.log\nappender.rollingFile.filePattern = etc/logs/server-%d{MM-dd-yyyy-HH-mm-ss}-%i.log.gz\nappender.rollingFile.layout.type = PatternLayout\nappender.rollingFile.layout.pattern = %d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n\n\nappender.rollingFile.policies.type = Policies\nappender.rollingFile.policies.time.type = TimeBasedTriggeringPolicy\nappender.rollingFile.policies.time.interval = 1\nappender.rollingFile.policies.size.type = SizeBasedTriggeringPolicy\nappender.rollingFile.policies.size.size = 10MB\n\nappender.rollingFile.strategy.type = DefaultRolloverStrategy\nappender.rollingFile.strategy.max = 5\nappender.rollingFile.strategy.fileIndex = max\n\nappender.rollingFile.strategy.action.type = Delete\nappender.rollingFile.strategy.action.basePath = etc/logs\nappender.rollingFile.strategy.action.condition.type = IfFileName\nappender.rollingFile.strategy.action.condition.glob = server-*.log.gz\nappender.rollingFile.strategy.action.ifAny.type = IfAccumulatedFileCount\nappender.rollingFile.strategy.action.ifAny.exceeds = 5\n\nrootLogger.level = info\nrootLogger.appenderRefs = rollingFile\nrootLogger.appenderRef.rollingFile.ref = RollingFile"` |  |
| server.conf.server | string | `"server.env=dev\n## Identity Provider authorization parameters\n# examples:\n# authorization=enable\n# authorization-url=https://accounts.google.com/o/oauth2/auth\n# token-url=https://oauth2.googleapis.com/token\n# client-id=111122223333-abab1212cdcd3434.apps.googleusercontent.com\n# client-secret=GOCSPX-ababfoobarcdcd-5q\nserver.authorization=disable\nserver.authorization-url=\nserver.token-url=\nserver.client-id=\nserver.client-secret=\nserver.redirect-port=\n# D-Days H-Hours M-Minutes S-Seconds (P5D = 5 days,PT5H = 5 hours, PT5M = 5 minutes, PT5S = 5 seconds)\nserver.cookie-timeout=P5D\n\n# Define the model storage root.  Cloud storage or file based allowed.\n# If no root specified, the current working directory of the server is used.\n\n#storage-root.models=s3://my-s3-bucket/root\n#storage-root.models=abfs://file_system@account_name.dfs.core.windows.net/root\n#storage-root.models=gs://my-gc-bucket/root\nstorage-root.models=file:/tmp/ucroot\n\n## S3 Storage Config (Multiple configs can be added by incrementing the index)\ns3.bucketPath.0=\ns3.region.0=\ns3.awsRoleArn.0=\n# Optional (If blank, it will use DefaultCredentialsProviderChain)\ns3.accessKey.0=\ns3.secretKey.0=\n# Test Only (If you provide a session token, it will just use those session creds, no downscoping)\ns3.sessionToken.0=\n\n## ADLS Storage Config (Multiple configs can be added by incrementing the index)\nadls.storageAccountName.0=\nadls.tenantId.0=\nadls.clientId.0=\nadls.clientSecret.0=\n\n## GCS Storage Config (Multiple configs can be added by incrementing the index)\ngcs.bucketPath.0=\n# Optional (If blank, it will use Default Application chain to find credentials)\ngcs.jsonKeyFilePath.0="` |  |
| server.create | bool | `true` |  |
| server.fullnameOverride | string | `""` |  |
| server.image.pullPolicy | string | `"IfNotPresent"` |  |
| server.image.repository | string | `"greypavan/unity-catalog"` |  |
| server.image.tag | string | `"main"` |  |
| server.imagePullSecrets | list | `[]` |  |
| server.ingress.annotations | object | `{}` |  |
| server.ingress.className | string | `""` |  |
| server.ingress.enabled | bool | `false` |  |
| server.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| server.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| server.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| server.ingress.tls | list | `[]` |  |
| server.livenessProbe.httpGet.path | string | `"/"` |  |
| server.livenessProbe.httpGet.port | string | `"http"` |  |
| server.livenessProbe.periodSeconds | int | `60` |  |
| server.livenessProbe.timeoutSeconds | int | `10` |  |
| server.mysql.enabled | bool | `false` |  |
| server.nameOverride | string | `""` |  |
| server.nodeSelector | object | `{}` |  |
| server.podAnnotations | object | `{}` |  |
| server.podLabels | object | `{}` |  |
| server.podSecurityContext | object | `{}` |  |
| server.postgresql-ha.enabled | bool | `false` |  |
| server.postgresql.enabled | bool | `false` |  |
| server.readinessProbe.httpGet.path | string | `"/"` |  |
| server.readinessProbe.httpGet.port | string | `"http"` |  |
| server.readinessProbe.periodSeconds | int | `60` |  |
| server.readinessProbe.timeoutSeconds | int | `10` |  |
| server.replicaCount | int | `1` |  |
| server.resources | object | `{}` |  |
| server.securityContext | object | `{}` |  |
| server.service.port | int | `8080` |  |
| server.service.type | string | `"ClusterIP"` |  |
| server.serviceAccount.annotations | object | `{}` |  |
| server.serviceAccount.automount | bool | `true` |  |
| server.serviceAccount.create | bool | `true` |  |
| server.serviceAccount.name | string | `""` |  |
| server.tolerations | list | `[]` |  |
| server.volumeMounts | list | `[]` |  |
| server.volumes | list | `[]` |  |
| ui.affinity | object | `{}` |  |
| ui.autoscaling.enabled | bool | `false` |  |
| ui.autoscaling.maxReplicas | int | `100` |  |
| ui.autoscaling.minReplicas | int | `1` |  |
| ui.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| ui.create | bool | `true` |  |
| ui.fullnameOverride | string | `""` |  |
| ui.image.pullPolicy | string | `"IfNotPresent"` |  |
| ui.image.repository | string | `"greypavan/unity-catalog-ui"` |  |
| ui.image.tag | string | `"main"` |  |
| ui.imagePullSecrets | list | `[]` |  |
| ui.ingress.annotations | object | `{}` |  |
| ui.ingress.className | string | `""` |  |
| ui.ingress.enabled | bool | `false` |  |
| ui.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ui.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ui.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ui.ingress.tls | list | `[]` |  |
| ui.livenessProbe.httpGet.path | string | `"/"` |  |
| ui.livenessProbe.httpGet.port | string | `"http"` |  |
| ui.nameOverride | string | `""` |  |
| ui.nodeSelector | object | `{}` |  |
| ui.podAnnotations | object | `{}` |  |
| ui.podLabels | object | `{}` |  |
| ui.podSecurityContext | object | `{}` |  |
| ui.readinessProbe.httpGet.path | string | `"/"` |  |
| ui.readinessProbe.httpGet.port | string | `"http"` |  |
| ui.replicaCount | int | `1` |  |
| ui.resources | object | `{}` |  |
| ui.securityContext | object | `{}` |  |
| ui.service.port | int | `3000` |  |
| ui.service.type | string | `"ClusterIP"` |  |
| ui.serviceAccount.annotations | object | `{}` |  |
| ui.serviceAccount.automount | bool | `true` |  |
| ui.serviceAccount.create | bool | `true` |  |
| ui.serviceAccount.name | string | `""` |  |
| ui.tolerations | list | `[]` |  |
| ui.volumeMounts | list | `[]` |  |
| ui.volumes | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
