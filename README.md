<img width="400" src="./images/logo.jpg" />

# Mainnet

The current CyberWay version: [v2.0.1](https://github.com/cyberway/cyberway/releases/tag/v2.0.1)

# Running node

Clone this repository and run `./start_light.sh`

# Upgrade from v2.0.0 to v2.0.1

1. Download the docker image `cyberway/cyberway:v2.0.1`:
```
sudo docker pull cyberway/cyberway:v2.0.1
```

2. In the file `/var/lib/cyberway/docker-compose.yml` update the version number of the `nodeos` container from `v2.0.0` to `v2.0.1`:
```
sudo sed -i 's|cyberway/cyberway:v2.0.0|cyberway/cyberway:v2.0.1|g' /var/lib/cyberway/docker-compose.yml
sudo sed -i 's|cyberway/cyberway:stable|cyberway/cyberway:v2.0.1|g' /var/lib/cyberway/docker-compose.yml
```

3. Stop and remove old version of `nodeosd`:
```
sudo docker stop nodeos
sudo docker rm nodeos
```

4. Run the new version of the `nodeos`:
```
cd /var/lib/cyberway
sudo docker-compose up -d
```

# Migration of the Golos blockchain

To start the transit you have to clone the contents of the repository and run `./start_check_state.sh`

## Preconditions

The shell script is configured to work with the following files:
- Path to the state and block-log: `/va/lib/golosd`
- Path to the configuration file: `/etc/golosd/config.ini`

If your configuration does not match this one, you should correct the variable values in the `transit.sh` file.

## Transit approval

The shell script `transit.sh` contains command `transit-approve`, which is called from the `start_check_state.sh`. To send operation `transit_to_cyberway` the script should sign it with the witness key taken from the file `/etc/golosd/config.ini`. The problem is that the signature of the witness key may not match the signature of the active account key. 

Please check this out. If so, then in this case you need to comment out the line containing `transit-approve` and send a transaction with the `transit_to_cyberway` operation manually. You can do it by using `cli_wallet`.
