# Docknode SEI

## Endpoints

- Fullnode: `https://mydomain.com`
- Node exporter: `https://mydomain.com:9100/metrics`

## Install

0. VPS config (optional)

```bash
# Install deps
apt update && apt upgrade -y && apt install -y git cmake gcc make jq snapd

# Install docker
# https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

# Install go
sudo snap install go --classic
```

1. Build image

```bash
git clone https://github.com/sei-protocol/sei-chain.git
cd sei-chain
git checkout v3.2.1
docker build --tag sei-chain/seid .
cd ..
```

2. Clone the repository and

```bash
git clone https://github.com/olivbau/docknode-sei.git
cd docknode-sei
```

3. Configure environement variables

```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

4. Setup UFW

```bash
ufw allow ssh
ufw deny 1317
ufw enable
```

5. Run

```bash
docker compose pull --ignore-pull-failures
docker compose up -d
docker logs -f docknode-sei-seid-1 --since 5m
docker compose down
```
