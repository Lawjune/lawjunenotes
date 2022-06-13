https://blog.feabhas.com/2020/02/running-the-eclipse-mosquitto-mqtt-broker-in-a-docker-container/

# 1 - eclipse-mosquitto Docker image

```sh
docker pull eclipse-mosquitto
```

# 2 - Run the docker image

```sh
docker run -it --name mosquitto -p 1883:1883 eclipse-mosquitto 
`=>
1582194844: mosquitto version 1.6.8 starting
1582194844: Config loaded from /mosquitto/config/mosquitto.conf.
1582194844: Opening ipv4 listen socket on port 1883.
1582194844: Opening ipv6 listen socket on port 1883.
```

The -p 1883:1883 argument maps the docker container’s default MQTT socket 1883 the localhost (127.0.0.1) port 1883. Alternatively, we could map that onto another localhost port if it clashed with a locally running MQTT broker, e.g. -p 11883:1883.

Using the --name directive also allows the container to be stopped and restarted, using:
```sh
docker stop mosquitto
```

```sh
docker start mosquitto
```

# 3 - Setting up persistent files

Mosquitto can be configured, for example, to change logging, password, listener-ports, etc. This is achieved using mosquitto.conf file.

To set up mosquitto.conf, first create a local working directory with a three sub-directories of config, data and log, e.g.


```sh
cd
mkdir docker-mosquitto
cd docker-mosquitto
mkdir mosquitto 
mkdir mosquitto/config/ 
mkdir mosquitto/data/
mkdir mosquitto/log/
touch mosquitto/config/mosquitto.conf
vi mosquitto/config/mosquitto.conf
```

```mosquitto.conf
# following two lines required for > v2.0
allow_anonymous true
listener 1883
persistence true
persistence_location /mosquitto/data/
log_dest file /mosquitto/log/mosquitto.log
```

# 4 - Run the docker image with a mounted volume

Now, when invoking the docker image we use the -v flag mapping the local filesystem into the docker container. The running container will now pick up the locally defined mosquitto.conf. Invoke e.g:

```sh
docker run -it --name mosquitto -p 1883:1883 -v $(pwd)/mosquitto:/mosquitto/ eclipse-mosquitto 
```






















