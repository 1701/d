# Data export

Via this API partners get the ability to query privacy status (netID permissions and TC strings of users) unrelated to a specific context, via the specification of changed_since  deltas can also be queried. There is an HTTP service with a REST API for this service.

``` shell
GET https://DATA-EXPORT-SERVICE/permissions/iab-permissions? 
    tapp_id=<TAPP_ID>&
    changed_since=<DATE>
    Authorization: Basic <b64(USERNAME:PASSWORD)>
```

``` shell
200 OK

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
