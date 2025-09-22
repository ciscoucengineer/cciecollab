# Users should authenticate using LDAPS when logging in to Jabber

## Requirements

- End users are logging in to their Cisco Jabber soft clients using their corporate LDAP accounts.
- End users should login using user@domain format.
- LDAP should be secured using TLS
- End users should automatically be assigned the proper roles and service profiles when they are imported in to the local Unified CM directory.
  - Two (2) types of users are in the directory and the service profile assigned should be based on user attributes when they are initially imported in to the directory.

## Solution
