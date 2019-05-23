# README.md - ansible-role-prometheus

This playbook will install and set a host up with Prometheus monitoring system

Clone this repository into the ansible roles path to be included in playbooks.

Depends on:
 * geerlingguy.docker
```bash
ansible-galaxy install geerlingguy.docker
```

Runs Prometheus docker container behind NGINX reverse proxy on **port 8443** thorugh HTTPS. It uses [anisble-role-reverse-proxy](https://github.com/Psiphon-Infrastructure/ansible-role-reverse-proxy) to setup reverse proxy.
Check `./defaults/main.yaml` for configurable variables. 

When setting up new prometheus server make sure to add it to **prometheus-servers** group in hosts file. By default it adds **all** hosts in inventory to scraping job even if inventory host does not have node_exporter. 
If new host been added to the inventory after prometheus server configured then make sure to reapply *ansible-role-prometheus* to the prometheus server.
If old host been enabled with node_exporer then metrics should be scraped automaticaly. You can check */opt/prometheus-data/prometheus.yaml* for the list of scraped hosts. If host is not there then add to inventory and reapply this role.
