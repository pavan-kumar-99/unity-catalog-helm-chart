[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Application

Generic helm chart to deploy Unity Catalog on Kubernetes:

- Stateful mode when the replicaCount is 1
- creates both UI and also the UC server
- don't need privileged containers
- Native support to download extraJars through initContainers and add them to classpath
- run either as deployment, statefulset
- Native support to deploy MYSQL, PSQL in HA Mode

## Installing the Chart

To install the chart with the release name `my-catalog` in namespace `uc`:

```shell
helm repo add unity-catalog https://pavan-kumar-99.github.io/unity-catalog-helm-chart
helm repo update
helm install my-catalog unity-catalog/unity-catalog --namespace uc
```

## Uninstall the Chart

To uninstall the chart:

```shell
helm delete --namespace unity-catalog my-catalog
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| server.create | bool | `true` |  |
| server.replicaCount | int | `1` |  |
| server.image.repository | string | `"greypavan/unity-catalog"` |  |
| server.image.pullPolicy | string | `"IfNotPresent"` |  |
| server.image.tag | string | `"main"` |  |
| server.extraJars[0].name | string | `"mysql-connector-j"` |  |
| server.extraJars[0].version | string | `"9.1.0"` |  |
| server.extraJars[0].url | string | `"https://repo.maven.apache.org/maven2/com/mysql/mysql-connector-j/9.1.0/mysql-connector-j-9.1.0.jar"` |  |
| server.extraJars[1].name | string | `"postgresql-connector"` |  |
| server.extraJars[1].version | string | `"42.3.3"` |  |
| server.extraJars[1].url | string | `"https://repo.maven.apache.org/maven2/org/postgresql/postgresql/42.3.3/postgresql-42.3.3.jar"` |  |
| server.imagePullSecrets | list | `[]` |  |
| server.nameOverride | string | `""` |  |
| server.fullnameOverride | string | `""` |  |
| server.conf.createCustomConfig | bool | `false` |  |
| server.conf.log4j2 | string | `"status = warn\nappenders = rollingFile\n\nappender.rollingFile.type = RollingFile\nappender.rollingFile.name = RollingFile\nappender.rollingFile.fileName = etc/logs/server.log\nappender.rollingFile.filePattern = etc/logs/server-%d{MM-dd-yyyy-HH-mm-ss}-%i.log.gz\nappender.rollingFile.layout.type = PatternLayout\nappender.rollingFile.layout.pattern = %d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n\n\nappender.rollingFile.policies.type = Policies\nappender.rollingFile.policies.time.type = TimeBasedTriggeringPolicy\nappender.rollingFile.policies.time.interval = 1\nappender.rollingFile.policies.size.type = SizeBasedTriggeringPolicy\nappender.rollingFile.policies.size.size = 10MB\n\nappender.rollingFile.strategy.type = DefaultRolloverStrategy\nappender.rollingFile.strategy.max = 5\nappender.rollingFile.strategy.fileIndex = max\n\nappender.rollingFile.strategy.action.type = Delete\nappender.rollingFile.strategy.action.basePath = etc/logs\nappender.rollingFile.strategy.action.condition.type = IfFileName\nappender.rollingFile.strategy.action.condition.glob = server-*.log.gz\nappender.rollingFile.strategy.action.ifAny.type = IfAccumulatedFileCount\nappender.rollingFile.strategy.action.ifAny.exceeds = 5\n\nrootLogger.level = info\nrootLogger.appenderRefs = rollingFile\nrootLogger.appenderRef.rollingFile.ref = RollingFile"` |  |
| server.conf.hibernate | string | `"hibernate.connection.driver_class=org.h2.Driver\nhibernate.connection.url=jdbc:h2:file:./etc/db/h2db;DB_CLOSE_DELAY=-1\nhibernate.hbm2ddl.auto=update\nhibernate.show_sql=false\nhibernate.archive.autodetection=class\nhibernate.use_sql_comments=true\norg.hibernate.SQL=INFO\norg.hibernate.type.descriptor.sql.BasicBinder=TRACE"` |  |
| server.conf.server | string | `"server.env=dev\n## Identity Provider authorization parameters\n# examples:\n# authorization=enable\n# authorization-url=https://accounts.google.com/o/oauth2/auth\n# token-url=https://oauth2.googleapis.com/token\n# client-id=111122223333-abab1212cdcd3434.apps.googleusercontent.com\n# client-secret=GOCSPX-ababfoobarcdcd-5q\nserver.authorization=disable\nserver.authorization-url=\nserver.token-url=\nserver.client-id=\nserver.client-secret=\nserver.redirect-port=\n# D-Days H-Hours M-Minutes S-Seconds (P5D = 5 days,PT5H = 5 hours, PT5M = 5 minutes, PT5S = 5 seconds)\nserver.cookie-timeout=P5D\n\n# Define the model storage root.  Cloud storage or file based allowed.\n# If no root specified, the current working directory of the server is used.\n\n#storage-root.models=s3://my-s3-bucket/root\n#storage-root.models=abfs://file_system@account_name.dfs.core.windows.net/root\n#storage-root.models=gs://my-gc-bucket/root\nstorage-root.models=file:/tmp/ucroot\n\n## S3 Storage Config (Multiple configs can be added by incrementing the index)\ns3.bucketPath.0=\ns3.region.0=\ns3.awsRoleArn.0=\n# Optional (If blank, it will use DefaultCredentialsProviderChain)\ns3.accessKey.0=\ns3.secretKey.0=\n# Test Only (If you provide a session token, it will just use those session creds, no downscoping)\ns3.sessionToken.0=\n\n## ADLS Storage Config (Multiple configs can be added by incrementing the index)\nadls.storageAccountName.0=\nadls.tenantId.0=\nadls.clientId.0=\nadls.clientSecret.0=\n\n## GCS Storage Config (Multiple configs can be added by incrementing the index)\ngcs.bucketPath.0=\n# Optional (If blank, it will use Default Application chain to find credentials)\ngcs.jsonKeyFilePath.0="` |  |
| server.serviceAccount.create | bool | `true` |  |
| server.serviceAccount.automount | bool | `true` |  |
| server.serviceAccount.annotations | object | `{}` |  |
| server.serviceAccount.name | string | `""` |  |
| server.podAnnotations | object | `{}` |  |
| server.podLabels | object | `{}` |  |
| server.podSecurityContext | object | `{}` |  |
| server.securityContext | object | `{}` |  |
| server.service.type | string | `"ClusterIP"` |  |
| server.service.port | int | `8080` |  |
| server.ingress.enabled | bool | `false` |  |
| server.ingress.className | string | `""` |  |
| server.ingress.annotations | object | `{}` |  |
| server.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| server.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| server.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| server.ingress.tls | list | `[]` |  |
| server.resources | object | `{}` |  |
| server.livenessProbe.periodSeconds | int | `60` |  |
| server.livenessProbe.timeoutSeconds | int | `10` |  |
| server.livenessProbe.httpGet.path | string | `"/"` |  |
| server.livenessProbe.httpGet.port | string | `"http"` |  |
| server.readinessProbe.periodSeconds | int | `60` |  |
| server.readinessProbe.timeoutSeconds | int | `10` |  |
| server.readinessProbe.httpGet.path | string | `"/"` |  |
| server.readinessProbe.httpGet.port | string | `"http"` |  |
| server.metrics.enabled | bool | `false` |  |
| server.metrics.podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| server.metrics.podAnnotations."prometheus.io/port" | string | `"{{ .Values.containerPorts.metrics }}"` |  |
| server.metrics.serviceMonitor.enabled | bool | `false` |  |
| server.metrics.serviceMonitor.namespace | string | `""` |  |
| server.metrics.serviceMonitor.annotations | object | `{}` |  |
| server.metrics.serviceMonitor.labels | object | `{}` |  |
| server.metrics.serviceMonitor.jobLabel | string | `""` |  |
| server.metrics.serviceMonitor.honorLabels | bool | `false` |  |
| server.metrics.serviceMonitor.interval | string | `""` |  |
| server.metrics.serviceMonitor.scrapeTimeout | string | `""` |  |
| server.metrics.serviceMonitor.metricRelabelings | list | `[]` |  |
| server.metrics.serviceMonitor.relabelings | list | `[]` |  |
| server.metrics.serviceMonitor.selector | object | `{}` |  |
| server.autoscaling.enabled | bool | `false` |  |
| server.autoscaling.minReplicas | int | `1` |  |
| server.autoscaling.maxReplicas | int | `100` |  |
| server.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| server.volumes | list | `[]` |  |
| server.volumeMounts | list | `[]` |  |
| server.nodeSelector | object | `{}` |  |
| server.tolerations | list | `[]` |  |
| server.affinity | object | `{}` |  |
| server.mysql.enabled | bool | `false` |  |
| server.postgresql.enabled | bool | `false` |  |
| server.postgresql-ha.enabled | bool | `false` |  |
| ui.create | bool | `true` |  |
| ui.replicaCount | int | `1` |  |
| ui.image.repository | string | `"greypavan/unity-catalog-ui"` |  |
| ui.image.pullPolicy | string | `"IfNotPresent"` |  |
| ui.image.tag | string | `"main"` |  |
| ui.imagePullSecrets | list | `[]` |  |
| ui.nameOverride | string | `""` |  |
| ui.fullnameOverride | string | `""` |  |
| ui.serviceAccount.create | bool | `true` |  |
| ui.serviceAccount.automount | bool | `true` |  |
| ui.serviceAccount.annotations | object | `{}` |  |
| ui.serviceAccount.name | string | `""` |  |
| ui.podAnnotations | object | `{}` |  |
| ui.podLabels | object | `{}` |  |
| ui.podSecurityContext | object | `{}` |  |
| ui.securityContext | object | `{}` |  |
| ui.service.type | string | `"ClusterIP"` |  |
| ui.service.port | int | `3000` |  |
| ui.ingress.enabled | bool | `false` |  |
| ui.ingress.className | string | `""` |  |
| ui.ingress.annotations | object | `{}` |  |
| ui.ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ui.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ui.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ui.ingress.tls | list | `[]` |  |
| ui.resources | object | `{}` |  |
| ui.livenessProbe.httpGet.path | string | `"/"` |  |
| ui.livenessProbe.httpGet.port | string | `"http"` |  |
| ui.readinessProbe.httpGet.path | string | `"/"` |  |
| ui.readinessProbe.httpGet.port | string | `"http"` |  |
| ui.autoscaling.enabled | bool | `false` |  |
| ui.autoscaling.minReplicas | int | `1` |  |
| ui.autoscaling.maxReplicas | int | `100` |  |
| ui.autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| ui.volumes | list | `[]` |  |
| ui.volumeMounts | list | `[]` |  |
| ui.nodeSelector | object | `{}` |  |
| ui.tolerations | list | `[]` |  |
| ui.affinity | object | `{}` |  |

## Naming convention for ConfigMap, Secret, SealedSecret and ExternalSecret

Name format of ConfigMap, Secret, SealedSecret and ExternalSecret is `{{ template "application.name" $ }}-{{ $nameSuffix }}` then:

- `{{ template "application.name" }}` is a helper function that outputs `.Values.applicationName` if exist else return chart name as output
- `nameSuffix` is the each key in `secret.files`, `configMap.files`, `sealedSecret.files` and `externalSecret.files`

For example if we have following values file:

```yaml
applicationName: helloworld # {{ template "application.name" $ }}

configMap:
  files:
    config: # {{ $nameSuffix }}
      key: value
```

then the configmap name will be named `helloworld-config`.

## Consuming extra JARS in your unity catalog server

In order to download extra JARS to the Unity catalog server, you can pass them to the Values file and they are downloaded through a curl command

- For simple key/value environment variable, just provide `value: <value>`

  ```yaml
  extraJars:
    - name: mysql-connector-j
      version: 9.1.0
      url: "https://repo.maven.apache.org/maven2/com/mysql/mysql-connector-j/9.1.0/mysql-connector-j-9.1.0.jar"
  ```

 - To get environement variable value from **ConfigMap**

   Suppose we have a configmap created from application chart

   ```yaml
   applicationName: my-application
   configMap:
     enabled: true
     files:
       application-config:
         LOG: DEBUG
         VERBOSE: v1
   ```

   To get environment variable value from above created configmap, we will need to add following

   ```yaml
   env:
    APP_LOG_LEVEL:
     valueFrom:
       configMapKeyRef:
         name: my-application-application-config
         key: LOG
   ```

   To get all environment variables key/values from **ConfigMap**, where configmap key being key of environment variable and value being value

   ```yaml
   envFrom:
     application-config-env:
       type: configmap
       nameSuffix: application-config
   ```

   You can either provide `nameSuffix` which means name added after prefix `<applicationName>-` or static name with `name` of configmap.

- To get environment variable value from **Secret**

   Suppose we have secret created from application chart

   ```yaml
   applicationName: my-application
   secret:
     enabled: true
     files:
        db-credentials:
          PASSWORD: skljd#2Qer!!
          USER: postgres
   ```

   To get environment variable value from above created secret, we will need to add following

   ```yaml
   env:
     KEY:
       valueFrom:
       secretKeyRef:
         name: my-application-db-credentials
         key: USER
   ```

   To get environement variable value from **Secret**, where secret key being key of environment variable and value being value

   ```yaml
   envFrom:
     database-credentials:
        type: secret
        nameSuffix: db-credentials
   ```
   you can either provide `nameSuffix` which means name added after prefix `<applicationName>-` or static name with `name` of secret

   **Note:** first key after `envFrom` is just used to uniquely identify different objects in `envFrom` block. Make sure to keep it unique and relevant

## Configuring probes

To disable liveness or readiness probe, set value of `enabled` to `false`.

```yaml
livenessProbe:
  enabled: false
```

By default probe handler type is `httpGet`. You just need to override `port` and `path` as per your need.

```yaml
livenessProbe:
  enabled: true
  httpGet:
    path: '/path'
    port: 8080
```

In order to use `exec` handler, you can define field `livenessProbe.exec` in your values.yaml.

```yaml
livenessProbe:
  enabled: true
  exec:
    command:
      - cat
      - /tmp/healthy
```
