# Route Tables

Route tables are associated to one or many subnets to control the flow of traffic in your virtual network. This template is designed to deploy one route table per subnet and as such makes use of the snetProperties parameter.

## Parameters

### Required

#### vnetName

The name of the virtual network.

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

#### snetProperties

An array of multiple properties to configure multiple route tables through a single deployment.

| Field | Value  |
| ----- | -----  |
| Type  | Array |

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
                }
            ]
        }
    ]
}
```

## References
