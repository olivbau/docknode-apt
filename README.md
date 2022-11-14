# Docknode ETH

## Install 

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
ufw deny 9101 && ufw deny 6180
ufw enable
```

4. Run
```bash
docker compose up -d --pull always
docker logs -f fullnode --since 1m
```