# Using Networks

## Network creation

With the release of Docker 1.9 you can now manage custom networks.


Here you can see how to create a network named `network1` using
the `bridge` driver

```python
docker_client.create_network("network1", driver="bridge")
```

You can also create more advanced networks with custom IPAM configurations.
For example, setting the subnet to `192.168.52.0/24` and gateway address
to `192.168.52.254`

```python

ipam_config = docker.utils.create_ipam_config(
    subnet='192.168.52.0/24',
    gateway='192.168.52.254'
)

docker_client.create_network("network1", driver="bridge", ipam=ipam_config)
```

With Docker 1.10 you can now also create internal networks

```python

docker_client.create_network("network1", driver="bridge", internal=True)
```

## Container network configuration

In order to specify which network(s) a container will be connected to and
additional configuration, use the `networking_config` parameter in
`Client.create_container`

```python
networking_config = docker_client.create_networking_config({
    'network1': docker_client.create_endpoint_config(
        ipv4_address: '172.28.0.124',
        aliases=['foo', 'bar'],
        links=['container2']
    )
})

ctnr = docker_client.create_container(
    img, command, networking_config=networking_config
)

```

## Network API documentation

### Client.create_networking_config

FIXME

### Client.create_endpoint_config

FIXME

### docker.utils.create_ipam_config

FIXME

### docker.utils.create_ipam_pool

FIXME