#docker_selenium

## install boot2docker
```sh
$ brew update
$ brew install boot2docker
```

## install fig
```sh
$ brew install fig
```

## run boot2docker
```sh
$ boot2docker init
$ boot2docker start
$ boot2docker shellinit
$ eval "$(boot2docker shellinit)"
```

## use library
- [selenium/node-firefox](https://registry.hub.docker.com/u/selenium/node-firefox/)
- [selenium/hub](https://registry.hub.docker.com/u/selenium/hub/)

## run command
- make file for use fig  
(docker-compose.yml)

```yaml:docker-compose.yml
hub:
    image: selenium/hub
    ports:
        - "4444"

node:
    image: selenium/node-firefox
    expose:
        - "5555"
    links:
        - hub
```

- run

```sh
$ fig up -d hub
Creating dockerprac_hub_1...
```

- increse node

```sh
$ fig scale node=5
Creating dockerprac_node_2...
Creating dockerprac_node_3...
Creating dockerprac_node_4...
Creating dockerprac_node_5...
Starting dockerprac_node_1...
Starting dockerprac_node_2...
Starting dockerprac_node_3...
Starting dockerprac_node_4...
Starting dockerprac_node_5...
```

- process

```sh
$ docker ps
CONTAINER ID        IMAGE                          COMMAND                CREATED              STATUS              PORTS                     NAMES
f19e7ca0f770        selenium/node-firefox:latest   "/opt/bin/entry_poin   13 seconds ago       Up 2 seconds        5555/tcp                  dockerprac_node_5
59507edae8cd        selenium/node-firefox:latest   "/opt/bin/entry_poin   13 seconds ago       Up 3 seconds        5555/tcp                  dockerprac_node_4
1a5bf882c41b        selenium/node-firefox:latest   "/opt/bin/entry_poin   13 seconds ago       Up 3 seconds        5555/tcp                  dockerprac_node_3
d26172996780        selenium/node-firefox:latest   "/opt/bin/entry_poin   13 seconds ago       Up 4 seconds        5555/tcp                  dockerprac_node_2
0c6340ff464e        selenium/node-firefox:latest   "/opt/bin/entry_poin   13 seconds ago       Up 4 seconds        5555/tcp                  dockerprac_node_1
ac4aa13a5427        selenium/hub:latest            "/opt/bin/entry_poin   About a minute ago   Up About a minute   0.0.0.0:32769->4444/tcp   dockerprac_hub_1
```

## check browser
- ip address

```sh
$ boot2docker ip
192.168.59.103
```

- port

```sh
$ docker port dockerprac_hub_1
4444/tcp -> 0.0.0.0:32769
```

- access browser  
http://192.168.59.103:32769/grid/console

