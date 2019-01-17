# Prometheus and Grafana - Example and My Personal Stack
I first search how works Prometheus and Grafana.

**Prometheus:** Collector of data(mainly in HTTP format).
**Grafana:** Expose that metrics in many ways(dashboard).
After do this i search for how to set up this in Docker
[Grafana](https://hub.docker.com/r/grafana/grafana/)
[Prometheus](https://hub.docker.com/r/prom/prometheus/)
Based on this i found some articles and tutorial:
https://medium.com/@salohyprivat/prometheus-and-grafana-d59f3b1ded8b
https://github.com/grafana/grafana/blob/master/conf/defaults.ini
https://github.com/prometheus/prometheus/blob/master/docs/getting_started.md
So i make my compose file with the necessary, and other things to run this Stack.

## For use this
1. Download Docker
2. Download WMI_Exporter Last Version https://github.com/martinlindhe/wmi_exporter/releases
3. Install in your machine
4. Run the command: docker-compose up -d
5. I STOP HERE------------------------------------------------------------------------------------

## For understand this
### Prometheus
I use sample configs of Prometheus and Grafana. This use WMI Exporter(BUT FELIPE, WHAT IS AN EXPORTER?)
Exporter is a tool(i dont know how to call this) that exposes the data about what you want. There are so many exporters. 
https://prometheus.io/docs/instrumenting/exporters/
I use this: https://github.com/martinlindhe/wmi_exporter, i install this in my host machine and a configure prometheus.yml with this:
``- job_name: 'win-exporter'``
    ``static_configs:``
      ``- targets: ['192.168.15.41:9182']``
This ip above it's my ip machine that I installed WMI_Exporter.
It is the  basic usage for prometheus and this Exporter.
### Grafana
In grafana is not to simple if you don't download any dashboard preconfigured. But i don't want to pass difficulty in a example. So i do this:
- Add the Data Source of Prometheus(Browser Mode), in that moment i have everything, but i need a dashboard dããr :/
- In this case, what i do? DOWNLOAD A EXAMPLE DASHBOARD THAT ALREADY HAVE MANY DASHBOARDS(yeeeeeeeep) https://grafana.com/dashboards/2129
- After this i just get in dashboard and i see this beatiful thing: https://prnt.sc/m79ow6, it is beatiful, isn't?
