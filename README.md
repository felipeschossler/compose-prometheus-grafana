# Prometheus and Grafana in Windows - Example and My Personal Stack

I first search how works Prometheus and Grafana.

- **Prometheus:** Collector of data(mainly in HTTP format).

- **Grafana:** Expose that metrics in many ways(dashboard).

After do this i search for how to set up this in Docker:

- [Grafana](https://hub.docker.com/r/grafana/grafana/)
- [Prometheus](https://hub.docker.com/r/prom/prometheus/)

Based on this i found some articles and tutorial:

[How to start up Stack](https://medium.com/@salohyprivat/prometheus-and-grafana-d59f3b1ded8b),
[Default File Grafana](https://github.com/grafana/grafana/blob/master/conf/defaults.ini),
[Default File Prometheus](https://github.com/prometheus/prometheus/blob/master/docs/getting_started.md)

So i make my compose file with the necessary, and other things to run this Stack.

## For use this

1. Download Docker and Install Docker
2. Download WMI_Exporter last version [WMI_Exporter Releases](https://github.com/martinlindhe/wmi_exporter/releases), and Install in your machine
3. Change the prometheus.yml file to your ip in targets of WMI exporter
4. Run the command: docker-compose up -d

## For understand this

### Prometheus

I use sample configs of Prometheus and Grafana. This use WMI Exporter(BUT FELIPE, WHAT IS AN EXPORTER?)
Exporter is a tool(i dont know how to call this) that exposes the data about what you want. There are so [many exporters](https://prometheus.io/docs/instrumenting/exporters/).

I use this: [WMI_Exporter](https://github.com/martinlindhe/wmi_exporter), and install this in my host machine and a configure prometheus.yml with this:

```yml
- job_name: 'win-exporter'
    static_configs:
      - targets: ['ip-that-you-want-metrics:9182']
```

It is the  basic usage for prometheus and this Exporter.

### Grafana

In grafana is not to simple if you don't download any dashboard preconfigured. But i don't want to pass difficulty in a example. So i do this:

- Add the Data Source of Prometheus(Browser Mode), in that moment i have everything, but i need a dashboard dããr :/

- In this case, what i do? DOWNLOAD A EXAMPLE DASHBOARD THAT ALREADY HAVE MANY DASHBOARDS (yeeeeeeeep) [Windows Exporter](https://grafana.com/dashboards/2129)

- After this i just get in dashboard and i see this beatiful thing: [Image of Dashboard](https://prnt.sc/m79ow6), it is beatiful, isn't?

---

## If you want more

### Node Exporter(Linux Metrics)

1. Download the package of Node Exporter: ``curl -LO https://github.com/prometheus/node_exporter/releases/download/v0.17.0/node_exporter-0.17.0.linux-amd64.tar.gz``
2. Unzip: ``tar xvfz node_exporter-0.17.0.linux-amd64.tar.gz``
3. Copy to /usr/local/bin: ``cp node_exporter-0.17.0.linux-amd64/node_exporter /usr/local/bin/``
4. Add user to node_exporter service: ``sudo useradd --no-create-home --shell /bin/false node_exporter``
5. Give permission in this directory to node_exporter user: ``sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter``
6. Create this file with the things below: ``sudo nano /etc/systemd/system/node_exporter.service``

```CONFIG
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

7. Start the service: ``systemctl start node_exporter``
8. Create a symlink: ``systemctl enable node_exporter``
9. Allow port 9100 on firewall: ``sudo ufw allow 9100/tcp``
10. Add the things below to this file ``prometheus.yml``

```YML
- job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['ip-that-you-want:9100']
```
