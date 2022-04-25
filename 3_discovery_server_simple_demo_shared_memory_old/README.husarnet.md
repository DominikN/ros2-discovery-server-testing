## Get Husarnet Join Code

Login on your account at https://app.husarnet.com, select a network, click the **[Add element]** button and copy a Join Code. Create `.env` file and plase the Join Code within:

```
HUSARNET_JOINCODE=fc94:b01d:1803:8dd8:b293:5c7d:7639:932a/FjsgtDGqP7CQzM4mgnCPDn
```


## On computer running `talker`

1. Generate Husarnet ID:

```bash
docker run --rm -it husarnet/husarnet:latest husarnet genid > id
```

2. Get the IPv6 address from generated `id` file

```bash
sed -r 's/([a-f0-9:]*)\s.*/\1/g' id
```

and paste it in `dds-config.client.xml` and `dds-config.server.xml` here:

```xml
<RemoteServer prefix="44.49.53.43.53.45.52.56.45.52.5F.31">
    <metatrafficUnicastLocatorList>
        <locator>
            <udpv6>
                <address>fc94:36c5:08f7:aa49:ec95:4e17:00f3:0157</address>
                <port>11811</port>
            </udpv6>
        </locator>
    </metatrafficUnicastLocatorList>
</RemoteServer>
```

3. Run the `talker` node:

```bash
docker compose -f compose.talker.yaml up
```

## On computer running `listener`

1. Paste the same address in `dds-config.client.xml` and `dds-config.server.xml` files as above:

```xml
<RemoteServer prefix="44.49.53.43.53.45.52.56.45.52.5F.31">
    <metatrafficUnicastLocatorList>
        <locator>
            <udpv6>
                <address>fc94:36c5:08f7:aa49:ec95:4e17:00f3:0157</address>
                <port>11811</port>
            </udpv6>
        </locator>
    </metatrafficUnicastLocatorList>
</RemoteServer>
```

2. Run the `listener` node:

```bash
docker compose -f compose.listener.yaml up
```