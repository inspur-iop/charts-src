# DBLE Helm Chart

[DBLE](https://opensource.actionsky.com/) is a high scalability middle-ware for MySQL sharding.

## TL;DR;

```console
$ helm repo add inspur https://inspur-iop.github.io/charts
$ helm install inspur/dble --values values.yaml
```

## Introduction
[DBLE](https://opensource.actionsky.com/) is a high scalability middle-ware for MySQL sharding maintained by ActionTech. 

## Features

- __Sharding__
As your business grows, you can use dble to replace the origin single MySQL instance. 

- __Compatible with MySQL protocol__
Use dble as same as MySQL. You can replace MySQL with dble to power your application without changing a single line of code in most cases.

- __High availability__
dble server can be used as clustered, business will not suffer from single node fail.

- __SQL Support__
Support(some in Roadmap) SQL 92 standard and MySQL dialect. We support complex SQL query like group by, order by, distinct, join ,union, sub-query(in Roadmap) and so on.

- __Complex Query Optimization__
Optimize the complex query, including, without limitation, Global-table join sharding-table, ER-relation tables, Sub-Queries, Simplifying select items, and the like.

- __Distributed Transaction__
Support Distributed Transaction using two-phase commit. You can choose normal mode for performance or XA mode for data safety, of course, the XA mode dependent on MySQL-5.7's XA Transaction, MySQL node's high availability and data reliability of disk.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add inspur https://inspur-iop.github.io/charts
$ helm install --name my-release inspur/dble --values values.yaml
```

The command deploys DBLE on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

| Parameter                                    | Description                                                                                                                      | Default                                            |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------| -------------------------------------------------- |
| `global.registry`                            | `dble` image repository                                                                                                         | `registry.icp.com:5000`                            |
| `global.arch`                                | `dble` image architecture, default is amd64                                                                                     | ``                                                 |
| `dble.image`                                 | `dble` image                                                                                                                    | `library/dble`                                    |
| `dble.imageTag`                              | `dble` image tag                                                                                                                | `2.19.09`                                            |
| `replicas`                                   | `dble` replicas                                                                                                                 | 2                                                  |
| `resources`                                  | `dble` resource requests/limit                                                                                                  | `{}`                                               |
| `imagePullPolicy`                            | image pull policy                                                                                                                | `IfNotPresent`                                     |
| `schedulerName`                              | Scheduler name for dble pod assignment                                                                                          | ``                                                 |
| `nodeSelector`                               | Node labels dble pod assignment                                                                                                 | `{}`                                               |
| `affinity`                                   | Affinity settings for dble pod assignment                                                                                       | `{}`                                               |
| `tolerations`                                | Toleration labels for dble pod assignment                                                                                       | `[]`                                               |
| `deploymentAnnotations`                      | Annotations for dble statefulset                                                                                                | `{}`                                               |
| `podAnnotations`                             | Annotations for dble pods                                                                                                       | `{}`                                               |
| `podLabels`                                  | Labels for dble pods                                                                                                            | `{}`                                               |
| `imagePullSecrets`                           | Optionally specify an array of imagePullSecrets.                                                                                 | `[]`                                               |
| `service.annotations`                        | Annotations for dble service                                                                                                    | `{}`                                               |
| `service.type`                               | Type for dble service                                                                                                           | `ClusterIP`                                        |
| `service.dble.port`                         | Port for dble service                                                                                                           | `8066`                                             |
| `service.dble.nodePort`                     | NodePort for dble service                                                                                                       | ``                                                 |
| `service.admin.port`                         | Port for dble management service                                                                                                | `9066`                                             |
| `service.admin.nodePort`                     | NodePort for dble management servic                                                                                             | ``                                                 |
| `service.loadBalancerIP`                     | LoadbalancerIP if dble service is `LoadBalancer`                                                                                | ``                                                 |
| `wrapperAdditionalParameters`                | Configurations about JVM in wrapper.conf. See https://actiontech.github.io/dble-docs-cn/1.config_file/1.04_wrapper.conf.html   | `["-XX:MaxPermSize=64M", "-XX:+AggressiveOpts", "-XX:MaxDirectMemorySize=1G", "-Xmx512m", "-Xms100m", "-XX:+UseParNewGC", "-XX:+UseConcMarkSweepGC", "-XX:+UseCMSCompactAtFullCollection", "-XX:CMSFullGCsBeforeCompaction=0", "-XX:CMSInitiatingOccupancyFraction=70"]` |                                                                                                                                                                                                                                          
| `configurationFiles`                         | DBLE configuration files, exclude wrapper.conf. For more details see https://actiontech.github.io/dble-docs-cn/1.config_file/1.00_config_file.html    | `[]`                                               |
| `zookeeper.resources`                        | `zookeeper` resource requests/limit                                                                                            | `{}`                                               |
| `zookeeper.persistence`                      | `zookeeper` data persistence                                                                                                   | `{}`                                               |
[For more DBLE configurations]: https://actiontech.github.io/dble-docs-cn/

