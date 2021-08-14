# ros2-discovery-server-testing

## Example 2: starting `talker` and `listener` with a preconfigured peers list

change directory to `2_discovery_server_demo` and run:

### launching listener (dummy start)

```bash
docker-compose -f docker-compose.listener.yml up
```

The output should look like:

```bash
$ docker-compose -f docker-compose.listener.yml up
Creating network "2_decentralized_demo_default" with the default driver
Creating 2_decentralized_demo_husarnet-listener_1 ... done
Creating 2_decentralized_demo_listener_1          ... done
Attaching to 2_decentralized_demo_husarnet-listener_1, 2_decentralized_demo_listener_1
husarnet-listener_1  | Waiting for the husarnet daemon to start
husarnet-listener_1  | [5620907] joining...
husarnet-listener_1  | [5622911] joining...
husarnet-listener_1  | [5624912] joining...
husarnet-listener_1  | [5626913] joining...
husarnet-listener_1  | [5628913] joining...
husarnet-listener_1  | [5630915] joining...
husarnet-listener_1  | Husarnet IP address: fc94:3619:bc8a:fafa:bbec:f5fd:e803:9901
```

and stop the container [`ctrl` + `c`]

Now paste, the IPv6 address of the `listener` device to `fastdds_talker.xml`

### launching talker

```bash
docker-compose -f docker-compose.talker.yml up
```

You should get on the output the IPv6 address of `talker`:

```bash
$ docker-compose -f docker-compose.talker.yml up
Creating 2_decentralized_demo_husarnet-talker_1 ... done
Creating 2_decentralized_demo_talker_1          ... done
Attaching to 2_decentralized_demo_husarnet-talker_1, 2_decentralized_demo_talker_1
husarnet-talker_1  | Waiting for the husarnet daemon to start
husarnet-talker_1  | [5800920] joining...
...
talker_1           | [INFO] [1628951875.529229908] [talker]: Publishing: 'Hello World: 11'
talker_1           | [INFO] [1628951876.529064758] [talker]: Publishing: 'Hello World: 12'
husarnet-talker_1  | Husarnet IP address: fc94:85e2:ae61:39d7:a861:598d:166b:b7de
```

> Do not stop this container, keep in rolling.

Now copy `talker`'s IPv6 address to `fastdds_listener.xml`.

### launching listener (actual start)

Re-run:

```bash
docker-compose -f docker-compose.listener.yml up
```

And everything works fine:

```bash
$ docker-compose -f docker-compose.listener.yml up

...

husarnet-listener_1  | [5978807] joining...
husarnet-listener_1  | Husarnet IP address: fc94:3619:bc8a:fafa:bbec:f5fd:e803:9901
listener_1           | [INFO] [1628952045.530885270] [listener]: I heard: [Hello World: 181]
listener_1           | [INFO] [1628952046.530331247] [listener]: I heard: [Hello World: 182]
listener_1           | [INFO] [1628952047.530181604] [listener]: I heard: [Hello World: 183]
```

## Example 3: testing FastDDS Discovery Server

change directory to `3_discovery_server_demo` and run:

### launching discovery server

```bash
docker-compose -f docker-compose.discovery-server.yml up
```

The output will look like:

```bash
$ docker-compose -f docker-compose.discovery-server.yml up
Starting 3_discovery_server_demo_husarnet-discovery-server_1 ... done
Starting 3_discovery_server_demo_discovery-server_1          ... done
Attaching to 3_discovery_server_demo_husarnet-discovery-server_1, 3_discovery_server_demo_discovery-server_1
husarnet-discovery-server_1  | Waiting for the husarnet daemon to start
husarnet-discovery-server_1  | [6130668] joining...
husarnet-discovery-server_1  | [6132669] joining...
husarnet-discovery-server_1  | [6134670] joining...
husarnet-discovery-server_1  | [6136671] joining...
husarnet-discovery-server_1  | [6138672] joining...
husarnet-discovery-server_1  | [6140673] joining...
husarnet-discovery-server_1  | [6142674] joining...
husarnet-discovery-server_1  | Husarnet IP address: fc94:cecc:3189:ae23:cc06:7b07:50fe:e0e9
```

Shut down container ([`ctrl` + `c`]) and copy the given IPv6 address to `fastdds_client.xml` and `fastdds_server.xml` files.

Now restart `DDS discovery serve container`:

```bash
docker-compose -f docker-compose.discovery-server.yml up
```

### launching listener

```bash
docker-compose -f docker-compose.listener.yml up
```

### launching talker

```bash
docker-compose -f docker-compose.talker.yml up
```