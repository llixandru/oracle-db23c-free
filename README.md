# Oracle Database
[Oracle](http://www.oracle.com)
Oracle Database 23c Free—Developer Release is the same, powerful Oracle Database that businesses throughout the world rely on. It offers a full-featured experience and is packaged for ease of use and simple download—for free.

## Getting started
A Helm chart is used for packaging the deployment yamls to simplify install in Kubernetes. The chart is available at [helm-charts/oracle-db](./) directory.
Clone the repo and execute the following command to generate oracle-db23c-free-1.0.0.tgz
```
$ helm package oracle-db23c-free
```

## Introduction

The Oracle Database Chart contains the Oracle Database 23c Free - Developer Release. 

For more information on Oracle Database 23c Free—Developer Release refer to https://www.oracle.com/database/free/

## Prerequisites

- Kubernetes 1.24+
- Helm 2.x or 3.x

## Installing the Chart

To install the chart with the release name `db23cfree`:

Helm 3.x syntax
```
$ helm install db23cfree oracle-db23c-free-1.0.0.tgz
```
Helm 2.x syntax
```
$ helm install --name db23cfree oracle-db23c-free-1.0.0.tgz
```

The command deploys Oracle Database on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `db23cfree` deployment:

Helm 3.x syntax
```
$ helm uninstall db23cfree 
```
Helm 2.x syntax
```
$ helm delete db23cfree
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Oracle  Database chart and their default values.

| Parameter                            | Description                                | Default                                                    |
| -------------------------------      | -------------------------------            | ---------------------------------------------------------- |
| oracle_sid                           | Database name (ORACLE_SID)                 | FREE                                                    |
| oracle_pdb                           | PDB name                                   | FREEPDB1                                                   |
| oracle_pwd                           | SYS, SYSTEM and PDB_ADMIN password         | Auto generated                                             |
| oracle_characterset                  | The character set to use                   | AL32UTF8                                                   |
| oracle_edition                       | The database edition                       | standard                                                 |
| persistence.size                     | Size of persistence storage                | 100g                                                       |
| persistence.storageClass             | Storage Class for PVC                      | oci-bv                                                           |
| loadBalService                       | Create a load balancer service instead of NodePort | false                                              |
| image                                | Image to pull                              | container-registry.oracle.com/database/free:latest |
| imagePullPolicy                      | Image pull policy                          | Always                                                     |
| imagePullSecrets                     | container registry login/password          |                                                            |
| enable_archivelog                    | Set true to enable archive log mode when creating the database | false                                                      |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

Helm 3.x syntax
```
$ helm install db23cfree --set oracle_sid=ORCL,oracle_pdb=dev oracle-db23c-free-1.0.0.tgz
```
Helm 2.x syntax
```
$ helm install --name db23cfree --set oracle_sid=ORCL,oracle_pdb=dev oracle-db23c-free-1.0.0.tgz
```

The above command sets  the Oracle Database name to 'ORCL' and PDB name to 'prod'.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

Helm 3.x syntax
```
$ helm install db23cfree -f values.yaml oracle-db23c-free-1.0.0.tgz
```
Helm 2.x syntax
```
$ helm install --name db23cfree -f values.yaml oracle-db23c-free-1.0.0.tgz
```

> **Tip**: You can use the default [values.yaml](values.yaml)
 

## Persistence

The [Oracle Database](https://www.oracle.com) image stores the Oracle Database data files  and configurations at the `/opt/oracle/oradata` path of the container.

Persistent Volume Claims are used to keep the data across deployments. 
See the [Configuration](#configuration) section to configure the PVC or to disable persistence.

