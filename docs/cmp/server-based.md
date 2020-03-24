# Server-based API (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

A netID Partner (TAPP) that sends a user through the Single Sign-On Flow and requests manage a privacy status receives the authentication token (`token`) after the successful login, based on which a user can be authenticated at the netID Permission Center to enable read/write access for that specific users privacy status.



!!! info  ""
    The server-based requests are secured via the authentication token.
    Calls of this type are blocked from the browser environments for security reasons (no Origin header is allowed!)

## Read APIs

### Accessing a user identifier

A CMP can retrieve the user's identifier (TPID) via the following interface:

``` shell
GET https://READSERVICE.netid.de/identification/tpid?
      token=<TOKEN>
```

``` shell
200 OK
Content-Type: application/vnd.netid.identification.tpid-read-v1+json
{
  "tpid": "<TPID>|null"
  "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users identifier (`tpid`). Only present if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null. |

| status | meaning | tpid |
| ----------- | ----------- | ----------- |
| OK | A TC string was stored for this TPID. | x |
| NO_TOKEN | No authentication token was transferred. | - |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("Identification"). | - |

### Privacy status

``` shell
GET https://READSERVICE.netid.de/permissions/iab-permissions?
      token=<TOKEN>
```

``` shell
200 OK
Content-Type: application/vnd.netid.permissions.iab-permission-read-v1+json

{
  "tpid": "<TPID>|null",
  "tc": "<TC string>|null",
  "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

**JSON Properties**

| |Description|
|---|---|
| tpid | Users identifier (`tpid`). Only present if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null. |
| tc | The TC String which should be stored for this this user in relation to the netID Partner (TCF 2.0) Only with status "OK". Otherwise null. |

| status | significance | tc | tpid |
| ----------- | ----------- | ----------- | ----------- |
| OK | TC String stored for this `tpid`. | x | x |
| NO_TPID | No authentication token was transferred. | - | - |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the `tpid` missing ("Identification"). | x | - |

## Write APIs
### Privacy status

``` shell
POST https://WRITESERVICE.netid.de/permissions/iab-permissions?
      token=<TOKEN>
{
  "identification": "true|false",
  "tc": "<TC string>"
}
```

``` shell
201 CREATED
Location: https://READSERVICE.netid.de/permissions/iab-permissions?
      token=<TOKEN>

{
  "tpid": "<TPID>|null",
  "status": "OK|NO_TOKEN|TOKEN_ERROR"
}
```

Remarks:

- If permission "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP. 
- If only the TC string is to be updated and the permission "Identification" already exists, only the "tc" attribute can be passed. Both can also be written at the same time.
- In case of revocation of permission "Identification", would pass only "identification: false".

**JSON Properties**

**request**

| |Description|
|---|---|
| identification | Boolean flag, indicating the status of the permission "Identification". <br>*Yes* = Consent given <br> *No* = consent not given / revoked |
| tc | The TC String which should be stored for this this user in relation to the netID Partner (TCF 2.0)  |

**response**

| |Description|
|---|---|
| tpid | Users identifier (`tpid`). Only present if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null. |

| status | significance |
| ----------- | ----------- |
| OK | TC String / ID CONSENT was saved. |
| NO_TOKEN | No authentication token was transferred. |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. |
