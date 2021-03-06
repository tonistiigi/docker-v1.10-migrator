### docker-v1.10-migrator

Starting from `v1.10` docker uses content addressable IDs for the images and layers instead of using generated ones. This tool calculates SHA256 checksums for docker layer content, so that they don't need to be recalculated when the daemon starts for the first time.

The migration usually runs on daemon startup but it can be quite slow(usually 100-200MB/s) and daemon will not be able to accept requests during that time. You can run this tool instead while the old daemon is still running and skip checksum calculation on startup.

#### Usage

```
docker-v1.10-migrator --help
Usage of docker-v1.10-migrator:
  -g string
    	Docker root dir (default "/var/lib/docker")
  -s string
    	Storage driver to migrate (default "auto")
```

Supported storage drivers are `aufs`, `overlay` and `devicemapper`. `auto` tries to automatically detect the driver from the root directory. `btrfs` and `zfs` are currently not supported.
