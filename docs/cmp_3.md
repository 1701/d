# Specification for Consent Management Providers

## APIs server-based (backend integration)

Description of the backend integration of the netID Permission Center by the CMP (integration from the server side / backend of the CMP if available).

In the case of first use and netID registration via the SSO flow, the publisher (TAPP) receives the authentication token (`token`) after the successful login, with which the user can be authenticated at the netID Permission Center. The CMP can use this authentication token to read and write the netID permissions / TC string of the user.

Remarks:

- The server-based requests are secured by the authentication token.

- Calls of this type are blocked from the web (no Origin header is allowed!)

### Reading the netID Identifier (TPID)

A CMP can retrieve the netID Identifier (TPID) via the following
interface:

``` shell
GET https://READSERVICE.netid.de/identification/tpid?token=<TOKEN>
Accept: application/vnd.netid.identification.tpid-read-v1+json
```

``` shell
200 OK
Content-Type: application/vnd.netid.identification.tpid-read-v1+json
{
  "tpid": "<TPID>|null"
  "status": "OK|NO_TOKEN|TOKEN_ERROR|CONSENT_REQUIRED"
}
```

#### JSON Properties

##### tpid

The ID of the netID user (`tpid`). Only if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null.

##### status

| status | meaning | tc oder pid??? @andrea |
| ----------- | ----------- | ----------- |
| OK | A TC string was stored for this TPID. | x |
| NO_TOKEN | No authentication token was transferred. | - |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. | - |
| CONSENT_REQUIRED | Consent for passing on the TPID missing ("Identification"). | x |

### Read permission (Identification, TC string)

``` shell
GET https://READSERVICE.netid.de/permissions/iab-permissions?token=<TOKEN>
Accept: application/vnd.netid.permissions.iab-permission-read-v1+json
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

#### JSON Properties

##### tpid

The ID of the netID user (`tpid`). Only if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null.

##### tc

The TC string stored for this `tpid` for this publisher (TCF 2.0). Only with status "OK". Otherwise null.

##### status

| status | significance | tc | pid |
| ----------- | ----------- | ----------- | ----------- |
| OK | TC String was stored for this `tpid`. | x | x |
| NO_TPID | No authentication token was transferred. | - | - |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. | - | - |
| CONSENT_REQUIRED | Consent for passing on the `tpid` missing ("Identification"). | x | - |

### Writing the permission (identification, TC string)

``` shell
POST https://WRITESERVICE.netid.de/permissions/iab-permissions?token=<TOKEN>
Content-Type: application/vnd.netid.permissions.iab-permission-write-v1+json
{
  "identification": "true|false",
  "tc": "<TC string>"
}
```

``` shell
201 CREATED
Location: https://READSERVICE.netid.de/permissions/iab-permissions?token=<TOKEN>

{
  "tpid": "<TPID>|null",
  "status": "OK|NO_TOKEN|TOKEN_ERROR"
}
```

Remarks:

- If permission "identification" has been given by the user, this must be signaled by passing "identification: true". For the avoidance of doubt, this of course requires the prior collection of this consent by the CMP. 
- If only the TC string is to be updated and the permission "Identification" already exists, only the "tc" attribute can be passed. Both can also be written at the same time.
- In case of revocation of permission "Identification", would pass only "identification: false".

#### JSON Properties

##### request

###### identification
The permission "Identification" (ID CONSENT) is to be stored (or not).

###### tc
The TC String which should be stored for this TPID for this publisher (TCF 2.0).

##### response

###### tpid

The ID of the netID user (`tpid`). Only if consent "Identification" is given, the `tpid` is present and status "OK". Otherwise null.

###### status

| status | significance |
| ----------- | ----------- |
| OK | TC String / ID CONSENT was saved. |
| NO_TOKEN | No authentication token was transferred. |
| TOKEN_ERROR | Authentication token (JWT) has expired or is invalid. |
