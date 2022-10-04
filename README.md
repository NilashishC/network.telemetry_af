# Ansible Collection - network.telemetry

An Ansible Collection to build, and maintain Telemetry stack using Telegraf, InfluxDB and Grafana for network appliances.

## Installation
```
pip install ansible-core
ansible-galaxy collection install git+https://github.com/NilashishC/network.telemetry.git
```

## Usage
```yaml
---
- hosts: collector
  gather_facts: yes
  tasks:
    - ansible.builtin.include_role:
        name: network.telemetry.setup_collector

```
```yaml
---
- hosts: network_appliances
  gather_facts: yes
  tasks:
    - ansible.builtin.include_role:
        name: network.telemetry.setup_telemetry

```

**Note:** This collection comes with setup data pre-loaded in vars/main.yaml for collector setup role. 
To override those, you can provide an YAML file with all the required variables and run your playbook
by passing `-e collector_setup_data=<path to setup data file>`.

### Example collector setup data file
```yaml
---
# vars file for setup_collector
package_path:
  destination: /home/ubuntu
  influxdb: https://dl.influxdata.com/influxdb/releases/influxdb2-2.4.0-amd64.deb
  influx_client: https://dl.influxdata.com/influxdb/releases/influxdb2-client-2.4.0-linux-amd64.tar.gz
  grafana: https://dl.grafana.com/enterprise/release/grafana-enterprise_9.1.6_amd64.deb

telegraf:
  config: files/telegraf/telegraf.conf.j2

influxdb:
  org: Ansible
  username: ansible
  password: ansible123
  token: MySecretToken
  bucket_name: nxos_dialout

influx_client:
  name: influxdb2-client-2.4.0-linux-amd64
  setup: "influx setup --org {{ influxdb.org }} --bucket {{ influxdb.bucket_name }} --username {{ influxdb.username }} --password {{ influxdb.password }} --token {{ influxdb.token }} --retention 2h --force"

grafana:
  org_name: Ansible
  org_role: Admin
  config: files/grafana/grafana.ini.j2
  datasources: files/grafana/datasources/datasources.yaml.j2
  dashboards:
    definitions: 
      - files/grafana/dashboards/dashboard_vxlan_dialout.json
    config: files/grafana/dashboards/dashboards.yaml

telemetry:
  transport: "grpc"
  service_address: ":57000"
```

### See Also:

* [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.