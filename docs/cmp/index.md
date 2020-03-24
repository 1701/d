# General information

In addition to the Single Sign-on, netID Partners can also leverage netID to allow users to manage their overall privacy settings in terms of commercial data usage. This offers a convenient, scalable and most importantly server-based/permanent way to manage a user’s consent status or more generally a status in terms of legal grounds for commercial data usage. 

To enable that netID (here specifically the netID Permission Center) provides the following services to integrate a netID Partners Consent Management Platform. Overall these APIs enable a Partner/his CMP to manage a TC-String associated to an individual user as well as netID specific consents (netID Permissions) which allow him to identity a user while using his services.

In the following descriptions we will refer to the user’s overall privacy setting as **privacy status**.

!!! info  ""
    All permissions (netID specific/TCF) stored/managed using netID are always scoped to an individual netID Partner. That means in terms of the CMP, that netID solely supports service scoped TC-Strings, and more importantly that the user’s explicit consent to be identified is managed/given per netID Partner   

## netID Permission Center Services

The following services are provided by the netID Permission Center to allow a CMP to store / manage a user’s privacy status for a specific netID Partner:

- READ SERVICE: Read the netID identifier (TPID), netID Permissions and TC Strings for an individual user
- WRITE SERVICE: Write netID Permissions and TC Strings for an individual user
- DATA EXPORT SERVICE: Export the netID permissions and TC strings for the respective netID Partner in general

## Read/Write Services

The READ and WRITE services rely on prior user authenticating and are provided in two variants, with overall similar functionalities, to the netID Partners Consent Management Platform.

### Functionality

- Store and retrieve netID Permissions
- Store and retrieve the TC String
- Reading the netID identifier of a specific user (TPID) in case the user has consented

### Variants

1. **Browser based** API: Usage based on an already established user authentication stored within the respective browser (ex-ante)
2. **Server based** API: Usage based on a authentication token acquired via a Single Sign-on.

The distinction browser vs. server-based refers mainly to how active users are authenticated prior to API usage/from where the APIs are being called.

Call information: Parameters / Header / Cookies

| name | type | function  | description |
| ----------- | ----------- | ----------- | ----------- |
| tapp_id | parameter | authentication | is made available by netID for each publisher when it is onboarded on and must be passed unchanged with each request. |
| origin | header | authentication | is passed by the browser for each XMLHttpsRequest (AJAX). The value must be a URL registered for this netID Partner (TAPP). |
| tpid_sec | cookie | user authentication/access token | Only relevant for the browser-based API: is located in the netid.de domain and is automatically passed on by the browser - if available. |
| token | parameter | user authentication/access token | Only relevant for the server-based API: Can be retrieved by the partner via the SSO process, is passed to access the API/identify the user |

## Data export service

The export APIs allows a partner to export the netID Permissions/TC String as well as deltas on those. The APIs is available solely **server based**.

## Authentication for API usage

Authentication of partners for the browser-based APIs is handled via the
parameter `tapp_id` and the `Origin` header. Access is secured via
[CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)

- Multiple URLs are allowed per publisher (TAPP). Those URLs must be registered upfront
- The read/write request must be made from an eligible URL.

Authentication with the server-based APIs is done as follows.

- The user-specific read/write access is secured via respective access tokens (authorization).
- Generic Data Export uses basic authentication

## User authentication when using APIs

Authentication of the individual netID User is done depending on the
API used by means of the `tpid_sec` (browser-based) or the
`token` (server-based).

`tpid_sec` is an ID Token (JWT) which is stored on the domain
netid.de as part of the Single Sign-on session information for the provision of the
netID service during login processes via the SSO/general login with the
netID Account Provider. This token is not accessible for netID Partners /
the CMP.

The Login `token` can be retrieved by a netID Partner during the Single Sign-on
process (OpenID Connect) in the form of a claim. This enables read/write
access independently of the browser session (limited in time).

If, depending on the context, the `token` or the `tpid_sec` does not
exist, has expired or is invalid, a publisher cannot read/write the TC
String and of course cannot access the TPID.

