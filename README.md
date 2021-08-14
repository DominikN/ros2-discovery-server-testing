# ros2-discovery-server-testing


## Example 3: testing FastDDS Discovery Server

change directory to `3_discovery_server_demo` and run:

### launching discovery server

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