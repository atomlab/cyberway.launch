<img width="400" src="./images/logo.jpg" />

# System requirements
- Debian 10
- Docker
- Docker-cmopose

# Prepare system
Ensure that Docker and Docker-compose installed

```
curl -fsSL https://get.docker.com -o get-docker.sh
sh ./get-docker.sh
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

# Mainnet

The current CyberWay version: [v2.1.1](https://github.com/cyberway/cyberway/releases/tag/v2.1.1)

# Running node

Clone this repository and run `sudo ./start_light.sh`

# Running full node

Clone this repository and run `sudo ./start_full_node.sh`

# Upgrade from v2.1.0 to v2.1.1

1. Download the docker image `cyberway/cyberway:v2.1.1`:
```
sudo docker pull cyberway/cyberway:v2.1.1
```

2. Download the last version of `docker-compose.yml` from the [GitHub](https://raw.githubusercontent.com/cyberway/cyberway.launch/master/docker-compose.yml)

```
sudo curl https://raw.githubusercontent.com/cyberway/cyberway.launch/master/docker-compose.yml --output /var/lib/cyberway/docker-compose.yml
```

3. Restart the nodeos container:
```
cd /var/lib/cyberway
sudo docker-compose up -t 120 -d
```


