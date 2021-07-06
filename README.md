# SLAX-Tools

Some routine helpers for JunOS

## Installation

1. Copy a file to your Juniper device and place it to `var/db/scripts/op/`
2. Enter the configuration mode and set:

```
user@router# set system scripts op file ccc-setup.slax
user@router# commit and-quit
```

3. Use a script (see example usages below) 

## ccc-setup
Creating l2circuit connections on a Juniper Router is a complex task:
- You have to enter configuration mode
- You have to configure sub-interface 
  - (encapsulation, description, vlan-id, family)
- You have to configure l2circuit neighbor section: 
  - (interface, virtual-circuit-id, description, mtu)

This script allows you to establish a vpls-ccc connections easy and fast with only one cli command!

### Usage
```
router> op ccc-setup ?
Possible completions:
  <[Enter]>            Execute this command
  <name>               Argument name
  description          Client name or description
  interface            Parent interface (ae0, xe-0/0/2, etc..)
  remote-address       Neighbor's loopback IP-address
  vlan-id              Vlan ID and Virtual Circuit ID

router> op ccc-setup interface ae0 vlan-id 100 remote-address 10.0.0.1 description "Office"
Confirm that you want to apply the configuration:
	Interface:   ae0.100
	Neighbor:    10.0.0.1
	Description: Office_ccc
Apply? (y/n) y
Applying the configuration...
Done

router>
```

## vlan-del

Deleting a vlan on a Juniper switch is fairly annoying: 
- You have to determine all interfaces with the vlan
- You have to delete the vlan from each of the interfaces
- You have to delete vlan itself
- Finally, you need to commit your configuration

`vlan-del` allows to make these steps at once!

### Usage

```
switch> op vlan-del ?                         
Possible completions:
  vlan-name            Vlan name

switch> op vlan-del vlan-name example    
Vlan example will be deleted from interfaces:
ge-0/0/30
Apply? (y/n) y
Applying the configuration...
Done

switch>
```
