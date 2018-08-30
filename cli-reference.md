---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# IBM Cloud VPC Beta CLI Reference

This document provides a reference of the command line interface (CLI) commands available for the functionality of the {{site.data.keyword.cloud}} Virtual Private Cloud Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).

This document is organized into three sections:
* [Network CLI commands](#network)
* [Compute CLI commands](#compute)
* [Regions and Zones CLI commands](#geography)
* [VPN CLI commands](#VPN)
* [Load Balancers CLI commands](#Load-Balancers)

You can scroll through the Table of Contents menu at the right side of your screen to view the functional groupings of commands, such as those related to subnets, Floating IPs, and so forth.

## Pre-requisites:

1. Install the [IBM Cloud CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
2. Install or update the infrastructure-service plugin.

  ```
  ibmcloud plugin install infrastructure-service
  ```
  {: codeblock}

  To update:

  ```
  ibmcloud plugin update
  ```
  {: codeblock}

  To view installed plugins and versions:

  ```
  ibmcloud plugin list
  ```
  {: codeblock}

3. Log in to IBM Cloud. infrastructure-service plugin use the region that `ibmcloud login` target to determine what VPC endpoint will be used. For example, if you want to access VPC endpoint `us-south.iaas.cloud.ibm.com`, you have to use `ibmcloud login -a api.ng.bluemix.net` to target us-south region.

  If you have a federated account:
  ```
  ibmcloud login -a api.ng.bluemix.net -sso
  ```
  {: codeblock}

  otherwise
  ```
  ibmcloud login -a api.ng.bluemix.net
  ```
  {: codeblock}

<p style="font-size:24px">Network CLI Commands</p>
{: #network}

This section provides a reference for the command line interface (CLI) commands available for the network functionality.

## Floating IPs

### `ibmcloud is floating-ips`

List all floating IPs

**Syntax**

`ibmcloud is floating-ips [--zone ZONE] [--json]`

**Options**

- `--zone`: List floating IPs which belongs to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip`

View details of a floating IP

**Syntax**

`ibmcloud is floating-ip FLOATING_IP_ID [--json]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-reserve`

Reserve a floating IP in current resource group

**Syntax**

`ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE | --nic-id NIC_ID) [--json]`

**Options**

- `FLOATING_IP_NAME`: Name of the floating IP
- `--zone`: Name of the target zone. This is exclusive with `--nic`
- `--nic-id`: ID of the target network interface. This is exclusive with `--zone`
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-release`

Release a floating IP

**Syntax**

`ibmcloud is floating-ip-release FLOATING_IP_ID [-f, --force]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `	-f, --force`: Release without confirmation

---

### `ibmcloud is floating-ip-update`

Update a floating IP

**Syntax**

`ibmcloud is floating-ip-update  FLOATING_IP_ID [--name NEW_NAME] [--nic-id NIC_ID] [--json]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `--name`: New name of the floating IP
- `--nic-id`: ID of the new network interface to associate with
- `--json`: Format output in JSON

---


## Public Gateways

### `ibmcloud is public-gateways`

List all public gateways

**Syntax**

`ibmcloud is public-gateways [--vpc VPC_ID] [--zone ZONE]  [--json]`

**Options**

- `--vpc`: List public gateways which contain the specified VPC.  
- `--zone`: List public gateways which belong to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway`

View details of a public gateway

**Syntax**

`ibmcloud is public-gateway GATEWAY_ID [--json]`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway-create`

Create a new public gateway in current resource group

**Syntax**

`ibmcloud is public-gateway-create GATEWAY_NAME VPC_ID ZONE [--floating-ip-id IP_ID | --floating-ip-address IP_ADDERSS] [--json]`

**Options**

- `GATEWAY_NAME `: Name of the public-gateway
- `VPC_ID`: ID of the VPC
- `ZONE`: Name of the zone
- `--floating-ip`: ID of the floating IP bound to the public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway-update`

Update a public gateway

**Syntax**

`ibmcloud is public-gateway-update GATEWAY_ID --name NEW_NAME [--json]`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `--name`: New name of the public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway-delete`

Delete a public gateway

**Syntax**

`ibmcloud is image-delete GATEWAY_ID [-f, --force]`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `-f, --force`: Delete without confirmation

## Network ACLs

### `ibmcloud is network-acls`

List all network ACLs

**Syntax**

`ibmcloud is network-acls [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is network-acl`

View details of a network ACL

**Syntax**

`ibmcloud is network-acl ACL_ID [--json]`

**Options**

- `ACL_ID`: ID of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is network-acl-create`

Create a network ACL in current resource group

**Syntax**

`ibmcloud is network-acl-create ACL_NAME [--source-acl-id SOURCE_ACL_ID] [--json]`

**Options**

- `ACL_NAME`: Name of the network acl
- `--source-acl`: the ID the source network ACL to copy from
- `--json`: Format output in JSON

---

### `ibmcloud is network-acl-update`

Update a network ACL

**Syntax**

`ibmcloud is network-acl-update ACL_ID --name NEW_NAME [--json]`

**Options**

- `ACL_ID`: ID of the network ACL
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is network-acl-delete`

Delete a network ACL

**Syntax**

`ibmcloud is network-acl-delete ACL_ID [-f, --force]`

**Options**

- `ACL_ID`: ID of the network ACL
- `-f, --force`: Delete without confirmation


### `ibmcloud is network-acl-rules`

List all the rules of a network ACL

**Syntax**

`ibmcloud is network-acl-rules ACL_ID [--direction DIRECTION] [--json]`

**Options**

- `ACL_ID `: ID of the security group
- `--direction`: Filter with direction.`ingress` and `egress`
- `--json`: show output in JSON format

---

### `ibmcloud is network-acl-rule`

Retrieve the details of a network ACL rule

**Syntax**

`ibmcloud is network-acl-rule ACL_ID RULE_ID [--json]`

**Options**

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is network-acl-rule-add`

Add a rule to a network ACL

**Syntax**

`ibmcloud is network-acl-rule-add RULE_NAME ACL_ID ACTION DIRECTION PROTOCOL SOURCE DESTINATION  [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule-id RULE_ID] [--json]`

**Options**

- `RULE_NAME`: Name of the rule
- `ACL_ID`: ID of the security group
- `ACTION`: `allow` or `deny`
- `DIRECTION`: Direction of traffic to enforce. Valid values are `ingress` and `egress`
- `SOURCE`: source IP address or CIDR block
- `DESTINATION`: destination IP address or CIDR block
- `PROCOTOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port number. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--before-rule-id`: ID of the rule id that this rule is inserted before.

---

### `ibmcloud is network-acl-rule-update`

Update a rule of network ACL

**Syntax**

`ibmcloud is network-acl-rule-update ACL_ID RULE_ID [--action ACTION] [--direction DIRECTION] [--source SOURCE] [--dest DEST] [--protocol PROTOCOL] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule-id RULE_ID] [--json]`

**Options**

- `ACL_ID`: ID of the security group
- `RULE_ID`: ID of the rule
- `--action`: `allow` or `deny`
- `--direction`: Direction of traffic to enforce. Valid values are `ingress` and `egress`
- `--source`: source IP address or CIDR block
- `--dest`: destination IP address or CIDR block
- `--protocol`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port number. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--before-rule-id`: ID of the rule id that this rule is inserted before.

---

### `ibmcloud is network-acl-rule-delete`

Delete a rule from network ACL

**Syntax**

`ibmcloud is network-acl-rule ACL_ID RULE_ID [-f, --force]`

**Options**

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `-f, --force`: Force the operation without confirmation

---

## Subnets

### `ibmcloud is subnets`

List all subnets

**Syntax**

`ibmcloud is subnets [--zone ZONE] [--vpc VPC_ID] [--network-acl NETWORK_ACL_ID]  [--json]`

**Options**

- `--zone`: List public gateways which belongs to given zone
- `--vpc: List public gateways which contains the specified VPC.
- `--network-acl`: Filter with the network ACL with specified ID, this is exclusive with `--network-acl-name`
- `--json`: Format output in JSON

---

### `ibmcloud is subnet`

View details of a subnet

**Syntax**

`ibmcloud is subnet SUBNET_ID [--json]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-create`

Create a subnet in current resource group

**Syntax**

`ibmcloud is subnet-create SUBNET_NAME VPC_ID ZONE (--ipv4_cidr_block CIDR_BLOCK | --ipv4_address_count ADDR_COUNT) [--generation GEN] [--network-acl NETWORK_ACL_ID] [--public-gateway PUBLIC_GATEWAY_ID] [--json]`

**Options**

- `SUBNET_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `ZONE`: name of the zone
- `--ipv4_cidr_block`: the IPv4 range of the subnet, this is exclusive with  `--ipv4_address_count`
- `--ipv4_address_count`: the total number of IPv4 addresses required. This is exclusive with `--ipv4_cidr_block`
- `--generation`:  generation of the subnet. Valid values are `gt` and `gc`. Defauts to `gt`
- `--network-acl`: the ID of the network ACL for the subnet
- `--public-gateway`: the ID of the public-gateway for the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-update`

Update a subnet

**Syntax**

`ibmcloud is subnet-update SUBNET_ID --name NEW_NAME `

**Options**

- `SUBNET_ID `: ID of the subnet
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-delete`

Delete a subnet

**Syntax**

`ibmcloud is subnet-delete SUBNET_ID [-f, --force]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is subnet-pubic-gateway-detach`

Detach the public gateway from a subnet

**Syntax**

`ibmcloud is subnet-pubic-gateway-detach SUBNET_ID [-f, --force]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `-f, --force`: Delete without confirmation
---

### `ibmcloud is subnet-network-acl-detach`

Detach the network acl from a subnet

**Syntax**

`ibmcloud is subnet-network-acl-detach SUBNET_ID [-f, --force]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `-f, --force`: Delete without confirmation
---

## Security Groups

### `ibmcloud is security-groups`

List all security groups

**Syntax**

`ibmcloud is security-groups [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is security-group`

View details of a security group

**Syntax**

`ibmcloud is security-group GROUP_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-create`

Create a security group in current resource group

**Syntax**

`ibmcloud is security-group-create GROUP_NAME VPC_ID [--json]`

**Options**

- `GROUP_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-update`

Update a subnet

**Syntax**

`ibmcloud is security-group-update GROUP_ID --name NEW_NAME [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-delete`

Delete a security group

**Syntax**

`ibmcloud is security-group-delete GROUP_ID [-f, --force]`

**Options**

- `GROUP_ID `: ID of the security group
- `-f, --force`: Delete without confirmation

---


### `ibmcloud is security-group-network-interfaces`

List all network interfaces of a security group

**Syntax**

`ibmcloud is security-group-network-interfaces GROUP_ID [--json]`

**Options**

- `GROUP_ID`: ID of the security group
- `--json`: show output in JSON format

---


### `ibmcloud is security-group-network-interface`

Retrieve the details of a network interface of a security group

**Syntax**

`ibmcloud is security-group-network-interface GROUP_ID NIC_ID [--json]`

**Options**

- `GROUP_ID`: ID of the security group
- `NIC_ID`: ID of the network interface
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-network-interface-add`

Add a network interface to a security group

**Syntax**

`ibmcloud is security-group-network-interface-add GROUP_ID NIC_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-network-interface-remove`

Remove a network interface from a security group

**Syntax**

`ibmcloud is security-group-network-interface-remove GROUP_ID NIC_ID [-f, --force]`

**Options**

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is security-group-rules`

List all the rules of a security group

**Syntax**

`ibmcloud is security-group-rules GROUP_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-rule`

Retrieve the details of a security group rule

**Syntax**

`ibmcloud is security-group-rule GROUP_ID RULE_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-rule-add`

Add a rule to a security group. The IP version defaults to IPv4.

**Syntax**

`ibmcloud is security-group-rule-add GROUP_ID DIRECTION IP_VERSION PROTOCOL [--remote REMOTE_ADDRESS | CIDR_BLOCK | SECURITY_GROUP_ID] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `DIRECTION`: Direction of traffic to enforce. Valid values are `inbound` or `outbound`
- `PROTOCOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `IP_VERSION`: Version of the IP address. Valid values are `ipv4` and `ipv6` 
- `PROTOCOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--remote`: the set of network interfaces from which this rule allows traffic, Can be specified as either an REMOTE_ADDRESS, CIDR_BLOCK and SECURITY_GROUP_ID
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port number. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---

### `ibmcloud is security-group-rule-update`

Update a rule of a security group. The IP version defaults to IPv4.

**Syntax**

`ibmcloud is security-group-rule-update GROUP_ID RULE_ID GROUP_ID RULE_ID [--direction DIRECTION] [--ip-version IP_VERSION] [--protocol PROTOCOL] [--remote REMOTE_ADDRESS | CIDR_BLOCK | SECURITY_GROUP_ID] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

**Options**

- `GROUP_NAME`: Name of the security group
- `GROUP_ID`: ID of the security group
- `RULE_ID`: ID of the rule
- `--direction`: Direction of traffic to enforce. Valid values are `ingress` or `egress`
- `--ip-version`: Version of the IP address. Valid values are `ipv4` and `ipv6` 
- `--protocol`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--remote`: the set of network interfaces from which this rule allows traffic, Can be specified as either an REMOTE_ADDRESS, CIDR_BLOCK and SECURITY_GROUP_ID
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---

### `ibmcloud is security-group-rule-delete`

Delete a rule from a security group

**Syntax**

`ibmcloud is security-group-rule-delete GROUP_ID RULE_ID [-f, --force]`

**Options**

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `-f, --force`: Delete without confirmation

---

## VPCs

### `ibmcloud is vpcs`

List all vpcs

**Syntax**

`ibmcloud is vpcs [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is vpc`

View details of a VPC

**Syntax**

`ibmcloud is vpc VPC_ID [--json]`

**Options**

- `VPC_ID `: ID of the VPC
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-create`

Create a VPC in current resource group

**Syntax**

`ibmcloud is vpc-create VPC_NAME [--default] [--default-network-acl-id ACL_ID] [--json]`

**Options**

- `VPC_NAME `: Name of the VPC
- `--default`: set the VPC default of the account
- `--default-network-acl-id`: the ID of the default network ACL. This is exclusive with `--default-network-acl-name`
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-update`

Update a vpc

**Syntax**

`ibmcloud is vpc-update VPC_ID --name NEW_NAME [--json]`

**Options**

- `VPC_ID `: ID of the vpc
- `--name`: New name of the vpc
- `--json`: Format output in JSON
---

### `ibmcloud is vpc-delete`

Delete a vpc

**Syntax**

`ibmcloud is subnet-delete VPC_ID [-f, --force]`

**Options**

- `VPC_ID `: ID of the vpc
- `-f, --force`: Delete without confirmation

---
### `ibmcloud is vpc-default-security-group`

Retrieve the details of the default security group of a VPC

**Syntax**

`ibmcloud is vpc-default-security-group VPC_ID [--json]`

**Options**

- `VPC_NAME`: Name of the vpc
- `--json`: Format the output in JSON

---

<p style="font-size:24px">Compute CLI commands</p>
{: #compute}


This section contains a reference for the CLI commands related to Compute functionality in the IBM Cloud VPC Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).

## Profiles

### `ibmcloud is instance-profiles`

List all instance profiles available in the region.

**Syntax**

`ibmcloud is instance-profiles [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is instance-profile`

View details of an instance profile

**Syntax**

`ibmcloud is instance-profile PROFILE_NAME [--json]`

**Options**

- `PROFILE_NAME `: Name of the profile
- `--json`: Format output in JSON

---

## Images

### `ibmcloud is images`

List all images available in the region

**Syntax**

`ibmcloud is images [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is image`

Show details of an image

**Syntax**

`ibmcloud is image IMAGE_ID [--json]`

**Options**

- `IMAGE_ID `: ID of the image
- `--json`: Format output in JSON

---

## Keys

### `ibmcloud is keys`

List all keys

**Syntax**

`ibmcloud is keys [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is key`

Show details of a key

**Syntax**

`ibmcloud is key KEY_ID [--json ]`

**Options**

- `KEY_ID`: ID of the key
- `--json`: Format output in JSON

---

### `ibmcloud is key-create`

Imports an RSA public key

**Syntax**

`ibmcloud is key-create KEY_NAME (KEY | @KEY_FILE) [--json]`

**Options**

- `KEY_NAME`: Name of the key
- `KEY`: The public ssh key. If starts with "@", the rest should be a file name.
- `--json`: Format output in JSON

---

### `ibmcloud is key-update`

Update the name of a key

**Syntax**

`ibmcloud is key-update KEY_ID --name NEW_NAME [--json]`

**Options**

- `KEY_ID`: ID of the key
- `--name NEW_NAME`: New name for the key
- `--json`: Format output in JSON

---

### `ibmcloud is key-delete`

Delete a key

**Syntax**

`ibmcloud is key-delete  KEY_ID [-f, --force]`

**Options**

- `KEY_ID`: ID of the key
- `-f, --force`: Delete without confirmation

---

## Instances

### `ibmcloud is instances`

List all server instances

**Syntax**

`ibmcloud is instances [--zone ZONE] [--subnet-id SUBNET_ID ] [--vpc-id VPC_ID ] [--json]`

**Options**

- `--zone ZONE`: Zone name to which the server instance belongs.
- `--subnet-id SUBNET_ID`: ID of the subnet to which the server instance belongs.
- `--vpc-id VPC_ID`: ID of the VPC to which the server instance belongs.
- `--json`: Format output in JSON

---

### `ibmcloud is instance`

Show details of a server instance

**Syntax**

`ibmcloud is instance INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID`: ID of the server intance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-create`

Create a server instance

**Syntax**

`ibmcloud is instance-create INSTANCE_NAME VPC_ID ZONE_NAME PROFILE_NAME SUBNET_ID PORT_SPEED (--image-id IMAGE_ID | --boot-volume-id BOOT_VOLUME_ID) (--key-ids IDS) [--generation GENERATION] [--volume-ids IDS] [--user-data DATA] [--security-group-ids SECURITY_GROUP_IDS] [--json]`


**Options**

- `INSTANCE_NAME `: Name of the server instance
- `VPC_ID`: ID of the VPC.
- `ZONE_NAME`: Name of the zone
- `PROFILE_NAME`: Name of the profile.
- `SUBNET_ID`: The network interface associated subnet ID
- `PORT_SPEED`: The network interface port speed in Mbps
- `--image-id IMAGE_ID`: ID of the image. This is exclusive with `--boot-volume-id`
- `--boot-volume-id VOLUME_ID`: ID of the boot volume. This is exclusive with `--image-id`
- `--generation GENERATION`: Generation of the server instance. Valid values are `gc`, `gt`. Default to `gt`. (`gc` only for beta)
- `--volumes-ids VOLUME_ID1,VOLUME_ID2...`: IDs of the volumes to attach to the server
- `--volumes-names VOLUME_NAME1,VOLUME_2...`: Names of the volumes to attach to the server
- `--key-ids KEY_ID1,KEY_ID2...`: IDs of the key
- `--key-names KEY_NAME1,KEY_NAME2...`: Names of the key
- `--user-data DATA`: User data to transfer to the server
- `--json`: Format output in JSON

---

### `ibmcloud is instance-update`

Update a server instance

**Syntax**

`ibmcloud is instance-update INSTANCE_ID [--name NEW_NAME] [--profile PROFILE] [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--name NEW_NAME`: New name of the server instance
- `--profile PROFILE`: Name of the profile
- `--json`: Format output in JSON

---

### `ibmcloud is instance-delete`

Delete a server instance

**Syntax**

`ibmcloud is instance-delete INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-initialization-values`

View initialization details for an instance

**Syntax**

`ibmcloud is instance-initialization-values INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---
### `ibmcloud is instance-start`

Start a server instance

**Syntax**

`ibmcloud is instance-start INSTANCE_ID`

**Options**

- `INSTANCE_ID `: ID of the server instance

---

### `ibmcloud is instance-stop`

Stop a server instance

**Syntax**

`ibmcloud is instance-stop INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Stop without confirmation

---

### `ibmcloud is instance-reboot`

Reboot a server instance

**Syntax**

`ibmcloud is instance-reboot INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reboot without confirmation

---

### `ibmcloud is instance-reset`

Reset a server instance

**Syntax**

`ibmcloud is instance-reset INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reset without confirmation

---

### `ibmcloud is instance-actions`

Retrieves all pending, running, and recent actions on a server instance.

**Syntax**

`ibmcloud is instance-actions INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action`

Show details of an action on a server instance

**Syntax**

`ibmcloud is instance-action INSTANCE_ID  ACTION_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: ID of the action
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action-cancel`

Cancel a pending server instance action

**Syntax**

`ibmcloud is instance-action-cancel INSTANCE_ID ACTION_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: Action ID
- `-f, --force`: cancel without confirmation

---


### `ibmcloud is instance-network-interfaces`

List all network interfaces of a server instance

**Syntax**

`ibmcloud is instance-network-interfaces INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface`

Show details of a network interface of a server instance

**Syntax**

`ibmcloud is instance-network-interface INSTANCE_ID  NIC_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-create`

Create a network interface for a server instance

**Syntax**

`ibmcloud is instance-network-interface-create NIC_NAME INSTANCE_ID SUBNET_ID PORT_SPEED [--ipv4 IPV4_ADDRESS] [--ipv6 IPV6_ADDRESS] [--secondary-addresses ADDR1,ADDR2...] [--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...]`

**Options**

- `INSTANCE_ID`: ID of the server instance
- `PORT_SPEED`: Speed of the network interface in Mbps
- `--ipv4 IPV4_ADDRESS`: primary IPv4 address
- `--ipv6 IPV6_ADDRESS`: primary IPv6 address (not for beta?)
- `--secondary-addresses ADDR1,ADDR2...`: secondary IP addresses
- `--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...`: security group IDs

---

### `ibmcloud is instance-network-interface-update`

Update a network interface of a server instance

**Syntax**

`ibmcloud is instance-network-interface-update INSTANCE_ID NIC_ID [--name NEW_NAME] [--port-speed SPEED]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--name NEW_NAME`: New name of NIC
- `--port-speed SPEED`: New speed of the NIC

---

### `ibmcloud is instance-network-interface-delete`

Delete a network interface from a server

**Syntax**

`ibmcloud is instance-network-interface-delete INSTANCE_ID NIC_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-network-interface-floating-ips`

List all floating IPs associated with a network interface

**Syntax**

`ibmcloud is instance-network-interface-floating-ips INSTANCE_ID NIC_ID --json`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip`

Show details of a floating IP associated with a network interface

**Syntax**

`ibmcloud is instance-network-interface-floating-ip INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip-add`

Associate a floating IP to a network interface

**Syntax**
`ibmcloud is instance-nic-floating-ip-add INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON
---

### `ibmcloud is instance-network-interface-floating-ip-remove`

Disassociate a floating IP from a server

**Syntax**

`ibmcloud is instance-nic-floating-ip-remove INSTANCE_ID NIC_ID FLOATING_IP_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `-f, --force`: Remove without confirmation


<p style="font-size:24px">Regions and Zones</p>
{: #geography}

This section gives details about the CLI commands available for working with regions and zones.

## Regions

### `ibmcloud is regions`

List all regions

**Syntax**

`ibmcloud is regions [--json]`

**Options**

- `--json`: Format output in JSON

### `ibmcloud is region`

View details about a region

**Syntax**

`ibmcloud is region REGION_NAME [--json]`

**Options**

- `REGION_NAME`: Name of region
- `--json`: Format output in JSON

## Zones

### ibmcloud is zones

View all zones in a region

**Syntax**

`ibmcloud is zones REGION_NAME [--json]`

**Options**

- `REGION_NAME`: Name of region
- `--json`: Format output in JSON

### ibmcloud is zone

View details about a zone

**Syntax**

`ibmcloud is zone REGION_NAME ZONE_NAME [--json]`

**Options**

- `REGION_NAME`: Name of region
- `ZONE_NAME`: Name of zone
- `--json`: Format output in JSON

---

<p style="font-size:24px">VPN</p>
{: #VPN}

This section gives details about the CLI commands available for working with VPN.

## IKE Policies

### `ibmcloud is ike-policies`

List all IKE policies 

**Syntax**

`ibmcloud is ike-policies [--json]`

**Options**

- `--json`: Format output in JSON

---
### `ibmcloud is ike-policy`

View details of an IKE policy

**Syntax**

`ibmcloud is ike-policy IKE_POLICY_ID [--json]`

**Options**
- `IKE_POLICY_ID`: ID of the IKE policy
- `--json`: Format output in JSON

---
### `ibmcloud is ike-policy-create`

Create an IKE policy in current resource group

**Syntax**

`ibmcloud is ike-policy-create IKE_POLICY_NAME AUTHENTICATION_ALGORITHM DH_GROUP ENCRYPTION_ALGORITHM IKE_VERSION [--key-lifetime KEY_LIFETIME] [--json]`

**Options**
- `IKE_POLICY_NAME`: Name of the IKE policy
- `AUTHENTICATION_ALGORITHM`: The authentication algorithm. Enumeration type: md5, sha1, sha256
- `DH_GROUP`: The Diffie-Hellman group. Enumeration type: 2, 5, 14
- `ENCRYPTION_ALGORITHM`: The encryption algorithm. Enumeration type: 3des, aes128, aes256
- `IKE_VERSION`: The IKE protocol version. Enumeration type: 1, 2
- `--key-lifetime`: The key lifetime in seconds. Maximum: 86400, Minimum: 300
- `--json`: Format output in JSON

---
### `ibmcloud is ike-policy-delete`

Delete an IKE policy

**Syntax**

`ibmcloud is ike-policy-delete IKE_POLICY_ID [-f, --force]`

**Options**

- `IKE_POLICY_ID`: ID of the IKE policy
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is ike-policy-update`

Update an IKE policy

**Syntax**

`ibmcloud is ike-policy-update IKE_POLICY_ID [--authentication_algorithm md5 | sha1 | sha256] [--dh-group 2 | 5 | 14] [--encryption-algorithm 3des | aes128 | aes256] [--ike-version 1 | 2] [--key-lifetime KEY_LIFETIME] [--name NEW_NAME] [--json]`

**Options**
- `IKE_POLICY_ID`: Name of the ID policy
- `--authentication_algorithm`: The authentication algorithm. Enumeration type: md5, sha1, sha256
- `--dh-group`: The Diffie-Hellman group. Enumeration type: 2, 5, 14
- `--encryption-algorithm`: The encryption algorithm. Enumeration type: 3des, aes128, aes256
- `--ike-version`: The IKE protocol version. Enumeration type: 1, 2
- `--key-lifetime`: The key lifetime in seconds. Maximum: 86400, Minimum: 300
- `--name`: New name of the IKE policy
- `--json`: Format output in JSON

---
### `ibmcloud is ike-policy-connections`

List all connections that use the IKE policy

**Syntax**

`ibmcloud is ike-policy-connections IKE_POLICY_ID [--json]`

**Options**
- `IKE_POLICY_ID`: ID of the IKE policy
- `--json`: Format output in JSON

---
## IPsec Policies

### `ibmcloud is ipsec-policies`

List all IPsec policies 

**Syntax**

`ibmcloud is ipsec-policies [--json]`

**Options**

- `--json`: Format output in JSON

---
### `ibmcloud is ipsec-policy`

View details of an IPsec policy

**Syntax**

`ibmcloud is ipsec-policy IPSEC_POLICY_ID [--json]`

**Options**
- `IPSEC_POLICY_ID`: ID of the IPsec policy
- `--json`: Format output in JSON

---
### `ibmcloud is ipsec-policy-create`

Create an IPsec policy in current resource group

**Syntax**
 
`ibmcloud is ipsec-policy-create IPSEC_POLICY_NAME AUTHENTICATION_ALGORITHM ENCRYPTION_ALGORITHM PFS [--key-lifetime KEY_LIFETIME] [--json]`

**Options**
- `IPSEC_POLICY_NAME`: Name of the IPsec policy
- `AUTHENTICATION_ALGORITHM`: The authentication algorithm. Enumeration type: md5, sha1, sha256
- `ENCRYPTION_ALGORITHM`: The encryption algorithm. Enumeration type: 3des, aes128, aes256
- `PFS`: Perfect Forward Secrecy. Enumeration type: disabled, group_2, group_5, group_14
- `--key-lifetime`: The key lifetime in seconds. Maximum: 86400, Minimum: 300
- `--json`: Format output in JSON

---
### `ibmcloud is ipsec-policy-delete`

Delete an IPsec policy

**Syntax**

`ibmcloud is ipsec-policy-delete IPSEC_POLICY_ID [-f, --force]`

**Options**

- `IPSEC_POLICY_NAME`: Name of the IPsec policy
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is ipsec-policy-update`

Update an IPsec policy

**Syntax**

`ibmcloud is ipsec-policy-update IPSEC_POLICY_ID [--authentication_algorithm md5 | sha1 | sha256] [--encryption-algorithm 3des | aes128 | aes256] [--key-lifetime KEY_LIFETIME] [--pfs disabled | group_2 | group_5 | group_14] [--name NEW_NAME] [--json]`

**Options**
- `IPSEC_POLICY_ID`: ID of the IPsec policy
- `--authentication_algorithm`: The authentication algorithm. Enumeration type: md5, sha1, sha256
- `--encryption-algorithm`: The encryption algorithm. Enumeration type: 3des, aes128, aes256
- `--key-lifetime`: The key lifetime in seconds. Maximum: 86400, Minimum: 300
- `--pfs`: Perfect Forward Secrecy. Enumeration type: disabled, group_2, group_5, group_14
- `--name`: New name of the IPsec policy
- `--json`: Format output in JSON

---
### `ibmcloud is ipsec-policy-connections`

List all connections that use the IPsec policy

**Syntax**

`ibmcloud is ipsec-policy-connections IPSEC_POLICY_ID [--json]`

**Options**
- `IPSEC_POLICY_NAME`: Name of the IPsec policy
- `--json`: Format output in JSON

---


## VPN Gateway

### `ibmcloud is vpn-gateways`

List all vpn gateways 

**Syntax**

`ibmcloud is vpn-gateways [--json]`

**Options**

- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway`

View details of an VPN gateway

**Syntax**

`ibmcloud is vpn-gateway VPN_GATEWAY_ID [--json]`

**Options**
- `VPN_GATEWAY_ID`: ID of the VPN gateway
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-create`

Create an VPN gateway in current resource group

**Syntax**

`ibmcloud is vpn-gateway-create VPN_GATEWAY_NAME SUBNET_ID [--json]`

**Options**
- `VPN_GATEWAY_NAME`: Name of the VPN gateway
- `SUBNET_ID`: The unique identifier for this subnet
- `--json`: Format output in JSON

--subnet were mandatory?

---
### `ibmcloud is vpn-gateway-delete`

Delete an VPN gateway

**Syntax**

`ibmcloud is vpn-gateway-delete VPN_GATEWAY_ID [-f, --force]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is vpn-gateway-update`

Update an VPN gateway

**Syntax**

`ibmcloud is vpn-gateway-update VPN_GATEWAY_ID [--name NEW_NAME] [--json]`

**Options**
- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `--name`: New name of the VPN gateway policy
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-connections`

List all connections of the VPN gateway

**Syntax**

`ibmcloud is vpn-gateway-connections VPN_GATEWAY_ID [--status STATUS] [--json]`

**Options**
- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `--status`: Filters the collection to VPN connections with the specified status
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-connection-create`

Create a connection of the vpn gateway in current resource group.

**Syntax**

`ibmcloud is vpn-gateway-connection-create CONNECTION_NAME VPN_GATEWAY_ID PEER_ADDRESS PRESHARED_KEY [--statue-up true | false] [--dead-peer-detection-action ACTION] [--dead-peer-detection-interval INTERVAL] [--dead-peer-detection-timeout TIMEOUT] [--ike-policy IKE_POLICY_ID] [--ipsec-policy IPSEC_POLICY_ID]  [--local-cidrs CIDR1, --local-cidrs CIDR2 ...] [--peer-cidrs CIDR1, --peer-cidrs CIDR2 ...] [--json]`

**Options**
- `CONNECTION_NAME`: Name of the connection
- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `PEER_ADDRESS`: The IP address of the peer VPN gateway
- `PRESHARED_KEY`: The preshared key
- `--statue-up`: If set to false, the VPN connection is shut down. default is false
- `--dead-peer-detection-action`: Dead Peer Detection actions. Enumeration type: restart, clear, hold, none
- `--dead-peer-detection-interval`: Dead Peer Detection interval in seconds
- `--dead-peer-detection-timeout`: Dead Peer Detection timeout in seconds
- `--ike-policy`: ID of the IKE policy
- `--ipsec-policy`: ID of the IPsec policy
- `--local-cidrs`: List of CIDRs for this resource
- `--peer-cidrs`: List of CIDRs for this resource
- `--json`: Format output in JSON
  
---
### `ibmcloud is vpn-gateway-connection`

Retrieve details of a vpn gateway connection

**Syntax**

`ibmcloud is vpn-gateway-connection VPN_GATEWAY_ID CONNECTION_ID [--json]`

**Options**
- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-connection-delete`

Delete a vpn gateway connection

**Syntax**

`ibmcloud is vpn-gateway-connection-delete VPN_GATEWAY_ID CONNECTION_ID [-f, --force]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is vpn-gateway-connection-update`

Update a vpn gateway connection

**Syntax**

`ibmcloud is vpn-gateway-connection-update VPN_GATEWAY_ID CONNECTION_ID [--statue-up true | false] [--dead-peer-detection-action ACTION] [--dead-peer-detection-interval INTERVAL] [--dead-peer-detection-timeout TIMEOUT] [--ike-policy IKE_POLICY_ID] [--ipsec-policy IPSEC_POLICY_ID] [--peer-address ADDRESS] [--psk PSK] [--name NEW_NAME] [--json]`

**Options**
- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `--statue-up`: If set to false, the VPN connection is shut down. default is false
- `--dead-peer-detection-action`: Dead Peer Detection actions. Enumeration type: restart, clear, hold, none
- `--dead-peer-detection-interval`: Dead Peer Detection interval in seconds
- `--dead-peer-detection-timeout`: Dead Peer Detection timeout in seconds
- `--ike-policy`: ID of the IKE policy
- `--ipsec-policy`: ID of the IPsec policy
- `--peer-address`: The IP address of the peer VPN gateway
- `--psk`: The preshared key
- `--name`: New name of the connection
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-connection-local-cidr-delete`

Remove a local CIDRs from the vpn gateway connection

**Syntax**

`ibmcloud is vpn-gateway-connection-local-cidr-delete VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [-f, --force]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `PREFIX_ADDRESS`: The prefix address part of the CIDR
- `PREFIX_LENGTH`: The prefix length part of the CIDR
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is vpn-gateway-connection-local-cidr-add`

Add a local CIDRs to a connection

**Syntax**

`ibmcloud is vpn-gateway-connection-local-cidr-add VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [--json]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `PREFIX_ADDRESS`: The prefix address part of the CIDR
- `PREFIX_LENGTH`: The prefix length part of the CIDR
- `--json`: Format output in JSON

---
### `ibmcloud is vpn-gateway-connection-peer-cidr-delete`

Remove a peer CIDRs from the vpn gateway connection

**Syntax**

`ibmcloud is vpn-gateway-connection-peer-cidr-delete VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [-f, --force]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `PREFIX_ADDRESS`: The prefix address part of the CIDR
- `PREFIX_LENGTH`: The prefix length part of the CIDR
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is vpn-gateway-connection-peer-cidr-add`

Add a peer CIDRs to a connection

**Syntax**

`ibmcloud is vpn-gateway-connection-peer-cidr-add VPN_GATEWAY_ID CONNECTION_ID PREFIX_ADDRESS PREFIX_LENGTH [--json]`

**Options**

- `VPN_GATEWAY_ID`: ID of the VPN gateway name
- `CONNECTION_ID`: ID of the connection
- `PREFIX_ADDRESS`: The prefix address part of the CIDR
- `PREFIX_LENGTH`: The prefix length part of the CIDR
- `--json`: Format output in JSON
---

<p style="font-size:24px">Load Balancers</p>
{: #Load-Balancers}

This section gives details about the CLI commands available for working with Load Balancers.

## Load Balancer

### `ibmcloud is load-balancers`

List all load balancers

**Syntax**

`ibmcloud is load-balancers [--json]`

**Options**

- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer`

View details of a load balancer

**Syntax**

`ibmcloud is load-balancer LOAD_BALANCER_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-create`

Create a load balancer in current resource group.

**Syntax**

`ibmcloud is load-balancer-create LOAD_BALANCER_NAME LOAD_BALANCER_TYPE (--subnets SUBNET_ID1, --subnets SUBNET_ID2 ...) [--json]`

**Options**

- `LOAD_BALANCER_NAME`: Name of the load balancer
- `LOAD_BALANCER_TYPE`:public or private
- `--subnets`: The subnets to provision this load balancer
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-delete`

Delete a load balancer

**Syntax**

`ibmcloud is load-balancer-delete LOAD_BALANCER_ID [-f, --force]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `-f, --force`: Delete without confirmation

---
### `ibmcloud is load-balancer-update`

Update a load balancer

**Syntax**

`ibmcloud is load-balancer-update LOAD_BALANCER_ID [--name NEW_NAME] [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `--name`: New name of the load balancer
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-listeners`

List all the listeners of a load balancer

**Syntax**

`ibmcloud is load-balancer-listeners LOAD_BALANCER_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-listener`

View details of a load balancer listener

**Syntax**

`ibmcloud is load-balancer-listener LOAD_BALANCER_ID LISTENER_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `LISTENER_ID `: ID of the listenser
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-listener-create`

Create a listener for a load balancer

**Syntax**

`ibmcloud is load-balancer-listener-create LOAD_BALANCER_ID PORT PROTOCOL [--certificate-instance CERTIFICATE_INSTANCE_CRN] [--connection-limit LIMIT] [--default-pool DEFAULT_POOL_ID] [--json]`

**Options**
- `LOAD_BALANCER_NAME`: Name of the load balancer
- `LOAD_BALANCER_ID `: ID of the load balancer
- `PORT`: The listener port number
- `PROTOCOL`: The listener protocol. Enumeration type: http, https, tcp
- `--certificate-instance-crn`: CRN of the certificate instance 
- `--connection-limit`: The connection limit of the listener
- `--default-pool`: ID of the default pool
- `--json`: Format output in JSON
  
---
### `ibmcloud is load-balancer-listener-delete`

Delete a listener from a load balancer

**Syntax**

`ibmcloud is load-balancer-listener-delete LOAD_BALANCER_ID LISTENER_ID [-f, --force]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `LISTENER_ID `: ID of the listenser
- `-f, --force`: Force delete without confirmation
  
---
### `ibmcloud is load-balancer-listener-update`

Update a listener of a load balancer

**Syntax**

`ibmcloud is load-balancer-listener-update LOAD_BALANCER_ID LISTENER_ID [--certificate-instance CERTIFICATE_INSTANCE_ID] [--connection-limit LIMIT] [--port PORT] [--protocol http | https | tcp] [--default-pool DEFAULT_POOL_ID] [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `LISTENER_ID `: ID of the listenser
- `--certificate-instance`: ID of the certificate instance 
- `--connection-limit`: The connection limit of the listener
- `--port`: The listener port number
- `--protocol`: The listener protocol. Enumeration type: http, https, tcp
- `--default-pool`: ID of the default pool
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pools`

List all pools of a load balancer

**Syntax**

`ibmcloud is load-balancer-pools LOAD_BALANCER_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool`

View details of load balancer pool

**Syntax**

`ibmcloud is load-balancer-pool LOAD_BALANCER_ID POOL_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `--json`: Format output in JSON
  
---
### `ibmcloud is load-balancer-pool-create`

Create a pool for a load balancer

**Syntax**

`ibmcloud is load-balancer-pool-create POOL_NAME LOAD_BALANCER_ID ALGORITHM PROTOCOL HEALTH_DELAY HEALTH_RETRIES HEALTH_TIMEOUT HEALTH_TYPE [--health-monitor-url URL][--session-persistence-type TYPE] [--session-persistence-cookie-name NAME] [--json]`

**Options**
- `POOL_NAME`: Name of the pool
- `LOAD_BALANCER_ID `: ID of the load balancer
- `ALGORITHM`: The load balancing algorithm. Enumeration type: round_robin, weighted_round_robin, least_connections
- `PROTOCOL`: The pool protocol. Enumeration type: http, tcp
- `HEALTH_DELAY`: The health check interval in seconds. Interval must be greater than timeout value
- `HEALTH_RETRIES`: The health check max retries
- `HEALTH_TIMEOUT`: The health check timeout in seconds
- `HEALTH_TYPE`: The pool protocol. Enumeration type: http, tcp
- `--health-monitor-url`: The health check url. This is applicable only to http type of HEALTH_TYPE
- `--session-persistence-type`: The session persistence type, Enumeration type: source_ip, http_cookie, app_cookie
- `--session-persistence-cookie-name`: Session persistence cookie name. This is applicable only to `--session-persistence-type` app_cookie.
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool-delete`

Delete a pool from a load balancer

**Syntax**

`ibmcloud is load-balancer-pool-delete LOAD_BALANCER_ID POOL_ID [-f, --force]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `-f, --force`: Force delete without confirmation

---
### `ibmcloud is load-balancer-pool-update`

Update a pool of a load balancer

**Syntax**

`ibmcloud is load-balancer-pool-update LOAD_BALANCER_ID POOL_ID [--algorithm round_robin | weighted_round_robin | least_connections] [--health-delay DELAY] [--health-max-retries RETRIES] [--health-timeout TIMEOUT] [--health-type TYPE] [--health-monitor-url URL] [--protocol http | tcp] [--session-persistence-type TYPE] [--session-persistence-cookie-name NAME] [--name NEW_NAME] [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `--algorithm`: The load balancing algorithm. Enumeration type: round_robin, weighted_round_robin, least_connections
- `--health-delay`: The health check interval in seconds. Interval must be greater than timeout value
- `--health-max-retries`: The health check max retries
- `--health-timeout`: The health check timeout in seconds
- `--health-type`: The pool protocol. Enumeration type: http, tcp
- `--health-monitor-url`: The health check url. This is applicable only to http type of --health-type
- `--protocol`: The pool protocol. Enumeration type: http, tcp
- `--session-persistence-type`: The session persistence type
- `--session-persistence-cookie-name`: The health check url. This is applicable only to http type of HEALTH_TYPE
- `--name`: New name of the pool
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool-members`

List all the members of a load balancer pool

**Syntax**

`ibmcloud is load-balancer-pool-members LOAD_BALANCER_ID POOL_ID [--json]`

**Options**

- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool-member`

View details of pool member 

**Syntax**

`ibmcloud is load-balancer-pool-member LOAD_BALANCER_ID POOL_ID MEMBER_ID [--json]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `MEMBER_ID `: ID of the member
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool-member-create`

Create a member of a load balancer pool

**Syntax**

`ibmcloud is load-balancer-pool-member-create LOAD_BALANCER_ID POOL_ID PORT TARGET_ADDRESS [--weight WEIGHT] [--json]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `PORT`: The port number of the application running in the server member
- `TARGET_ADDRESS`: The IP address of the pool member
- `--weight`: Weight of the server member. This takes effect only when the load balancing algorithm of its belonging pool is weighted_round_robin
- `--json`: Format output in JSON

---
### `ibmcloud is load-balancer-pool-member-update`

Update a member of a load balancer pool

**Syntax**

`ibmcloud is load-balancer-pool-member-update LOAD_BALANCER_ID POOL_ID MEMBER_ID [--port PORT] [--target-address TARGET_ADDRESS] [--weight WEIGHT] [--json]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `MEMBER_ID `: ID of the member
- `--port`: The port number of the application running in the server member
- `--target-address`: The IP address of the pool member
- `--weight`: Weight of the server member. This takes effect only when the load balancing algorithm of its belonging pool is weighted_round_robin
- `--json`: Format output in JSON

---

### `ibmcloud is load-balancer-pool-member-delete`

Delete a member from a load balancer pool

**Syntax**

`ibmcloud is load-balancer-pool-delete LOAD_BALANCER_ID POOL_ID MEMBER_ID [-f, --force]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `POOL_ID `: ID of the pool
- `MEMBER_ID `: ID of the member
- `-f, --force`: Force delete without confirmation.

---
### `ibmcloud is load-balancer-statistics`

List all statistics of a load balancer

**Syntax**

`ibmcloud is load-balancer-statistics LOAD_BALANCER_ID [--json]`

**Options**
- `LOAD_BALANCER_ID `: ID of the load balancer
- `--json`: Format output in JSON

