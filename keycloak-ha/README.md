# Helm Chart Values

## Global Container Image Configuration
| Parameter                | Description                                          | Default                 |
|--------------------------|------------------------------------------------------|-------------------------|
| `global.registry`        | Global container image registry                      | `docker.io`             |
| `global.repository`      | Global container image repository                    | `coredgeio`             |
| `global.imagePullPolicy` | Global container image pull policy                   | `Always`                |
| `global.imagePullSecrets`| Global container image pull secrets                  | `[]`                    |
| `global.storageClass`    | Global storage class for persistent volumes          | `""`                    |

## Keycloak Configuration
| Parameter                | Description                                          | Default                 |
|--------------------------|------------------------------------------------------|-------------------------|
| `replicaCount`           | Keycloak replica count                               | `3`                     |
| `image.name`             | Keycloak image name                                  | `keycloak`              |
| `image.tag`              | Keycloak image tag                                   | `24.0.5`                |
| `auth.adminUser`         | Keycloak administrator username                      | `admin`                 |
| `auth.adminPass`         | Keycloak administrator password                      | `admin`                 |
| `service.type`           | Keycloak service type                                | `NodePort`              |
| `service.nodePorts.http` | NodePort for HTTP                                    | `""`                    |
| `service.nodePorts.https`| NodePort for HTTPS                                   | `""`                    |
| `themeOverride.enabled`  | Enable custom themes                                 | `false`                 |
| `themeOverride.default`  | Default theme                                        | `""`                    |
| `themeOverride.welcome`  | Welcome theme                                        | `""`                    |
| `themeOverride.admin`    | Admin theme                                          | `""`                    |
| `resources`              | Resource requests and limits                         | `{}`                    |
| `customCaExistingSecret` | Name of the secret containing custom CA certificates | `""`                    |
| `tls.enabled`            | Enable TLS                                           | `true`                  |
| `tls.selfSigned`         | Use self-signed TLS certificates                     | `true`                  |
| `tls.tlsSecretName`      | Name of the existing secret containing TLS certs     | `""`                    |
| `production`             | Run Keycloak in production mode                      | `true`                  |
| `proxy`                  | Proxy mode (`edge`, `reencrypt`, `passthrough`, `none`)| `edge`                |
| `httpRelativePath`       | Path relative to `/` for serving resources           | `/auth/`                |
| `ingress.enabled`        | Enable user-facing ingress                           | `false`                 |
| `ingress.className`      | Ingress class name                                   | `""`                    |
| `ingress.extraAnnotations`| Additional ingress annotations                      | `{}`                    |
| `ingress.hostname`       | Ingress hostname                                     | `""`                    |
| `ingress.tlsSecret`      | TLS secret for ingress                               | `""`                    |
| `adminIngress.enabled`   | Enable admin ingress                                 | `false`                 |
| `adminIngress.className` | Admin ingress class name                             | `""`                    |
| `adminIngress.extraAnnotations`| Additional admin ingress annotations           | `{}`                    |
| `adminIngress.hostname`  | Admin ingress hostname                               | `""`                    |
| `adminIngress.tlsSecret` | TLS secret for admin ingress                         | `""`                    |
| `logging.output`         | Logging output format                                | `default`               |
| `logging.level`          | Logging level                                        | `INFO`                  |
| `autoscaling.enabled`    | Enable HPA autoscaling                               | `false`                 |
| `autoscaling.minReplicas`| Minimum number of replicas for autoscaling           | `1`                     |
| `autoscaling.maxReplicas`| Maximum number of replicas for autoscaling           | `100`                   |
| `autoscaling.targetCPUUtilizationPercentage`| Target CPU utilization percentage for autoscaling | `80`             |
| `autoscaling.targetMemoryUtilizationPercentage`| Target memory utilization percentage for autoscaling | `80`         |
| `volumes`                | Additional volumes                                   | `[]`                    |
| `volumeMounts`           | Additional volume mounts                             | `[]`                    |
| `command`                | Override command                                     | `[]`                    |
| `nodeSelector`           | Node selector for pod scheduling                     | `{}`                    |
| `tolerations`            | Tolerations for pod scheduling                       | `[]`                    |
| `affinity`               | Affinity rules for pod scheduling                    | `{}`                    |

## PostgreSQL Cluster Configuration
| Parameter                       | Description                                          | Default                 |
|---------------------------------|------------------------------------------------------|-------------------------|
| `pgcluster.name`                | PostgreSQL cluster name                              | `keycloak`              |
| `pgcluster.image`               | PostgreSQL cluster image                             | `docker.io/coredgeio/spilo-16:3.2-p3`|
| `pgcluster.postgresVersion`     | PostgreSQL version                                   | `15`                    |
| `pgcluster.replica`             | Number of replicas in the PostgreSQL cluster         | `3`                     |
| `pgcluster.loadBalancer.master` | Enable load balancer for master                      | `false`                 |
| `pgcluster.loadBalancer.replica`| Enable load balancer for replicas                    | `false`                 |
| `pgcluster.connectionPooler.instances`| Number of connection pooler instances         | `1`                     |
| `pgcluster.volume.size`         | Volume size for the PostgreSQL cluster               | `10Gi`                  |
| `pgcluster.monitoring.enabled`  | Enable monitoring                                    | `false`                 |

## PostgreSQL Operator Configuration
| Parameter                       | Description                                          | Default                 |
|---------------------------------|------------------------------------------------------|-------------------------|
| `postgres-operator.enabled`     | Enable PostgreSQL operator                           | `true`                  |
| `postgres-operator.registry`    | PostgreSQL operator image registry                   | `docker.io`             |
| `postgres-operator.repository`  | PostgreSQL operator image repository                 | `coredgeio/postgres-operator`|
| `postgres-operator.tag`         | PostgreSQL operator image tag                        | `v1.12.2`               |
| `postgres-operator.pullPolicy`  | PostgreSQL operator image pull policy                | `IfNotPresent`          |
| `postgres-operator.configMajorVersionUpgrade.major_version_upgrade_mode`| Major version upgrade mode | `off`          |
| `postgres-operator.configMajorVersionUpgrade.minimal_major_version`| Minimal major version | `12`                 |
| `postgres-operator.configMajorVersionUpgrade.target_major_version`| Target major version | `16`                    |
| `postgres-operator.configKubernetes.enable_cross_namespace_secret`| Enable cross namespace secret | `false`      |
| `postgres-operator.configKubernetes.enable_sidecars`| Enable sidecars                    | `true`                  |
| `postgres-operator.configKubernetes.storage_resize_mode`| Storage resize mode            | `pvc`                   |
| `postgres-operator.configKubernetes.watched_namespace`| Watched namespace                | `*`                     |
| `postgres-operator.configConnectionPooler.connection_pooler_image`| Connection pooler image | `docker.io/coredgeio/pgbouncer:master-32`|
| `postgres-operator.configConnectionPooler.connection_pooler_max_db_connections`| Max DB connections | `500`               |
| `postgres-operator.resources.limits.cpu`| CPU limits                                | `400m`                  |
| `postgres-operator.resources.limits.memory`| Memory limits                          | `500Mi`                 |
| `postgres-operator.resources.requests.cpu`| CPU requests                             | `100m`                  |
| `postgres-operator.resources.requests.memory`| Memory requests                       | `250Mi`                 |
| `postgres-operator.nodeSelector`| Node selector for PostgreSQL operator pod scheduling | `{}`                   |
| `postgres-operator.affinity`    | Affinity rules for PostgreSQL operator pod scheduling | `{}`                   |
| `postgres-operator.tolerations` | Tolerations for PostgreSQL operator pod scheduling    | `[]`                   |
| `postgres-operator.serviceAccount.name`| Service account name for PostgreSQL operator | `postgresql-operator` |