# Network Security Groups

Network Security Groups (NSGs) add rules to the software defined network. They're essentially dumb firewalls/packet filters. They can be associated with subnets, network interfaces or both. This template is design to deploy a single network security group for a single virtual network.

## Parameters

### Required

#### vnetName

The virtual network name is used in name for the NSG. Check out the template variable nsgNameFormat to change the name format. The name format will also need to be amended in the virtual network template.

| Field | Value  |
| ----- | -----  |
| Type  | String |
| Min Length | 2  |
| Max Length | 64 |

##### vnetName Example

```json
"vnetName": {
    "value": "example-vnet"
}
```

#### nsgInboundRules

A JSON arrary of network security rules. The splitting of Inbound rules and Outbound rules in separate parameters is purely cosmetic. The two arrays are unioned together in the template.

| Field | Value  |
| ----- | -----  |
| Type  | Array |

##### nsgInboundRules Example

```json
"nsgInboundRules": {
    "value": [
        {
            "name": "in_DenyAll",
            "properties": {
                "description": "Denies all inbound flows that haven't been explicitly allowed.",
                "direction": "Inbound",
                "access": "Deny",
                "protocol": "*",
                "priority": 4096,
                "sourcePortRange": "*",
                "destinationPortRange": "*",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*"
            }
        }
    ]
}
```

#### nsgOutboundRules

A JSON arrary of network security rules. The splitting of Inbound rules and Outbound rules in separate parameters is purely cosmetic. The two arrays are unioned together in the template.

| Field | Value  |
| ----- | -----  |
| Type  | Array |

##### nsgOutboundRules Example

```json
"nsgOutboundRules": {
    "value": [
        {
            "name": "out_DenyAll",
            "properties": {
                "description": "Denies all outbound flows that haven't been explicitly allowed.",
                "direction": "Outbound",
                "access": "Deny",
                "protocol": "*",
                "priority": 4096,
                "sourcePortRange": "*",
                "destinationPortRange": "*",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*"
            }
        }
    ]
}
```

## References
