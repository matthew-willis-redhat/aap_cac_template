# Ansible Automation Platform - Configuration as Code - Template

This is a combination of all the Red Hat CoP Config as Code collections to deploy and configure Ansible Automation Platform. This is built for multi environment (meaning multiple AAP instances/clusters), similary setup as the [Red Hat CoP - AAP Configuration Template](https://github.com/redhat-cop/aap_configuration_template.git). However, there are a few changes in this template that differs from the other template repository. 

- Using the `configs` directory, rather than just solely the `group_vars` directory
- The `group_vars` directory, resides under the `inventories` directory; This is similar to the previous template
- Inside each config directory, there's the ability to suffix an environment specific list, that can be used in their respective environments (Development, Test, Production)
- During the configuration process, each file will be read and the lists inside those files will be combined into a single list, for `infra.aap_configuration` roles to interpret

The main branch is built for Ansible Automation Platform 2.5+

You will need to replace the vault files with your own with these variables:

```yaml
---
console_token: 'this is the one from console.redhat.com'
redhat_api_token: 'this is the one linked below about api token'
rh_username: 'redhat user login (this is used to attach your subs to controller)'
rh_password: 'password for redhat account'
root_machine_pass: 'password for root user on builder (if not root user more changes will need to be made)'
hub_api_user_pass: 'this will create and use this password can be generated'
controller_api_user_pass: 'this will create and use this password can be generated'
aap_user: 'admin account used for gateway'
aap_pass: 'admin account pass for gateway, if none is given it will default to Password1234!'
# aap_token: 'admin account token used for authentication'
hub_pass: 'hub admin account pass, if none is given it will default to Password1234!'
# hub_token: 'hub token to pull collections, it is best to save in vault for more reliable usage vs generating on the fly'
vault_pass: 'the password to decrypt this vault'
...
```

**_NOTE:_** Do not forget to update your inventory files replacing the `HERE` lines, if you do not have a `builder` server you can use `hub` for this.

## Getting Help

Getting help with the Ansible Forums and Matrix, if you want to discuss something, ask for help, or participate in the community. Please use the #infra-config-as-code tag on the forum, or post to the chat in Matrix.

[Ansible Forums](https://forum.ansible.com/tag/infra-config-as-code)

[Matrix Chat Room](https://matrix.to/#/#aap_config_as_code:ansible.com)

## Documentation

[For documentation and examples, please visit us on Galaxy]([https://console.redhat.com/ui/repo/published/infra/aap_configuration/](https://console.redhat.com/ansible/automation-hub/repo/validated/infra/aap_configuration/docs/))

## Requirements

The supported collections that contains the modules are required for this collection to work, you can copy this requirements.yml file example.

```yaml
---
collections:
  - name: ansible.platform
  - name: ansible.hub
  - name: ansible.controller
  - name: ansible.eda
  - name: infra.aap_configuration
...
```


## Links to Ansible Automation Platform Collections

|                                      Collection Name                                |            Purpose            |
|:-----------------------------------------------------------------------------------:|:-----------------------------:|
| ansible.platform repo (no public repo for this collection)                          | gateway/platform modules      |
| [ansible.hub repo](https://github.com/ansible-collections/ansible_hub)              | Automation hub modules        |
| [ansible.controller repo](https://github.com/ansible/awx/tree/devel/awx_collection) | Automation controller modules |
| [ansible.eda repo](https://github.com/ansible/event-driven-ansible)                 | Event Driven Ansible modules  |

## Links to other Validated Configuration Collections for Ansible Automation Platform

|                                      Collection Name                                       |                      Purpose                      |
|:------------------------------------------------------------------------------------------:|:-------------------------------------------------:|
| [AAP Configuration Extended](https://github.com/redhat-cop/aap_configuration_extended)     | Where other useful roles that don't fit here live |
| [EE Utilities](https://github.com/redhat-cop/ee_utilities)                                 | Execution Environment creation utilities          |
| [AAP installation Utilities](https://github.com/redhat-cop/aap_utilities)                  | Ansible Automation Platform Utilities             |
| [AAP Configuration Template](https://github.com/redhat-cop/aap_configuration_template)     | Configuration Template for this suite             |

## AAP config

`ansible-playbook -i inventories/inventory_dev.yml playbooks/configure_aap.yml --ask-vault-pass`
