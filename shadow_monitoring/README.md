# shadow_monitoring
Docker Monitoring Stack for Shadow Operators

### Docker install for 20.04 taken from DigitalOcean - https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04

**Step 1 — Installing Docker**

```

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Then install
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

Clone the shadow_monitoring repository:

```git clone https://github.com/DataKnox/Shadow-RPC-Operator.git```


Enter Shadow Monitoring Folder

```cd ~/Shadow-RPC-Operator/shadow_monitoring```

Create a docker storage for Grafana so that its persistent during reboots:

```docker volume create grafana-storage```

**OPTIONAL**

If you'd like to view prometheus, complete the following to protect it.

Perform:

```docker run --rm caddy caddy hash-password --plaintext 'ADMIN_PASSWORD'``` 

in order to generate a hash for your new password. ENSURE that you replace ADMIN_PASSWORD with new plain text password and ADMIN_PASSWORD_HASH with the hashed password references in docker-compose.yml for the caddy container.

You will need to uncomment the ```9090:9090``` in the caddy section of the docker-compose.yml

Run Docker Compose and turn up the monitoring

```docker compose up -d```

Connect to grafana by going to the IP of the server with port 3000:

```
Example:
http://1.2.3.4:3000
```
Login with default credentials

```admin/admin```

You will be asked to change the admin password.

You now have a full linux node dashboard for your server and should start to see your metrics populate the dashboard soon.  More dashboards from GG will be coming soon, so stay tuned!
