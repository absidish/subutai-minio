# Subutai Minio Blueprint 

## Minio version is: `2019-04-23T23:50:36Z`

# NOTE `Subutai container does not support O_DIRECT at this moment, we can update minio after enable it.`


**Subutai Minio Blueprint** to install MinIO in distributed mode.

![wizard](https://ipfs.subutai.io/ipfs/QmSqVD4eu8HaZk1PXgwoMVNNX2B1yHJFvyrm4a5wjd3Cus/minioWizardMini.png)

## How to enable https

Add port mapping to all containers: external port is https **443** and internal port is **9199**, **ssl_backend** should be enabled,  provide a **custom SSL certificate** in the following single file format:

### Example:

![portmapping](https://ipfs.subutai.io/ipfs/QmcFuie2ru5KiUw2T14waRvkCgsjiCL92X9rtTpT15wDZg/miniport.png)

## SSL certificate format:
```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----

-----BEGIN PRIVATE KEY-----
...
-----END PRIVATE KEY-----
```

## NOTE:

1. Minio is designed to deploy once and forget. You can not add new disks to an existing configuration.
2. Minio does not support the addition of new nodes (only repair downed nodes)
3. Clusters continue to operate as long as (nodes_count / 2) + 1 nodes are running 

## Useful

MinIO Client (mc) provides a modern alternative to UNIX commands like ls, cat, cp, mirror, diff, find etc.

Add a node to the `mc` client:

```shell
mc config host add minio http://node-ip:9199 accessKey secretKey
```

Get information about a cluster with `mc`:

```shell
mc admin info minio
```

Sync a minio node with `mc`:

```shell
mc admin heal -r minio
```

Add a bucket (a la S3) with `mc`:

```shell
mc mb minio/mybucket
```

### How to fix a dead node:

1) Fix its corrupted disk

2) Make sure the minio service has started and is running

3) Sync minio node with cmd: 

```shell
mc admin heal -r minio
```

