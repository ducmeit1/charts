## KongA for Kubernetes

[KongA for Dashboard Monitoring Kong](https://github.com/pantsel/konga) is an open-source Dashboard Monitoring for [Kong](https://github.com/Kong/kong)

This chart bootstraps all the components needed to run KongA on a
[Kubernetes](http://kubernetes.io) cluster using the
[Helm](https://helm.sh) package manager.

## TL;DR;
```bash
helm repo add konga https://ducmeit1.github.io/charts
helm repo update
helm install konga/konga
```

## Prerequisites

- Kubernetes 1.12+
- PV provisioner support in the underlying infrastructure if persistence
  is needed for Kong datastore.

## Install

To install the chart with the release `my-release`:

```bash
helm repo add konga https://ducmeit1.github.io/charts
helm repo update
helm install --name myrelease konga/konga
```

## Uninstall

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

Addition: You may add arguments `--purge` for remove clean.

The command removes all the Kubernetes components associated with the
chart and deletes the release.

> **Tip**: List all releases using `helm list`

## Database

Konga is bundled with It's own persistence mechanism for storing users and configuration.

A local persistent object store is used by default, which works great as a bundled, starter database (with the strict caveat that it is for non-production use only).

The application also supports some of the most popular databases out of the box:

- MySQL
- MongoDB
- PostgresSQL

In order to use them, set the appropriate env vars in your `config section`.

## Configuration

| Parameter                          | Description                                                                           | Default             |
| ---------------------------------- | ------------------------------------------------------------------------------------- | ------------------- |
| image.repository                   | KongA image                                                                            | `pantsel/konga`              |
| image.tag                          | KongA image version                                                                    | `0.14.7`               |
| image.pullPolicy                   | Image pull policy                                                                     | `IfNotPresent`      |
| image.pullSecrets                  | Image pull secrets                                                                    | `null`              |
| replicaCount                       | KongA instance count                                                                   | `1`                 |
| resources                          | Pods limits/requests resource                                              | `{}` |
| ingress.enabled | Enable/Disable set service ingress | `false` |
| ingress.hosts | Hosts of service ingress | `{}` |
| ingress.path | Routing path of service ingress | `/` |
| nodeSelector | Select node to deployment | `{}` |
| tolerations                        | List of node taints to tolerate                                                       | `[]`                |
| affinity                           | Node/pod affinities                                                                   |                     |
| config.host | The IP address that will be bind by Konga's server | `0.0.0.0` |
| config.port | The port that will be used by Konga's server | `1337` |
| config.node_env | The environment `(deployment | production)` | `deployment` |
| config.ssl_key_path | If you want to use SSL, this will be the absolute path to the .key file. Both SSL_KEY_PATH & SSL_CRT_PATH must be set. | |
| config.ssl_crt_path | If you want to use SSL, this will be the absolute path to the .crt file. Both SSL_KEY_PATH & SSL_CRT_PATH must be set. | |
| config.konga_hook_timeout | If you want to use SSL, this will be the absolute path to the .crt file. Both SSL_KEY_PATH & SSL_CRT_PATH must be set. | 60000 |
| config.db_adapter | The database that Konga will use. If not set, the localDisk db will be used. | `postgres` |
| config.db_uri | The full db connection string. Depends on DB_ADAPTER. If this is set, no other DB related var is needed. | |
| config.db_host | If DB_URI is not specified, this is the database host. Depends on DB_ADAPTER. | `localhost` |
| config.db_port | If DB_URI is not specified, this is the database port. Depends on DB_ADAPTER. | `5432` |
| config.db_user | If DB_URI is not specified, this is the database user. Depends on DB_ADAPTER. | |
| config.db_password | If DB_URI is not specified, this is the database user's password. Depends on DB_ADAPTER. | |
| config.db_database | If DB_URI is not specified, this is the name of Konga's db. Depends on DB_ADAPTER. | `konga` |
| config.db_pg_schema | If using postgres as a database, this is the schema that will be used. | If using postgres as a database, this is the schema that will be used. | `public` |
| config.log_level | The logging level (`silly`,`debug`,`info`,`warn`,`error`) | `debug` for `deployment` env - `warn` for `production` env |
| config.token_secret | The secret that will be used to sign JWT tokens issued by Konga | |