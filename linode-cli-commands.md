# Linode CLI Commands with Examples

This document provides a collection of common `linode-cli` commands with examples. Ensure `linode-cli` is installed (`pip install linode-cli`) and configured (`linode-cli configure`) before use.

## Linode Management

### List All Linodes

Display a list of all Linode instances.

```bash
linode-cli linodes list
```

### Create a Linode

Create a new Nanode instance in the us-east region.

```bash
linode-cli linodes create --label my-linode --region us-east --type g6-nanode-1 --image linode/ubuntu20.04 --root-pass securepassword123
```

### View Linode Details

View details of a specific Linode by its ID.

```bash
linode-cli linodes view 12345678
```

### Reboot a Linode

Reboot a Linode by its ID.

```bash
linode-cli linodes reboot 12345678
```

### Delete a Linode

Delete a Linode by its ID.

```bash
linode-cli linodes delete 12345678
```

## Region and Type Information

### List Available Regions

Display all available regions for Linode deployment.

```bash
linode-cli regions list
```

### List Linode Types

List all available Linode instance types.

```bash
linode-cli linodes types
```

## NodeBalancer Management

### Create a NodeBalancer

Create a NodeBalancer in the us-east region.

```bash
linode-cli nodebalancers create --label my-nodebalancer --region us-east
```

### List All NodeBalancers

Display a list of all NodeBalancers.

```bash
linode-cli nodebalancers list
```

## Domain Management

### Add a Domain

Create a new domain with master type.

```bash
linode-cli domains create --domain example.com --type master --soa_email admin@example.com
```

### List All Domains

Display all managed domains.

```bash
linode-cli domains list
```

## Volume Management

### Create a Volume

Create a 20GB volume in the us-east region.

```bash
linode-cli volumes create --label my-volume --size 20 --region us-east
```

### List All Volumes

Display all storage volumes.

```bash
linode-cli volumes list
```

## StackScript Management

### List All StackScripts

Display all available StackScripts.

```bash
linode-cli stackscripts list
```

### Create a Linode with a StackScript

Create a Linode using a specific StackScript.

```bash
linode-cli linodes create --label my-scripted-linode --region us-east --type g6-nanode-1 --stackscript_id 12345 --stackscript_data '{"key": "value"}' --root-pass securepassword123
```

## Account Management

### List Account Invoices

Display all account invoices.

```bash
linode-cli account invoices-list
```

### View Account Balance

Check the current account balance.

```bash
linode-cli account balance
```

## SSH Key Management

### List All SSH Keys

Display all SSH keys associated with the account.

```bash
linode-cli profile sshkeys-list
```

### Add an SSH Key

Upload a new SSH key from the local machine.

```bash
linode-cli profile sshkey-upload --label my-key --ssh_key "$(cat ~/.ssh/id_rsa.pub)"
```

## Firewall Management

### List All Firewalls

Display all configured firewalls.

```bash
linode-cli firewalls list
```

### Create a Firewall

Create a firewall allowing TCP traffic on port 80.

```bash
linode-cli firewalls create --label my-firewall --rules.inbound '[{"protocol": "TCP", "ports": "80", "action": "ACCEPT"}]'
```