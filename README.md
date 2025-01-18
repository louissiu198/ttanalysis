# TikTok Analysis
## Signatures
### X-Argus
1. Generate Protobuf
Protobuf Field Table
| Field Number | Data Type      | Field Name                        | Description                       | Calculation                       | Required                          |
|--------------|----------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| 1            | `int32`       | Magic                              | 0x20200929 << 1
| 2            | `int32`       | Version                            | 2
| 3            | `string`      | XorRand                            | range(0, 0x7FFFFFFF) << 1                                             | Depends
| 4            | `int32`       | AppId                              | 1233                              | 1233, 1340, 1180, ....            | True
| 5            | `bool`        | DeviceId                           | 75...........                     | LogEndpoint -> DeviceRegister
| 6            | `string`      | LicenseID                          | 2142840551                        | AppVersion > 260000               | True - match x-ladon
| 7            | `string`      | AppVersion                         | 38.X.X                            | Latest -> 38.3.2                  | True
| 8            | `string`      | MssdkVersionStr                    | v05.01.00-ov-android              | [CAL] appVer -> mssdkVerStr       | True - match with int
| 9            | `string`      | MssdkVersionInt                    | 83951648 << 1                     | [CAL] mssdkVerStr -> mssdkVerInt  | True - match with str
| 10           | `string`      | EncryptBytes                       | \x00\x00\x00\x00\x00\x00\x00\x00  |                                   | True
| 11           | `float`       | DevicePlatform                     | 0                                 | [DEP]: android -> 0; iOS -> 1
| 12           | `int64`       | Timestamp                          | timestamp << 1
| 13           | `int64`       | SM3-Stub                           | sm3(stub if not none else 16 bytes) | [CAL]: sm3    
| 14           | `string`      | SM3-Query                          | sm3(query)                          | [CAL]: sm3
| 15           | `string`      | DeviceCount                        | 
| 15.1         | `string`      | unknown                            | range(1, 100) << 1
| 15.2         | `string`      | unknown                            | range(1, 8) << 1
| 15.3         | `string`      | unknown                            | range(1, 8) << 1
| 15.4         | `string`      | unknown                            |                                   | [HINT]: specific range            | True
| 15.5         | `string`      | unknown                            | range(1, 8) << 1
| 15.6         | `string`      | unknown                            | range(1, 8) << 1
| 15.7         | `string`      | unknown                            | timestamp << 1
| 16           | `bool`        | DeivceToken                        |                                   | MssdkEP -> SdiGetToken             | Depends - anti-system 20% chance don't check 
| 17           | `int32`       | Timestamp                          | timestamp << 1
| 18           | `string`      | LanuskHash                         | md5(x-bd-lanusk)                  | NormalEP -> RegisterAccount        | Depends - required if login
| 19           | `string`      | PskCalHash                         |                                   | [CAL]: psk_cal_hash(query, stub)   | Depends - required if login
| 20           | `string`      | PskVersion                         | login: 0 ; guest: none
| 21           | `int32`       | paskCalType                        | 624                               | DID 6 -> 738, DID 7 -> 624
| 23           | `int32`       | DeviceInfo                         |
| 23.1         | `int32`       | DeviceType                         | samsumg
| 23.2         | `int32`       | MetaSecConstant                    |                                   | [CAL]: hash for osVersion          | True
| 23.3         | `int32`       | DeviceChannel                      | android  
| 23.4         | `int32`       | AppVersionConstant                 |                                   | [CAL]: hash for appVersion         | True 
| 24           | `string`      | SeedData                           | MDGkG5rQqX.....                   | MssdkEP -> MsGetSeed
| 25           | `string`      | optionType                         |                                   | [HINT]: situation type for dT      | Depends - required if you don't want to send dyn
| 26           | `string`      | dynField                           |                                  
| 26.1         | `string`      | dynVersion                         |                                   | MssdkEP -> MsGetSeed               | Depends - required if you sign dyn
| 26.2         | `string`      | dynHash                            |                                   | [CAL]: 8 different encryption type | Depends - required if you sign dyn for follow/like
| 27           | `string`      | Timestamp                          | timestamp << 1
| 28           | `string`      | OptionType                         |                                   | [HINT]: situation type for dT, sD
| 29           | `string`      | Investigating                      |                                   | [UNKNOWN] 6 digit -> static 
| 30           | `bool`        | optionType                         |                                   | [HINT]: situation type for query
| 31           | `string`      | Random                             | range(0, 0x7FFFFFFF) << 1         | [UNKNOWN] random                   |
2. Shift / unpack
3. Simon Encrypt into arrays
4. Encrypt Enc Pb
5. Bufer: Pack bytes of sp and field 13 / 14
6. Pck7 Padding
7. AES encrypt
8. base64 encrypt

