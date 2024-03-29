# cloudflared tunnel

This repo sets up cloudflared to run on the docker host's network and use remote management so you can use the Zero Trust dashboard.

## System Setup

```sh
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## Container Time

```sh
# Place the other files in this repo into `/opt/cloudflared-tunnel`
cd /opt/cloudflared-tunnel
# Create a .env file and replace the CHANGEME items. Your tunnel token will be in the Zero Trust dashboard.
sudo systemctl enable --now /opt/cloudflared-tunnel/cloudflared-tunnel.service
docker compose logs -f
# Your tunnel should be up and show as connected in the dashboard!
```
