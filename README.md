# Arista AVD

This Repo contains Examples from Arista and my own configuration for network with 2 spines and 4 leaves, with each 2 leaf switches being in a group in which is MLAG configured.

My configs are based on Arista's Single DC L3LS topology and configs, however, they are modified in some ways and for example the L2LEAF switches are completly missing as they are not important in this scenario...

## Links which can come handy:

- [Arista AVD 5.4 guide](https://avd.arista.com/5.4/index.html)
- [Arista AVD 4.4 guide](https://avd.arista.com/4.4/index.html)

Those guide contains step-by-step instruction on how to install ansible and arista.avd collection

The reason why I included guides for 2 versions is that in 4.4, some things could be easier to read and understand

## Installation

**Requirments**
- Python 3.10+ installed
- pip installed
- ansible installed

<br>

```shell
pip install "pyavd[ansible]"
```

*If you are running AVD in virtualization, PIP could return* `error: externally-managed-environment`*. In this case use* `--break-system-packages` *to override the error*

```shell
ansible-galaxy collection install arista.avd
```

## After installation

After installation create a directory where you want to store your config files.
In my case I had a directory `~/lab/avd`.
In this directory create this folder structure.

```shell
---
lab
|-avd
 |-inventory
  |-documentation
  |-group_vars
  |-intended
  |-playbook(optional)
---
```

Move to the `~/lab/avd/inventory` and create there a config file `ansible.cfg` in which you will write those paramters

```shell
[defaults]
jinja2_extensions=jinja2.ext.loopcontrols,jinja2.ext.do
duplicate_dict_key=error
inventory=~/lab/avd/inventory/inventory.yml
```

Now, as it is useless to rewrite here the Arista documentation, I am going to refer you to the [Arista AVD 5.4 guide](https://avd.arista.com/5.4/index.html) and before you leave, it is important to stick to the order in which the commands and settings in the config are being run or else you might run into problems.

<br>

Now good luck!!!