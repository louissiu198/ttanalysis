# TikTok Analysis
## Signatures
### X-Argus
Generate Protobuf
CAL -> calculation to calculate specific values
HINT => easy to figure out, a hint provided
DEP => depreciated

Protobuf Field Table
| Field Number | Data Type      | Field Name                        | Description                       | Calculation                       | Required                          |
|--------------|----------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| 1            | `int64`        | Magic                              | 0x20200929 << 1
| 2            | `int64`        | Version                            | 2
| 3            | `int64`        | XorRand                            | range(0, 0x7FFFFFFF) << 1                                             | Depends
| 4            | `string`       | AppId                              | 1233                              | 1233, 1340, 1180, ....            | True
| 5            | `string`       | DeviceId                           | 75...........                     | LogEndpoint -> DeviceRegister
| 6            | `string`       | LicenseID                          | 2142840551                        | AppVersion > 260000               | True - match x-ladon
| 7            | `string`       | AppVersion                         | 38.X.X                            | Latest -> 38.3.2                  | True
| 8            | `string`       | MssdkVersionStr                    | v05.01.00-ov-android              | [CAL] appVer -> mssdkVerStr       | True - match with int
| 9            | `int64`        | MssdkVersionInt                    | 83951648 << 1                     | [CAL] mssdkVerStr -> mssdkVerInt  | True - match with str
| 10           | `bytes`        | EncryptBytes                       | \x00\x00\x00\x00\x00\x00\x00\x00  |                                   | True
| 11           | `int64`        | DevicePlatform                     | 0                                 | [DEP]: android -> 0; iOS -> 1
| 12           | `int64`        | Timestamp                          | timestamp << 1
| 13           | `bytes`        | SM3-Stub                           | sm3(stub if not none else 16 bytes) | [CAL]: sm3    
| 14           | `bytes`        | SM3-Query                          | sm3(query)                          | [CAL]: sm3
| 15           | `field`        | DeviceCount                        | 
| 15.1         | `int64`        | unknown                            | range(1, 100) << 1
| 15.2         | `int64`        | unknown                            | range(1, 8) << 1
| 15.3         | `int64`        | unknown                            | range(1, 8) << 1
| 15.4         | `int64`        | unknown                            |                                   | [HINT]: specific range            | True
| 15.5         | `int64`        | unknown                            | range(1, 8) << 1
| 15.6         | `int64`        | unknown                            | range(1, 8) << 1
| 15.7         | `int64`        | unknown                            | timestamp << 1
| 16           | `string`       | DeivceToken                        |                                   | MssdkEP -> SdiGetToken             | Depends - anti-system 20% chance don't check 
| 17           | `int64`        | Timestamp                          | timestamp << 1
| 18           | `bytes`        | LanuskHash                         | md5(x-bd-lanusk)                  | NormalEP -> RegisterAccount        | Depends - required if login
| 19           | `bytes`        | PskCalHash                         |                                   | [CAL]: psk_cal_hash(query, stub)   | Depends - required if login
| 20           | `string`       | PskVersion                         | login: 0 ; guest: none
| 21           | `int64`        | paskCalType                        | 624                               | DID 6 -> 738, DID 7 -> 624
| 23           | `field`        | DeviceInfo                         |
| 23.1         | `string`       | DeviceType                         | samsumg
| 23.2         | `int64`        | MetaSecConstant                    |                                   | [CAL]: hash for osVersion          | True
| 23.3         | `string`       | DeviceChannel                      | android  
| 23.4         | `int64`        | AppVersionConstant                 |                                   | [CAL]: hash for appVersion         | True 
| 24           | `string`       | SeedData                           | MDGkG5rQqX.....                   | MssdkEP -> MsGetSeed
| 25           | `int64`        | optionType                         |                                   | [HINT]: situation type for dT      | Depends - required if you don't want to send dyn
| 26           | `field`        | dynField                           |                                  
| 26.1         | `int64`        | dynVersion                         |                                   | MssdkEP -> MsGetSeed               | Depends - required if you sign dyn
| 26.2         | `bytes`        | dynHash                            |                                   | [CAL]: 8 different encryption type | Depends - required if you sign dyn for follow/like
| 27           | `int64`        | Timestamp                          | timestamp << 1
| 28           | `int64`        | OptionType                         |                                   | [HINT]: situation type for dT, sD
| 29           | `int64`        | Investigating                      |                                   | [UNKNOWN] 6 digit -> static 
| 30           | `int64`        | optionType                         |                                   | [HINT]: situation type for query
| 31           | `int64`        | Random                             | range(0, 0x7FFFFFFF) << 1         | [UNKNOWN] random                   |
2. Shift / unpack
3. Simon Encrypt into arrays
4. Encrypt Enc Pb
5. Bufer: Pack bytes of sp and field 13 / 14
6. PCK7 Padding (Not Released: a new type of padding for appVer > 38.0.0)
7. AES encrypt
8. base64 encrypt

### X-Ladon
Encrypt "timestamp-licenseId-appId" // data
1. generate key - md5 -> random + appId
2. PCK7 Padding
3. Turn it into arrays of bytes
4. Hash keyByte, data, size of data
5. Base64 encrypt bytes -> string

### X-Gorgon
Depreciated

### X-Khronos
Depreciated
Timestamp - s

### X-SS-STUB
Not Required
MD5hash the string payload

### X-SS-REQ-TICKET
Not Required
Timestamp - ms

