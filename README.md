# Deploying Virtual Machines on Hyper-V Using Vagrant with a Public Network

❗ Change variables in the `.env` to meet your requirements.

💡 Note that the `.env` file should be in the same directory as `Vagrantfile`.

To work with this project, you need to install the required Vagrant plugins

and generate SSH keys, or use the project's provided keys.

## Vagrant Plugin Installation

Install necessary Vagrant plugins

`vagrant plugin install vagrant-reload`

`vagrant plugin install dotenv`

Start Vagrant with the Hyper-V provider

`vagrant up --provider=hyperv`

Destroy the Vagrant environment

`vagrant destroy`


## Network Configuration

This configuration uses a public network. Ensure that you select an external/public switch in Hyper-V that provides access to the external network.

You need to set the switch name in the `HPV_PUBLIC_SWITCH` variable in the `.env` file, e.g.:
`HPV_PUBLIC_SWITCH=ExternalSwitch`

### DHCP vs. Static IP
In the `.env` file, specify whether to use DHCP for IP addresses or to configure static IPs:

* Set `DHCP=yes` to obtain IP addresses automatically via DHCP.

* Set `DHCP=no` (or comment this option) to configure static IP addresses based on the following parameters:

- `BASE_IP_ADDRESS=192.168.123`

- `VM_GATEWAY=192.168.123.254`

When `DHCP=no` (or commented out), the VMs will be provisioned with static IP addresses according to the `BASE_IP_ADDRESS` and `VM_GATEWAY` values specified in the `.env` file.


## SSH 

By default, the SSH key from the project's `ssh_keys` directory is distributed to the machines.
To connect, you need to copy the private key to your user's directory on the connecting machine or generate a new key following the instructions below.
Add the public key to the `ssh_keys` folder in the project and update the `SSH_KEY_PATH=./ssh_keys/id_rsa.pub` variable in the `.env` file.

### Generating an SSH Key

#### PowerShell

1. **Generate a new SSH key pair**

Replace "my_key" with your preferred key name.

`$sshKeyPath = "$env:USERPROFILE/.ssh/my_key"`

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f $sshKeyPath`

Set the path to the public key in the .env file


#### Bash

2. **Generate a new SSH key pair**

Replace "my_key" with your preferred key name.

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f "$HOME/.ssh/my_key"`

Set the path to the public key in the `.env` file


💡 This README.md file includes instructions for generating SSH keys and setting up Vagrant with the necessary plugins. Make sure to select the appropriate network settings in Hyper-V to match the public network configuration.