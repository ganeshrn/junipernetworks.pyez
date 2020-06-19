

# Juniper Networks PYEZ Collection

The Ansible Juniper Networks PYEZ collection includes a variety of Ansible content to help automate the management of Juniper Networks Junos network appliances.

This collection uses [junos-eznc](https://github.com/Juniper/py-junos-eznc) library as transport with Ansible pyez collection.

### Supported connections
The Juniper Networks Junos collection supports ``pyez``.

## Included content

Click the ``Content`` button to see the list of content included in this collection.

## Installing this collection

You can install the Juniper Networks Junos collection with the Ansible Galaxy CLI:

    ansible-galaxy collection install junipernetworks.pyez

You can also include it in a `requirements.yml` file and install it with `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: junipernetworks.pyez
    version: 0.0.1
```
## Using this collection

You can call modules by their Fully Qualified Collection Namespace (FQCN), such as `junipernetworks.pyez.jsnapy`.
The following example task take pre and post snapshot and check for conditions, using the FQCN:

```yaml
---
---
- hosts: junos
  gather_facts: no
  connection: junipernetworks.pyez.pyez
  vars:
    dir: "./"
  tasks:
  - name: JUNOS Post Checklist
    junipernetworks.pyez.jsnapy:
      test_files:
      - test_version.yml
      action: snapcheck
      dir: "{{ dir }}"
    register: test1


  - name: "Collect Pre Snapshot"
    junipernetworks.pyez.jsnapy:
      action: "snap_pre"
      test_files: "test_loopback.yml"
      dir: "{{ dir }}"

  - name: "Collect Post Snapshot"
    junipernetworks.pyez.jsnapy:
      action: "snap_post"
      test_files: "test_loopback.yml"
      dir: "{{ dir }}"

  - name: "Check after Pre and Post Snapshots"
    junipernetworks.pyez.jsnapy:
      action: "check"
      test_files: "test_loopback.yml"
      dir: "{{ dir }}"

```

The following example runs junos_rpc, using the FQCN:
```yaml
---
- hosts: junos
  gather_facts: no
  tasks:
  - name: Get Device Configuration for interface - 1
    junipernetworks.pyez.rpc:
      rpc: "get-config"
      filter_xml: "<configuration><interfaces/></configuration>"
      dest: "get_config_interfaces.conf"
    register: junos

  - name: Get Device Configuration for interface - 2
    junipernetworks.pyez.rpc:
      rpc: "get-config"
      filter_xml: "<configuration><interfaces/></configuration>"
      dest: "get_config_interfaces.conf"
    register: junos

  - name: Get Device Configuration for vlan - 1
    junipernetworks.pyez.rpc:
      rpc: "get-config"
      filter_xml: "<configuration><vlans/></configuration>"
      dest: "get_config_vlan.conf"
    register: junos

  - name: Get Device Configuration for vlan - 2
    junipernetworks.pyez.rpc:
      rpc: "get-config"
      filter_xml: "<configuration><vlans/></configuration>"
      dest: "get_config_vlan.conf"
    register: junos
```


### See Also:

* [Juniper Junos Platform options](https://docs.ansible.com/ansible/latest/network/user_guide/platform_junos.html).
* [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.

## Contributing to this collection

We welcome community contributions to this collection. If you find problems, please open an issue or create a PR against the [Juniper Networks Junos collection repository](https://github.com/ansible-collections/junipernetworks.junos).

You can also join us on:

- Freenode IRC - ``#ansible-network`` Freenode channel
- Slack - https://ansiblenetwork.slack.com

See the [Ansible Community Guide](https://docs.ansible.com/ansible/latest/community/index.html) for details on contributing to Ansible.


## Changelogs
<!--Add a link to a changelog.md file or an external docsite to cover this information. -->

## Roadmap

<!-- Optional. Include the roadmap for this collection, and the proposed release/versioning strategy so users can anticipate the upgrade/update cycle. -->

## More information

- [Ansible network resources](https://docs.ansible.com/ansible/latest/network/getting_started/network_resources.html)
- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/latest/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
