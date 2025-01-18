# Protobuf Field Table


| Field Number | Data Type      | Field Name                        | Description                       | Calculation                       |
|--------------|----------------|-----------------------------------|-----------------------------------|-----------------------------------|
| 1            | `int32`       | Magic                              | 0x20200929 << 1
| 2            | `int32`       | Version                            | 2
| 3            | `string`      | XorRand                            | randint(0, 0x7FFFFFFF) << 1
| 4            | `int32`       | AppId                              | params["aid"]
| 5            | `bool`        | DeviceId                           | 75...........                     | LogEndpoint -> DeviceRegister
| 6            | `string`      | LicenseID                          | 2142840551                        | AppVersion > 260000
| 7            | `string`      | AppVersion                         | 38.X.X                            
| 8            | `string`      | MssdkVersionStr                    |
| 9            | `string`      | MssdkVersionInt                    |
| 10           | `string`      | EncryptBytes                       |
| 11           | `float`       | DevicePlatform                     |
| 12           | `int64`       | Timestamp                          |
| 13           | `int64`       | SM3-Stub                           |
| 14           | `string`      | SM3-Query                          |
| 15           | `string`      | DeviceInfo                         |
| 16           | `bool`        | DeivceToken                        |
| 17           | `int32`       | Timestamp                          |
| 18           | `string`      | LanuskHash                         |
| 19           | `string`      | PskCalHash                         |
| 20           | `string`      | PskVersion                         |
| 21           | `int32`       | paskCalType                        |
| 23           | `int32`       | DeviceInfo                         |
| 24           | `string`      | SeedData                           |
| 25           | `string`      | optionType                         |
| 26           | `string`      | dynHash                            |
| 27           | `string`      | Timestamp                          |
| 28           | `string`      | OptionType                         |
| 29           | `string`      | Investigating                      |
| 30           | `bool`        | optionType                         |
| 31           | `string`      | Random                             |


