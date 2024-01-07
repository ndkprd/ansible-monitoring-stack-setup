### Ansible Monitoring Stack Setup

Basically an Ansible Playbook that would setup a monitoring stack (Grafana, Prometheus, and its exporters) using Docker.

Using Docker Compose, it would install the following containers:
- [Grafana] as the monitoring front-end;
- [Prometheus] as the TSDB and datasource;
- [Blackbox Exporter] to export ICMP, HTTP, and DNS metrics of your targets;
- [SMMP Exporter] to export your network devices metrics;
- [Node Exporter] to export your server utility metrics;
- [Traefik] as a Reverse Proxy.

### What this playbook do?

- Do a basic setup of your server (update repo and packages, install needed softwares to your choosing);
- Setup a Prometheus target based on Jinja2 templates;
- Install docker;
- Move all the configuration file to target server;
- Run the docker compose.

### How to use?

Optional:
0.1. Setup a passwordless and sudoless user on your target machine;
0.2. Copy your controller machine public-key into your target machine.


1. Install [Ansible] on your controller machine;
2. Clone this repo;
3. `cd` into the repo directory;
4. Edit the  files inside the `vars` folder;
6. Run the playbook:
```
ansible-playbook -i hosts.yaml playbook.yaml
```

### How to access?

Grafana: grafana.{{ base-domain }} | {{ ip-server }}:3000
Prometheus: prometheus.{{ base-domain }} | {{ ip-server }}:9090
Dashboard Traefik: traefik.{{ base_domain }} | {{ ip-server }}:8080

### Roadmap and to-do

- [x] Able to do basic setup;
- [x] Able to install docker;
- [x] Able to install and run the docker compose;
- [x] Able to run Traefik container;
  - [ ] Able to setup HTTPS;
  - [ ] Able to setup Let's Encrypt;
- [x] Able to run Grafana container;
  - [x] Provision Datasources Prometheus;
  - [ ] Make custom Grafana dashboard;
    - [x] Web Host Dashboard (HTTP + DNS + Ping);
    - [ ] Web Endpoint Dashboard (HTTP);
    - [ ] Network Devices Dashboard (SNMP);
    - [ ] Server Dashboard (Node);
- [x]  Able to run Prometheus container;
  - [x] Make the target template using Jinja2;
    - [x] Templating target DNS;
    - [x] Templating target HTTP;
    - [x] Templating target perangkat jaringan;
- [ ] Divide playbook into `roles`;
- [ ] Add Loki logging;
- [ ] Able to configure Prometheus federation so it configure both main and satellite site at the same time.

## License

This project is licensed under [MIT license](https://mit-license.org/).
