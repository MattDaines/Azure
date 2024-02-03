# Virtual Networks

Virtual networks are a fundamental building block of Azure. The resource enables you to build your own private software defined network for other Azure resources to utilise.

## Parameters

### Required

#### vnetName

The name of the virtual network. If you've also deployed Route Tables or NSGs prior to deploying this template then this parameter should be identical to those template(s).

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

#### vnetAddressPrefixes

A comma separated list of address ranges in CIDR notation.

| Field | Value  |
| ----- | -----  |
| Type  | Array |
| Min Length | 1  |
| Max Length | 255 |

##### vnetAddressPrefixes Example

```json
"vnetAddressPrefixes": {
    "value": [
        "10.0.0.0/8",
        "172.16.0.0/12",
        "192.168.0.0/16"
    ]
}
```

#### routeTablePer

A switch parameter that defines the name to use for route tables. If `VirtualNetwork` all subnets with `attachRT` set to `true` will use a route table named: `<vnetName>-rt`. If `Subnet` is used, all subnets with `attachRT` set to `true` will use a route table named `<vnetName>-<subnetName>-rt`.

| Field | Value  |
| ----- | -----  |
| Type  | String |
| Allowed Values | `VirtualNetwork` or `Subnet`  |

##### routeTablePer Examples

```json
"routeTablePer": {
    "value": "VirtualNetwork"
}
```

#### snetProperties

A JSON array of subnets to deploy and their properties to apply.

snetProperties (Subnet properties) is a complex array parameter that is used to deploy and configure subnets within the virtual network. The table below details all currently implemented subnet properties. 

If `attachNSG` is set to `true` then you have an implicit dependency on the network security group (NSG) template. If you've changed the naming convention in the NSG template you will also need to be update the naming convention used in the virtual network template.

If `attachRT` is set to `true` then you have an implicit dependency on the route table template. Like the NSG, if you've changed the naming convention in the route table template then you will also need to update the virtual network template. It's worth noting that the naming convention for the route table will vary depending on whether route tables are being created per `VirtualNetwork` or `Subnet`. The value for `routeTablePer` should be identical between this virtual network template and the route table template.

As a result of this naming convention, `name` in `snetProperties` should match name used in the route tables template.

| Parameter Property | Type | Expected Value |
| ----- | -----  | -----  |
| `name` | String  | Subnet name between 1-80 characters |
| `addressPrefix` | String | A string representing an address space in CIDR notation. Example: `10.0.0.0/24` |
| `attachNSG` | Boolean | A `true` or `false` value. If true, requires the NSG template to be deployed beforehand |
| `attachRT` | Boolean | A `true` or `false` value. If true, requires the Route Table template to be deployed beforehand |
| `serviceEndpoints` | Array | See [MS Docs](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview#vnet-service-endpoint-policies) for a list of valid service endpoints. See *snetProperties Example* or the parameter file for input examples. |
| `delegations` | Array | Check MS Docs or the Azure Portal for valid delegations. See *snetProperties Example* or the parameter file for input examples. |
| `privateEndpointNetworkPolicies` | String | `"Enabled"`, `"Disabled"` or `null` |

##### snetProperties Example

```json
"snetProperties": {
    "value": [
        {
            "name": "subnet01",
            "addressPrefix": "10.0.0.0/24",
            "attachNSG": false,
            "attachRT": true,
            "serviceEndpoints": [
                {
                    "service": "Microsoft.Storage"
                },
                {
                    "service": "Microsoft.KeyVault"
                }
            ],
            "delegations": [
                {
                    "name": "Delegation",
                    "properties": {
                        "serviceName": "Microsoft.Web/serverFarms",
                        "actions": [
                            "Microsoft.Network/virtualNetworks/subnets/action"
                        ]
                    }
                }
            ],
            "privateEndpointNetworkPolicies": null
        },
        {
            "name": "subnet02",
            ...
        }
    ]
}
```

## Optional

#### vnetDnsServers

A comma separated list of domain name servers to use. If no parameter is provided this template will default to Azure Provided DNS.

| Field | Value  |
| ----- | -----  |
| Type  | Array |
| Max Length | 20 |
| Default Value | 168.63.129.16 |

##### vnetDnsServers Example

```json
"vnetDnsServers": {
    "value": [
        "1.1.1.1",
        "8.8.8.8"
    ]
}
```

## References

| Relevant Property | Link |
| - | - |
| vnetName | [Virtual Network Name Limits](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules#microsoftnetwork) |
| vnetDnsServers | [DNS servers per virtual network](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#networking-limits) |