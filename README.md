
# 0. Docker setup
```
sudo snap install docker
sudo groupadd docker
sudo usermod -aG docker ubuntu
sudo reboot
```

# 1. init chaindata from genesis.json and create account

## edit genesis.json
## edit passwd
## build 

```
cd singlehost
docker build -f config/Dockerfile_init -t geth4init:1.0 config
docker run -d -v $PWD/volume:/tmp --name geth4init geth4init:1.0 --networkid <NETWORK_ID> --datadir=/root/.ethereum
docker exec -it geth4init /bin/bash

:/# geth account new
:/# rsync -av /root/.ethereum /tmp/
:/# exit

docker container stop geth4init
```

# 2. make .env

`singlehost/.env`
```
NETWORK_ID=
ACCOUNT_ADDR=
ENODE=
EXTIP=
```

# 3. compsose up
`docker compose up -d --build`

### ipc
`geth attach /root/.ethereum/geth.ipc`
```
admin.addPeer("enode://aaaaa....30303?discport=0")
admin.peers
net.peerCount
```

