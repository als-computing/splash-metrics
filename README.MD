# Description of splash-metrics
This repo contains the necessary docker-compose file, and configs for setting up prometheus, grafana and nginx. The only open port on this system is port 80 through which nginx acts as a proxy to grafana.
# Setup of splash-metrics
Create a `.env` file adjacent to `docker-compose.yml`. This is an example of the contents:
```
ADMIN_NAME=Sauron
ADMIN_PASSWORD=the_one_ring
```
This determines the default admin password and username for grafana.

In `prometheus.yml` you will need to configure the target for pulling metrics from:

```
     static_configs:
      - targets: ['{domain}:{port}'] 
```
Replace {domain} with the domain name of the service and {port} with the port the target service you want metrics for is running on.

Navigate to the grafana front page and log in. 

Starting from the sidebar navigate to "Configuration (gear icon) > Data Sources > Add data source" 

Select Prometheus and type in for the URL: `prometheus:9090` Then hit "Save & Test" button.

Now starting from the sidebar navigate to "Create (plus icon) > Import." From here copy and paste the contents of `grafana-dashboard.json` Then hit "Import."