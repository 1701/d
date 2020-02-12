# Specification for Consent Management Providers

## Data export for partners

Via this API partners get the ability to query netID permissions and TC strings of users (export) unrelated to a specific context, via the specification of changed_since  deltas can also be queried. There is an HTTP service with a REST API for this service.

``` shell
GET https://DATA-EXPORT-SERVICE/permissions/iab-permissions? tapp_id=<TAPP_ID>&changed_since=<DATE>
Accept: application/vnd.netid.permissions.iab-permission-export.list-v1+json
Authorization: Basic <b64(USERNAME:PASSWORD)>
```

``` shell
200 OK
Content-Type: application/vnd.netid.permissions.iab-permission-export.list-v1+json

{
  [
    {
      "tpid": "<tpid>",
      "type": "IDCONSENT",
      "status": "VALID",
      "changed_at": "<timestamp>"
    },
    {
      "tpid": "<tpid>",
      "tc": "<tc-string>",
      "changed_at": "<timestamp>"
    }
  ]
}
```
