# Docknode APT

## Metrics

- `https://mydomain.com:9100/metrics`
- `https://mydomain.com:9102/metrics`

## Install

0. VPS config (optional)

```bash
apt update
apt upgrade
apt install git
# Or all in one command
apt update && apt upgrade -y && apt install -y git

# install docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository and

```bash
git clone https://github.com/olivbau/docknode-apt.git
cd docknode-apt
```

2. Configure environement variables

```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

3. Setup UFW

```bash
ufw allow ssh
ufw deny 8080
ufw enable
```

4. Run

```bash
curl -o ./aptos/genesis.blob https://raw.githubusercontent.com/aptos-labs/aptos-networks/main/mainnet/genesis.blob
curl -o ./aptos/waypoint.txt https://raw.githubusercontent.com/aptos-labs/aptos-networks/main/mainnet/waypoint.txt

docker compose pull
docker compose up -d --abort-on-container-exit
docker logs -f docknode-apt-fullnode-1 --since 5m
docker compose down
```
