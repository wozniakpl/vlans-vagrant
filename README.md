# VLAN Setup with Vagrant

This `Vagrantfile` provides a virtual environment to simulate a network setup with VLAN separation. VLANs, or Virtual Local Area Networks, are a means to partition a physical network into multiple, isolated logical networks. This setup helps in understanding and experimenting with VLAN configurations in a controlled environment.

## Overview

The provided Vagrant setup comprises:

1. **Router VM**: 
   - Acts as the main router for the VLANs.
   - Configures and manages the VLAN interfaces, ensuring traffic separation between VLANs.
   - IP: `192.168.56.1`.

2. **NGINX VM 1 (VLAN 10)**: 
   - Hosts an NGINX web server.
   - Resides within VLAN 10.
   - IP within VLAN 10: `192.168.10.2`.

3. **Client VM 1 (VLAN 10)**: 
   - A basic client machine set up within VLAN 10.
   - Can be used to test connectivity and access to resources within VLAN 10.
   - IP within VLAN 10: `192.168.10.3`.

4. **NGINX VM 2 (VLAN 20)**: 
   - Hosts an NGINX web server.
   - Resides within VLAN 20.
   - IP within VLAN 20: `192.168.20.2`.

5. **Client VM 2 (VLAN 20)**: 
   - A basic client machine set up within VLAN 20.
   - Can be used to test connectivity and access to resources within VLAN 20.
   - IP within VLAN 20: `192.168.20.3`.

## Getting Started

### Prerequisites

Ensure you have the following installed on your machine:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

### Usage

1. Clone this repository or copy the `Vagrantfile` to a directory on your machine.
2. Open a terminal and navigate to the directory containing the `Vagrantfile`.
3. Run the command `vagrant up`. This will start the provisioning of the VMs as defined in the Vagrantfile.
4. Once provisioning is complete, the VMs will be up and running. You can SSH into any VM using the command `vagrant ssh <vm_name>`. For example, to SSH into the router VM, use `vagrant ssh router`.

## Testing VLAN Separation

1. SSH into `client1` and try accessing the NGINX web page hosted by `nginx1` using `curl http://192.168.10.2`. You should be able to access it.
2. From the same client, attempt to access the NGINX page hosted by `nginx2` with `curl http://192.168.20.2`. This should fail due to VLAN separation.
3. Perform similar tests from `client2` to verify VLAN separation.

## Cleanup

To halt the VMs, use the command `vagrant halt`. If you wish to delete the VMs and clean up, use `vagrant destroy`.
