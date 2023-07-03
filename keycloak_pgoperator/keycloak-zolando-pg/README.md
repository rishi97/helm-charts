<!--- app-name: Keycloak -->

# Keycloak packaged by Bitnami

Keycloak is a high performance Java-based identity and access management solution. It lets developers add an authentication layer to their applications with minimum effort.

[Overview of Keycloak](https://www.keycloak.org/)


## Introduction

Bitnami charts for Helm are carefully engineered, actively maintained and are the quickest and easiest way to deploy containers on a Kubernetes cluster that are ready to handle production workloads.

This chart bootstraps a [Keycloak](https://github.com/bitnami/containers/tree/main/bitnami/keycloak) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.dev/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm dependency build <chart-name>
helm package <chart-name>
helm install <release-name> <packaged-chart-name.tgz> -n <namespace> --create-namespace
```
These commands deploy a Keycloak application on the Kubernetes cluster in the default configuration.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install <release-name> --set auth.adminPassword=secretpassword <packaged-chart-name.tgz> -n <namespace> --create-namespace
```

The above command sets the Keycloak administrator password to `secretpassword`.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm uninstall <release-name> -n <namespace>
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |

### Common parameters

| Name                     | Description                                                                             | Value           |
| ------------------------ | --------------------------------------------------------------------------------------- | --------------- |
| `kubeVersion`            | Force target Kubernetes version (using Helm capabilities if not set)                    | `""`            |
| `nameOverride`           | String to partially override common.names.fullname                                      | `""`            |
| `fullnameOverride`       | String to fully override common.names.fullname                                          | `""`            |
| `namespaceOverride`      | String to fully override common.names.namespace                                         | `""`            |
| `commonLabels`           | Labels to add to all deployed objects                                                   | `{}`            |
| `enableServiceLinks`     | If set to false, disable Kubernetes service links in the pod spec                       | `true`          |
| `commonAnnotations`      | Annotations to add to all deployed objects                                              | `{}`            |
| `dnsPolicy`              | DNS Policy for pod                                                                      | `""`            |
| `dnsConfig`              | DNS Configuration pod                                                                   | `{}`            |
| `clusterDomain`          | Default Kubernetes cluster domain                                                       | `cluster.local` |
| `extraDeploy`            | Array of extra objects to deploy with the release                                       | `[]`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden) | `false`         |
| `diagnosticMode.command` | Command to override all containers in the the statefulset                               | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the the statefulset                                  | `["infinity"]`  |

### Keycloak parameters

| Name                             | Description                                                                                                                  | Value                         |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| `image.registry`                 | Keycloak image registry                                                                                                      | `docker.io`                   |
| `image.repository`               | Keycloak image repository                                                                                                    | `bitnami/keycloak`            |
| `image.tag`                      | Keycloak image tag (immutable tags are recommended)                                                                          | `21.1.1-debian-11-r8`         |
| `image.digest`                   | Keycloak image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag                     | `""`                          |
| `image.pullPolicy`               | Keycloak image pull policy                                                                                                   | `IfNotPresent`                |
| `image.pullSecrets`              | Specify docker-registry secret names as an array                                                                             | `[]`                          |
| `image.debug`                    | Specify if debug logs should be enabled                                                                                      | `false`                       |
| `auth.adminUser`                 | Keycloak administrator user                                                                                                  | `user`                        |
| `auth.adminPassword`             | Keycloak administrator password for the new user                                                                             | `""`                          |
| `auth.existingSecret`            | Existing secret containing Keycloak admin password                                                                           | `""`                          |
| `auth.passwordSecretKey`         | Key where the Keycloak admin password is being stored inside the existing secret.                                            | `""`                          |
| `tls.enabled`                    | Enable TLS encryption. Required for HTTPs traffic.                                                                           | `false`                       |
| `tls.autoGenerated`              | Generate automatically self-signed TLS certificates. Currently only supports PEM certificates                                | `false`                       |
| `tls.existingSecret`             | Existing secret containing the TLS certificates per Keycloak replica                                                         | `""`                          |
| `tls.usePem`                     | Use PEM certificates as input instead of PKS12/JKS stores                                                                    | `false`                       |
| `tls.truststoreFilename`         | Truststore filename inside the existing secret                                                                               | `keycloak.truststore.jks`     |
| `tls.keystoreFilename`           | Keystore filename inside the existing secret                                                                                 | `keycloak.keystore.jks`       |
| `tls.keystorePassword`           | Password to access the keystore when it's password-protected                                                                 | `""`                          |
| `tls.truststorePassword`         | Password to access the truststore when it's password-protected                                                               | `""`                          |
| `tls.passwordsSecret`            | Secret containing the Keystore and Truststore passwords.                                                                     | `""`                          |
| `spi.existingSecret`             | Existing secret containing the Keycloak truststore for SPI connection over HTTPS/TLS                                         | `""`                          |
| `spi.truststorePassword`         | Password to access the truststore when it's password-protected                                                               | `""`                          |
| `spi.truststoreFilename`         | Truststore filename inside the existing secret                                                                               | `keycloak-spi.truststore.jks` |
| `spi.passwordsSecret`            | Secret containing the SPI Truststore passwords.                                                                              | `""`                          |
| `spi.hostnameVerificationPolicy` | Verify the hostname of the server’s certificate. Allowed values: "ANY", "WILDCARD", "STRICT".                                | `""`                          |
| `production`                     | Run Keycloak in production mode. TLS configuration is required except when using proxy=edge.                                 | `false`                       |
| `proxy`                          | reverse Proxy mode edge, reencrypt, passthrough or none                                                                      | `passthrough`                 |
| `httpRelativePath`               | Set the path relative to '/' for serving resources. Useful if you are migrating from older version which were using '/auth/' | `/`                           |
| `configuration`                  | Keycloak Configuration. Auto-generated based on other parameters when not specified                                          | `""`                          |
| `existingConfigmap`              | Name of existing ConfigMap with Keycloak configuration                                                                       | `""`                          |
| `extraStartupArgs`               | Extra default startup args                                                                                                   | `""`                          |
| `initdbScripts`                  | Dictionary of initdb scripts                                                                                                 | `{}`                          |
| `initdbScriptsConfigMap`         | ConfigMap with the initdb scripts (Note: Overrides `initdbScripts`)                                                          | `""`                          |
| `command`                        | Override default container command (useful when using custom images)                                                         | `[]`                          |
| `args`                           | Override default container args (useful when using custom images)                                                            | `[]`                          |
| `extraEnvVars`                   | Extra environment variables to be set on Keycloak container                                                                  | `[]`                          |
| `extraEnvVarsCM`                 | Name of existing ConfigMap containing extra env vars                                                                         | `""`                          |
| `extraEnvVarsSecret`             | Name of existing Secret containing extra env vars                                                                            | `""`                          |

### Keycloak statefulset parameters

| Name                                    | Description                                                                                                              | Value           |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `replicaCount`                          | Number of Keycloak replicas to deploy                                                                                    | `1`             |
| `containerPorts.http`                   | Keycloak HTTP container port                                                                                             | `8080`          |
| `containerPorts.https`                  | Keycloak HTTPS container port                                                                                            | `8443`          |
| `containerPorts.infinispan`             | Keycloak infinispan container port                                                                                       | `7800`          |
| `extraContainerPorts`                   | Optionally specify extra list of additional port-mappings for Keycloak container                                         | `[]`            |
| `podSecurityContext.enabled`            | Enabled Keycloak pods' Security Context                                                                                  | `true`          |
| `podSecurityContext.fsGroup`            | Set Keycloak pod's Security Context fsGroup                                                                              | `1001`          |
| `containerSecurityContext.enabled`      | Enabled Keycloak containers' Security Context                                                                            | `true`          |
| `containerSecurityContext.runAsUser`    | Set Keycloak container's Security Context runAsUser                                                                      | `1001`          |
| `containerSecurityContext.runAsNonRoot` | Set Keycloak container's Security Context runAsNonRoot                                                                   | `true`          |
| `resources.limits`                      | The resources limits for the Keycloak containers                                                                         | `{}`            |
| `resources.requests`                    | The requested resources for the Keycloak containers                                                                      | `{}`            |
| `livenessProbe.enabled`                 | Enable livenessProbe on Keycloak containers                                                                              | `true`          |
| `livenessProbe.initialDelaySeconds`     | Initial delay seconds for livenessProbe                                                                                  | `300`           |
| `livenessProbe.periodSeconds`           | Period seconds for livenessProbe                                                                                         | `1`             |
| `livenessProbe.timeoutSeconds`          | Timeout seconds for livenessProbe                                                                                        | `5`             |
| `livenessProbe.failureThreshold`        | Failure threshold for livenessProbe                                                                                      | `3`             |
| `livenessProbe.successThreshold`        | Success threshold for livenessProbe                                                                                      | `1`             |
| `readinessProbe.enabled`                | Enable readinessProbe on Keycloak containers                                                                             | `true`          |
| `readinessProbe.initialDelaySeconds`    | Initial delay seconds for readinessProbe                                                                                 | `30`            |
| `readinessProbe.periodSeconds`          | Period seconds for readinessProbe                                                                                        | `10`            |
| `readinessProbe.timeoutSeconds`         | Timeout seconds for readinessProbe                                                                                       | `1`             |
| `readinessProbe.failureThreshold`       | Failure threshold for readinessProbe                                                                                     | `3`             |
| `readinessProbe.successThreshold`       | Success threshold for readinessProbe                                                                                     | `1`             |
| `startupProbe.enabled`                  | Enable startupProbe on Keycloak containers                                                                               | `false`         |
| `startupProbe.initialDelaySeconds`      | Initial delay seconds for startupProbe                                                                                   | `30`            |
| `startupProbe.periodSeconds`            | Period seconds for startupProbe                                                                                          | `5`             |
| `startupProbe.timeoutSeconds`           | Timeout seconds for startupProbe                                                                                         | `1`             |
| `startupProbe.failureThreshold`         | Failure threshold for startupProbe                                                                                       | `60`            |
| `startupProbe.successThreshold`         | Success threshold for startupProbe                                                                                       | `1`             |
| `customLivenessProbe`                   | Custom Liveness probes for Keycloak                                                                                      | `{}`            |
| `customReadinessProbe`                  | Custom Rediness probes Keycloak                                                                                          | `{}`            |
| `customStartupProbe`                    | Custom Startup probes for Keycloak                                                                                       | `{}`            |
| `lifecycleHooks`                        | LifecycleHooks to set additional configuration at startup                                                                | `{}`            |
| `hostAliases`                           | Deployment pod host aliases                                                                                              | `[]`            |
| `podLabels`                             | Extra labels for Keycloak pods                                                                                           | `{}`            |
| `podAnnotations`                        | Annotations for Keycloak pods                                                                                            | `{}`            |
| `podAffinityPreset`                     | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                      | `""`            |
| `podAntiAffinityPreset`                 | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                 | `soft`          |
| `nodeAffinityPreset.type`               | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                | `""`            |
| `nodeAffinityPreset.key`                | Node label key to match. Ignored if `affinity` is set.                                                                   | `""`            |
| `nodeAffinityPreset.values`             | Node label values to match. Ignored if `affinity` is set.                                                                | `[]`            |
| `affinity`                              | Affinity for pod assignment                                                                                              | `{}`            |
| `nodeSelector`                          | Node labels for pod assignment                                                                                           | `{}`            |
| `tolerations`                           | Tolerations for pod assignment                                                                                           | `[]`            |
| `topologySpreadConstraints`             | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template | `[]`            |
| `podManagementPolicy`                   | Pod management policy for the Keycloak statefulset                                                                       | `Parallel`      |
| `priorityClassName`                     | Keycloak pods' Priority Class Name                                                                                       | `""`            |
| `schedulerName`                         | Use an alternate scheduler, e.g. "stork".                                                                                | `""`            |
| `terminationGracePeriodSeconds`         | Seconds Keycloak pod needs to terminate gracefully                                                                       | `""`            |
| `updateStrategy.type`                   | Keycloak statefulset strategy type                                                                                       | `RollingUpdate` |
| `updateStrategy.rollingUpdate`          | Keycloak statefulset rolling update configuration parameters                                                             | `{}`            |
| `extraVolumes`                          | Optionally specify extra list of additional volumes for Keycloak pods                                                    | `[]`            |
| `extraVolumeMounts`                     | Optionally specify extra list of additional volumeMounts for Keycloak container(s)                                       | `[]`            |
| `initContainers`                        | Add additional init containers to the Keycloak pods                                                                      | `[]`            |
| `sidecars`                              | Add additional sidecar containers to the Keycloak pods                                                                   | `[]`            |

### Exposure parameters

| Name                               | Description                                                                                                                      | Value                    |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `service.type`                     | Kubernetes service type                                                                                                          | `ClusterIP`              |
| `service.http.enabled`             | Enable http port on service                                                                                                      | `true`                   |
| `service.ports.http`               | Keycloak service HTTP port                                                                                                       | `80`                     |
| `service.ports.https`              | Keycloak service HTTPS port                                                                                                      | `443`                    |
| `service.nodePorts`                | Specify the nodePort values for the LoadBalancer and NodePort service types.                                                     | `{}`                     |
| `service.sessionAffinity`          | Control where client requests go, to the same pod or round-robin                                                                 | `None`                   |
| `service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                                                                                      | `{}`                     |
| `service.clusterIP`                | Keycloak service clusterIP IP                                                                                                    | `""`                     |
| `service.loadBalancerIP`           | loadBalancerIP for the SuiteCRM Service (optional, cloud specific)                                                               | `""`                     |
| `service.loadBalancerSourceRanges` | Address that are allowed when service is LoadBalancer                                                                            | `[]`                     |
| `service.externalTrafficPolicy`    | Enable client source IP preservation                                                                                             | `Cluster`                |
| `service.annotations`              | Additional custom annotations for Keycloak service                                                                               | `{}`                     |
| `service.extraPorts`               | Extra port to expose on Keycloak service                                                                                         | `[]`                     |
| `service.extraHeadlessPorts`       | Extra ports to expose on Keycloak headless service                                                                               | `[]`                     |
| `service.headless.annotations`     | Annotations for the headless service.                                                                                            | `{}`                     |
| `service.headless.extraPorts`      | Extra ports to expose on Keycloak headless service                                                                               | `[]`                     |
| `ingress.enabled`                  | Enable ingress record generation for Keycloak                                                                                    | `false`                  |
| `ingress.ingressClassName`         | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                     |
| `ingress.pathType`                 | Ingress path type                                                                                                                | `ImplementationSpecific` |
| `ingress.apiVersion`               | Force Ingress API version (automatically detected if not set)                                                                    | `""`                     |
| `ingress.hostname`                 | Default host for the ingress record (evaluated as template)                                                                      | `keycloak.local`         |
| `ingress.path`                     | Default path for the ingress record (evaluated as template)                                                                      | `""`                     |
| `ingress.servicePort`              | Backend service port to use                                                                                                      | `http`                   |
| `ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `ingress.tls`                      | Enable TLS configuration for the host defined at `ingress.hostname` parameter                                                    | `false`                  |
| `ingress.selfSigned`               | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                  |
| `ingress.extraHosts`               | An array with additional hostname(s) to be covered with the ingress record                                                       | `[]`                     |
| `ingress.extraPaths`               | Any additional arbitrary paths that may need to be added to the ingress under the main host.                                     | `[]`                     |
| `ingress.extraTls`                 | The tls configuration for additional hostnames to be covered with this ingress record.                                           | `[]`                     |
| `ingress.secrets`                  | If you're providing your own certificates, please use this to add the certificates as secrets                                    | `[]`                     |
| `ingress.extraRules`               | Additional rules to be covered with this ingress record                                                                          | `[]`                     |
| `networkPolicy.enabled`            | Enable the default NetworkPolicy policy                                                                                          | `false`                  |
| `networkPolicy.allowExternal`      | Don't require client label for connections                                                                                       | `true`                   |
| `networkPolicy.additionalRules`    | Additional NetworkPolicy rules                                                                                                   | `{}`                     |

### RBAC parameter

| Name                                          | Description                                               | Value   |
| --------------------------------------------- | --------------------------------------------------------- | ------- |
| `serviceAccount.create`                       | Enable the creation of a ServiceAccount for Keycloak pods | `true`  |
| `serviceAccount.name`                         | Name of the created ServiceAccount                        | `""`    |
| `serviceAccount.automountServiceAccountToken` | Auto-mount the service account token in the pod           | `true`  |
| `serviceAccount.annotations`                  | Additional custom annotations for the ServiceAccount      | `{}`    |
| `serviceAccount.extraLabels`                  | Additional labels for the ServiceAccount                  | `{}`    |
| `rbac.create`                                 | Whether to create and use RBAC resources or not           | `false` |
| `rbac.rules`                                  | Custom RBAC rules                                         | `[]`    |

### Other parameters

| Name                       | Description                                                    | Value   |
| -------------------------- | -------------------------------------------------------------- | ------- |
| `pdb.create`               | Enable/disable a Pod Disruption Budget creation                | `false` |
| `pdb.minAvailable`         | Minimum number/percentage of pods that should remain scheduled | `1`     |
| `pdb.maxUnavailable`       | Maximum number/percentage of pods that may be made unavailable | `""`    |
| `autoscaling.enabled`      | Enable autoscaling for Keycloak                                | `false` |
| `autoscaling.minReplicas`  | Minimum number of Keycloak replicas                            | `1`     |
| `autoscaling.maxReplicas`  | Maximum number of Keycloak replicas                            | `11`    |
| `autoscaling.targetCPU`    | Target CPU utilization percentage                              | `""`    |
| `autoscaling.targetMemory` | Target Memory utilization percentage                           | `""`    |

### Metrics parameters

| Name                                       | Description                                                                                                               | Value   |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- | ------- |
| `metrics.enabled`                          | Enable exposing Keycloak statistics                                                                                       | `false` |
| `metrics.service.ports.http`               | Metrics service HTTP port                                                                                                 | `8080`  |
| `metrics.service.annotations`              | Annotations for enabling prometheus to access the metrics endpoints                                                       | `{}`    |
| `metrics.serviceMonitor.enabled`           | Create ServiceMonitor Resource for scraping metrics using PrometheusOperator                                              | `false` |
| `metrics.serviceMonitor.port`              | Metrics service HTTP port                                                                                                 | `http`  |
| `metrics.serviceMonitor.endpoints`         | The endpoint configuration of the ServiceMonitor. Path is mandatory. Interval, timeout and labellings can be overwritten. | `[]`    |
| `metrics.serviceMonitor.path`              | Metrics service HTTP path. Deprecated: Use @param metrics.serviceMonitor.endpoints instead                                | `""`    |
| `metrics.serviceMonitor.namespace`         | Namespace which Prometheus is running in                                                                                  | `""`    |
| `metrics.serviceMonitor.interval`          | Interval at which metrics should be scraped                                                                               | `30s`   |
| `metrics.serviceMonitor.scrapeTimeout`     | Specify the timeout after which the scrape is ended                                                                       | `""`    |
| `metrics.serviceMonitor.labels`            | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus                                     | `{}`    |
| `metrics.serviceMonitor.selector`          | Prometheus instance selector labels                                                                                       | `{}`    |
| `metrics.serviceMonitor.relabelings`       | RelabelConfigs to apply to samples before scraping                                                                        | `[]`    |
| `metrics.serviceMonitor.metricRelabelings` | MetricRelabelConfigs to apply to samples before ingestion                                                                 | `[]`    |
| `metrics.serviceMonitor.honorLabels`       | honorLabels chooses the metric's labels on collisions with target labels                                                  | `false` |
| `metrics.serviceMonitor.jobLabel`          | The name of the label on the target service to use as the job name in prometheus.                                         | `""`    |
| `metrics.prometheusRule.enabled`           | Create PrometheusRule Resource for scraping metrics using PrometheusOperator                                              | `false` |
| `metrics.prometheusRule.namespace`         | Namespace which Prometheus is running in                                                                                  | `""`    |
| `metrics.prometheusRule.labels`            | Additional labels that can be used so PrometheusRule will be discovered by Prometheus                                     | `{}`    |
| `metrics.prometheusRule.groups`            | Groups, containing the alert rules.                                                                                       | `[]`    |

### Database parameters

| Name                                         | Description                                                                                                       | Value              |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------ |
| `postgresql.enabled`                         | Switch to enable or disable the PostgreSQL helm chart                                                             | `false`             |
| `externalDatabase.host`                      | Database host                                                                                                     | `""`               |
| `externalDatabase.port`                      | Database port number                                                                                              | `5432`             |
| `externalDatabase.user`                      | Non-root username for Keycloak                                                                                    | `bn_keycloak`      |
| `externalDatabase.password`                  | Password for the non-root username for Keycloak                                                                   | `""`               |
| `externalDatabase.database`                  | Keycloak database name                                                                                            | `bitnami_keycloak` |
| `externalDatabase.existingSecret`            | Name of an existing secret resource containing the database credentials                                           | `""`               |
| `externalDatabase.existingSecretHostKey`     | Name of an existing secret key containing the database host name                                                  | `""`               |
| `externalDatabase.existingSecretPortKey`     | Name of an existing secret key containing the database port                                                       | `""`               |
| `externalDatabase.existingSecretUserKey`     | Name of an existing secret key containing the database user                                                       | `""`               |
| `externalDatabase.existingSecretDatabaseKey` | Name of an existing secret key containing the database name                                                       | `""`               |
| `externalDatabase.existingSecretPasswordKey` | Name of an existing secret key containing the database credentials                                                | `""`               |

### Keycloak Cache parameters

| Name              | Description                                                                | Value        |
| ----------------- | -------------------------------------------------------------------------- | ------------ |
| `cache.enabled`   | Switch to enable or disable the keycloak distributed cache for kubernetes. | `true`       |
| `cache.stackName` | Set infinispan cache stack to use                                          | `kubernetes` |
| `cache.stackFile` | Set infinispan cache stack filename to use                                 | `""`         |

### Keycloak Logging parameters

| Name             | Description                                                                    | Value     |
| ---------------- | ------------------------------------------------------------------------------ | --------- |
| `logging.output` | Alternates between the default log output format or json format                | `default` |
| `logging.level`  | Allowed values as documented: FATAL, ERROR, WARN, INFO, DEBUG, TRACE, ALL, OFF | `INFO`    |


> NOTE: Once this chart is deployed, it is not possible to change the application's access credentials, such as usernames or passwords, using Helm. To change these application credentials after deployment, delete any persistent volumes (PVs) used by the chart and re-deploy it, or use the application's built-in administrative tools if available.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml oci://registry-1.docker.io/bitnamicharts/keycloak
```

> **Tip**: You can use the default [values.yaml](values.yaml)

Keycloak realms, users and clients can be created from the Keycloak administration panel. Refer to the [tutorial on adding user authentication to applications with Keycloak](https://docs.bitnami.com/tutorials/integrate-keycloak-authentication-kubernetes) for more details on these operations.

## Configuration and installation details

### Use an external database

Sometimes, you may want to have Keycloak connect to an external PostgreSQL database rather than a database within your cluster - for example, when using a managed database service, or when running a single database server for all your applications. To do this, set the `postgresql.enabled` parameter to `false` and specify the credentials for the external database using the `externalDatabase.*` parameters.

> NOTE: Only PostgreSQL database server is supported as external database

### Add extra environment variables

In case you want to add extra environment variables (useful for advanced operations like custom init scripts), you can use the `extraEnvVars` property.

```yaml
extraEnvVars:
  - name: KEYCLOAK_LOG_LEVEL
    value: DEBUG
```

Alternatively, you can use a ConfigMap or a Secret with the environment variables. To do so, use the `extraEnvVarsCM` or the `extraEnvVarsSecret` values.

### Use Sidecars and Init Containers

If additional containers are needed in the same pod (such as additional metrics or logging exporters), they can be defined using the `sidecars` config parameter. Similarly, extra init containers can be added using the `initContainers` parameter.

Refer to the chart documentation for more information on, and examples of, configuring and using [sidecars and init containers]

### Initialize a fresh instance

The Bitnami Keycloak image allows you to use your custom scripts to initialize a fresh instance. In order to execute the scripts, you can specify custom scripts using the `initdbScripts` parameter as dict.

In addition to this option, you can also set an external ConfigMap with all the initialization scripts. This is done by setting the `initdbScriptsConfigMap` parameter. Note that this will override the previous option.

The allowed extensions is `.sh`.

### Deploy extra resources

There are cases where you may want to deploy extra objects, such a ConfigMap containing your app's configuration or some extra deployment with a micro service used by your app. For covering this case, the chart allows adding the full specification of other objects using the `extraDeploy` parameter.


### Configure Ingress

This chart provides support for Ingress resources. If you have an ingress controller installed on your cluster, such as [nginx-ingress-controller](https://github.com/bitnami/charts/tree/main/bitnami/nginx-ingress-controller) or [contour](https://github.com/bitnami/charts/tree/main/bitnami/contour) you can utilize the ingress controller to serve your application.

To enable Ingress integration, set `ingress.enabled` to `true`. The `ingress.hostname` property can be used to set the host name. The `ingress.tls` parameter can be used to add the TLS configuration for this host. It is also possible to have more than one host, with a separate TLS configuration for each host. [Learn more about configuring and using Ingress](https://docs.bitnami.com/kubernetes/apps/keycloak/configuration/configure-ingress/).

### Configure TLS Secrets for use with Ingress

The chart also facilitates the creation of TLS secrets for use with the Ingress controller, with different options for certificate management. [Learn more about TLS secrets](https://docs.bitnami.com/kubernetes/apps/keycloak/administration/enable-tls-ingress/).

### Use with ingress offloading SSL

If your ingress controller has the SSL Termination, you should set `proxy` to `edge`.

### Manage secrets and passwords

This chart provides several ways to manage passwords:

- Values passed to the chart
- An existing secret with all the passwords (via the `existingSecret` parameter)
- Multiple existing secrets with all the passwords (via the `existingSecretPerPassword` parameter)


## License

Copyright &copy; 2023 VMware, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.