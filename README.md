## Summary

This repository contains an example of ansible playbooks for automating Cisco Nexus Dashboard Orchestrator that were used during the **Automating Nexus Dashboard Orchestrator** webinar delivered in EMEAR.

## Inventory

The inventory includes not only NDO but also APICs on both sites, although those are not used in any of the playbooks provided in this repository.

## Demo Description

This demo consists on a master playbook called `deploy_config.yaml` where other playbooks are imported. There are 4 imported playbooks:

* Playbook `schema.yaml`, which creates a new tenant in NDO, together with one schema and 3 templates (Streched + Local templates). 
* Playbook `stretched.yaml`, which creates several objects inside the Stretched template (VRF, BDs, ANP, EPGs, ...), performs a deployment plan preview and saves it into a file, and finally deploys or undeploys the template based on the variable `deployment_state`
* Playbook `mdr-only.yaml`, which creates several objects inside the MDR1Only template (BDs, ANP, EPGs, ...), performs a deployment plan preview and saves it into a file, and finally deploys or undeploys the template based on the variable `deployment_state`
* Playbook `mlg-only.yaml`, which creates several objects inside the MLG1Only template (In this particular example, there are objects created), performs a deployment plan preview and saves it into a file, and finally deploys or undeploys the template based on the variable `deployment_state`

## Instructions

These playbooks has been tested with Ansible 2.9 and Cisco NDO collection 1.3.0.

Cisco ACI ansible collection can be installed using the following command:

```
$ ansible-galaxy collection install cisco.ndo
```

Cisco ACI ansible collection can be upgraded using either --force option or --upgrade option (available in 2.10+):

```
$ ansible-galaxy collection install cisco.ndo --upgrade
```

Before using these playbooks, ansible inventory needs to modified according to your environment.

To run the playbooks:

```
$ ansible-playbook -i inventory.yaml deploy_config.yaml
```

If ansible vault is being used for encrypting sensitive variables (such as in this example), then use the following command:

```
$ ansible-playbook --vault-pass-file vault.key -i inventory.yaml deploy_config.yaml
```

where `vault.key` contains the passphrase used to encrypt the inventory or sensitive variables.