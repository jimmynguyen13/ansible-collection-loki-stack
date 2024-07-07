# Ansible Collection - jimmynguyen13.loki_stack

# Ansible Collection - jimmynguyen13.loki_stack

### Version 1.0.0
This should be enough to set up centralized logging and monitoring fairly easily. Prometheus will be configured to monitor every host in the inventory (see roles/prometheus/templates/prometheus.yml.j2). Loki agents will point to the loki server(configured as `loki_server` variable). All of these services are installed as binaries with systemd.
### This collection has a role for each of the following:
- docker
- loki_stack
## Requirements
For the prometheus config to work correctly, the ansible inventory hostname of each server must be a DNS name that your prometheus server can resolve.
Current supported distributions are Debian 10/11 and Ubuntu 22/24. It may work on other distros, but it has not been tested.
## Example Playbook
```
- name: bootstrap monitoring server
  hosts: monitoring
  become: True
  vars:
    loki_server: loki_server.local
  roles:
    - jimmynguyen13.loki_stack.docker
    - jimmynguyen13.loki_stack.loki_stack
```

#### Promtail
Several variables can be used to customize the config file for promtail:
- `loki_server: loki` - change this to whatever host you want to use as the loki server
- `custom_server_config` - If defined this will replace the "server" section of the config with whatever is defined in the variable. 
- `custom_scrape_configs` - If defined this will replace the "scrape_configs" section of the config with whatever is defined in the variable. 
- `loki_server` - If defined this will replace the loki server's address (if using this, you must also define the port as shown below)
- `loki_port` - If defined this will replace the loki server's port (if using this, you must also define the address as shown above)
