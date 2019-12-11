# InfluxDB-srelay Helm Chart

[InfluxDB-srelay](https://github.com/toni-moreno/influxdb-srelay) is an InfluxDB proxy for achieving a highly available setup on 2 InfluxDB instances. 

## TL;DR;

```console
$ helm install influxdb-srelay --values values.yaml
```

## Introduction
[InfluxDB-srelay](https://github.com/toni-moreno/influxdb-srelay) adds a basic high availability layer to InfluxDB. With [Syncflux](https://github.com/toni-moreno/syncflux)(which is already built-in) as disaster recovery processes, this achieves a highly available setup.

## Limitions

- Support Http and UDP connection
- Support /write requests
- Support GET /query requests like SELECT, SHOW 
- POST /query requests like ALTER, CREATE, DELETE, DROP, GRANT, KILL, REVOKE, SELECT INTO are ```NOT SUPPORTED```!
- ```DO NOT``` use GET /query to send POST query command like ALTER, CREATE etc, the request can be sent to only one influxdb instance.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release influxdb-srelay --values values.yaml
```

The command deploys InfluxDB-srelay on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

| Parameter                                    | Description                                                                                                                                                                   | Default                                            |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| `busybox.image`                              | `busybox` image repository                                                                                                                                                    | `registry.icp.com:5000/library/common/busybox`     |
| `busybox.imageTag`                           | `busybox` image tag                                                                                                                                                           | `1.30.1`                                           |
| `srelay.image`                               | `influxdb-srelay` image repository                                                                                                                                            | `registry.icp.com:5000/service/db/influxdb-srelay` |
| `srelay.imageTag`                            | `influxdb-srelay` image tag                                                                                                                                                   | `0.6.0`                                            |
| `srelay.resources`                           | `influxdb-srelay` resource requests/limit                                                                                                                                     | `{}`                                               |
| `srelay.livenessProbe.initialDelaySeconds`   | Delay before liveness probe is initiated (influxdb-srelay container)                                                                                                          | `5`                                                |
| `srelay.livenessProbe.periodSeconds`         | How often to perform the probe (influxdb-srelay container)                                                                                                                    | `10`                                               |
| `srelay.livenessProbe.timeoutSeconds`        | When the probe times out (influxdb-srelay container)                                                                                                                          | `1`                                                |
| `srelay.livenessProbe.successThreshold`      | Minimum consecutive successes for the probe to be considered successful after having failed (influxdb-srelay container)                                                       | `1`                                                |
| `srelay.livenessProbe.failureThreshold`      | Minimum consecutive failures for the probe to be considered failed after having succeeded. (influxdb-srelay container)                                                        | `3`                                                |
| `srelay.readinessProbe.initialDelaySeconds`  | Delay before readiness probe is initiated (influxdb-srelay container)                                                                                                         | `5`                                                |
| `srelay.readinessProbe.periodSeconds`        | How often to perform the probe (influxdb-srelay container)                                                                                                                    | `10`                                               |
| `srelay.readinessProbe.timeoutSeconds`       | When the probe times out (influxdb-srelay container)                                                                                                                          | `1`                                                |
| `srelay.readinessProbe.successThreshold`     | Minimum consecutive successes for the probe to be considered successful after having failed (influxdb-srelay container)                                                       | `1`                                                |
| `srelay.readinessProbe.failureThreshold`     | Minimum consecutive failures for the probe to be considered failed after having succeeded. (influxdb-srelay container)                                                        | `3`                                                |
| `syncflux.image`                             | `syncflux` image repository                                                                                                                                                   | `registry.icp.com:5000/service/db/syncflux`        |
| `syncflux.imageTag`                          | `syncflux` image tag                                                                                                                                                          | `0.6.5`                                            |
| `syncflux.resources`                         | `syncflux` resource requests/limit                                                                                                                                            | `{}`                                               |
| `syncflux.livenessProbe.initialDelaySeconds` | Delay before liveness probe is initiated (syncflux container)                                                                                                                 | `30`                                               |
| `syncflux.livenessProbe.periodSeconds`       | How often to perform the probe (syncflux container)                                                                                                                           | `10`                                               |
| `syncflux.livenessProbe.timeoutSeconds`      | When the probe times out (syncflux container)                                                                                                                                 | `1`                                                |
| `syncflux.livenessProbe.successThreshold`    | Minimum consecutive successes for the probe to be considered successful after having failed (syncflux container)                                                              | `1`                                                |
| `syncflux.livenessProbe.failureThreshold`    | Minimum consecutive failures for the probe to be considered failed after having succeeded. (syncflux container)                                                               | `3`                                                |
| `syncflux.readinessProbe.initialDelaySeconds`| Delay before readiness probe is initiated (syncflux container)                                                                                                                | `30`                                               |
| `syncflux.readinessProbe.periodSeconds`      | How often to perform the probe (syncflux container)                                                                                                                           | `10`                                               |
| `syncflux.readinessProbe.timeoutSeconds`     | When the probe times out (syncflux container)                                                                                                                                 | `1`                                                |
| `syncflux.readinessProbe.successThreshold`   | Minimum consecutive successes for the probe to be considered successful after having failed (syncflux container)                                                              | `1`                                                |
| `syncflux.readinessProbe.failureThreshold`   | Minimum consecutive failures for the probe to be considered failed after having succeeded. (syncflux container)                                                               | `3`                                                |
| `imagePullPolicy`                            | image pull policy                                                                                                                                                             | `IfNotPresent`                                     |
| `imagePullSecrets`                           | Optionally specify an array of imagePullSecrets.                                                                                                                              | `[]`                                               |
| `schedulerName`                              | Scheduler name for influxdb-srelay pod assignment                                                                                                                             | ``                                                 |
| `nodeSelector`                               | Node labels influxdb-srelay pod assignment                                                                                                                                    | `{}`                                               |
| `affinity`                                   | Affinity settings for influxdb-srelay pod assignment                                                                                                                          | `{}`                                               |
| `tolerations`                                | Toleration labels for influxdb-srelay pod assignment                                                                                                                          | `[]`                                               |
| `deploymentAnnotations`                      | Annotations for influxdb-srelay statefulset                                                                                                                                   | `{}`                                               |
| `podAnnotations`                             | Annotations for influxdb-srelay pods                                                                                                                                          | `{}`                                               |
| `podLabels`                                  | Labels for influxdb-srelay pods                                                                                                                                               | `{}`                                               |
| `service.annotations`                        | Annotations for influxdb-srelay service                                                                                                                                       | `{}`                                               |
| `service.type`                               | Type for influxdb-srelay service                                                                                                                                              | `ClusterIP`                                        |
| `service.port`                               | Port for influxdb-srelay service                                                                                                                                              | `9096`                                             |
| `service.nodePort`                           | NodePort for influxdb-srelay service                                                                                                                                          | ``                                                 |
| `service.loadBalancerIP`                     | LoadbalancerIP if influxdb-srelay service is `LoadBalancer`                                                                                                                   | ``                                                 |
| `tls.enabled`                                | Setup and use TLS for influxdb-srelay connections                                                                                                                             | `flase`                                            |
| `tls.cert`                                   | Server certificate (public key)                                                                                                                                               | ``                                                 |
| `tls.key`                                    | Server key (private key)                                                                                                                                                      | ``                                                 |
| `influxdbCluster.node1.location`             | The first InfluxDB location (```Required```)                                                                                                                                  | ``                                                 |
| `influxdbCluster.node1.timeout`              | The first InfluxDB connection timeout                                                                                                                                         | `10s`                                              |
| `influxdbCluster.node1.adminUser`            | The first InfluxDB admin user                                                                                                                                                 | ``                                                 |
| `influxdbCluster.node1.adminPassword`        | The first InfluxDB admin password                                                                                                                                             | ``                                                 |
| `influxdbCluster.node2.location`             | The second InfluxDB location (```Required```)                                                                                                                                 | ``                                                 |
| `influxdbCluster.node2.timeout`              | The second InfluxDB connection timeout                                                                                                                                        | `10s`                                              |
| `influxdbCluster.node2.adminUser`            | The second InfluxDB admin user                                                                                                                                                | ``                                                 |
| `influxdbCluster.node2.adminPassword`        | The second InfluxDB admin password                                                                                                                                            | ``                                                 |
| `config.rateLimit`                           | Request limits per second                                                                                                                                                     | `1000000`                                          |
| `config.burstLimit`                          | Request burst limits per second                                                                                                                                               | `2000000`                                          |
| `config.checkInterval`                       | The inteval for health cheking for both master and slave databases                                                                                                            | `10s`                                              |
| `config.minSyncInterval`                     | The inteval in which HA monitor will check both are ok and change                                                                                                             | `20s`                                              |
| `config.initialReplication`                  | Tells syncflux if needed some type of replication on slave database from master database on initialize                                                                        | `none`                                             |
| `config.monitorRetryInterval`                | syncflux only can begin work when master and slave database are both up, if some of them is down synflux will retry infinitely each monitor-retry-interval to work.           | `30s`                                              |
| `config.dataChuckDuration`                   | Duration for each small, read  from master -> write to slave, chuck of data                                                                                                   | `5m`                                               |
| `config.maxRetentionInterval`                | For infinite ( or bigger ) retention policies full replication should begin somewhere in the time                                                                             | `8760h`                                            |
| `config.rwMaxRetries`                        | If any of the read ( from master) or write ( to slave ) querys fails, the query will be repeated at leas rw-max-retries                                                       | `5`                                                |
| `config.rwRetryDelay`                        | If any of the read ( from master) or write ( to slave ) querys fails, the query will be repeated at leas rw-max-retries and we can force a pause from at least rw-retry-delay | `10s`                                              |
| `config.numWorkers`                          | Num paralel  workers querying and writting at time on both databases (master & slave)                                                                                         | `4`                                                |
| `config.maxPointsOnSingleWrite`              | Syncflux splits  all chunk data  to write into multiple writes of max-points-on-single-write                                                                                  | `20000`                                            |
                                                                                                                                                                                                                                                                                    
[influxdb-srelay config example]: https://github.com/toni-moreno/influxdb-srelay/blob/master/examples/sample.influxdb-srelay.conf
[syncflux config example]: https://github.com/toni-moreno/syncflux/blob/master/conf/sample.syncflux.toml

