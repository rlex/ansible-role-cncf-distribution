WIP.
Ansible role for [cncf distibution](https://github.com/distribution/distribution), previously known as [docker registry](https://github.com/docker-archive/docker-registry).

Installs from binaries, runs with systemd, doesn't require docker to run.

### Usage

The main variable you need is cncf_distribution_config. Since registry is configured using yaml, you can just pass [any supported config](https://github.com/distribution/distribution/blob/main/docs/configuration.md) you need to it.

By default, it ships with sample config which mirrors docker.io registry and uses local storage, listening to port 5000 for registry itself, and 5001 for prometheus metrics:
```yaml
cncf_distribution_config:
  storage:
    filesystem:
      rootdirectory: /var/lib/registry
  http:
    addr: 0.0.0.0:5000
    secret: asecretforlocaldevelopment
    debug:
      addr: 0.0.0.0:5001
      prometheus:
        enabled: true
        path: /metrics
  proxy:
    remoteurl: https://registry-1.docker.io
```

Additionally, if you specify different directory, it will be automatically created on ansible run.
