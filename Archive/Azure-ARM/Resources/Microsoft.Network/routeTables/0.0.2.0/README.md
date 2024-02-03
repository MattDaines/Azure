# Route Tables

Route tables are associated to one or many subnets to control the flow of traffic in your virtual network. This template is designed to deploy one route tables per subnet and as such makes use of the snetProperties parameter.

## Parameters

### Required

#### vnetName

The name of the virtual network. Used for the route table name.

| Field | Value   |
| ----- | ------  |
| Type  | String  |
| Min Length | 2  |
| Max Length | 64 |

##### vnetName Example

```json
"vnetName": {
    "value": "example-vnet"
}
```

### routeTablePer

A string that accepts either `VirtualNetwork` or `Subnet`. Will default to `Subnet` if the count of the `rtProperties` array is greater than 1.

| Field | Value |
| ----- | ----- |
| Type  | String |

#### routeTablePer Examples

```json
"routeTablePer": {
    "value": "VirtualNetwork"
}
```

#### rtProperties

An array of route tables including user defined routes to configure.

| Field | Value  |
| ----- | -----  |
| Type  | Array  |

##### snetProperties Example

```json
"snetProperties": {
    "value": [
        {
            "snetName": "subnet01",
            "disableBgpRoutePropagation": true,
            "routes": [
                {
                    "name": "to_Internet",
                    "properties": {
                        "addressPrefix": "0.0.0.0/0",
                        "nextHopType": "Internet"
                    }
                },
                {
                    ...
                }
            ]
        },
        {
            "snetName": "subnet02",
            "disableBgpRoutePropagation": true,
            "routes": [
                ...
            ]
        }
    ]
}
```

## References
