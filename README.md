# DuoAccessGateway (SimpleSAMLPHP) & CloudHealth
This JSON file will allow the mapping of Active Directory groups to [CloudHealth](https://www.cloudhealthtech.com) Roles instead of the CloudHealth standard of using Active Directory Attributes.

This guide applies to the [Duo Access Gateway](https://duo.com/docs/dag) however the AuthProc rules & regex can be modified to suit your needs

## Motivation

 The goal for this was to remove the CloudHealth role e.g. cloudhealth-administrator from an Active Directory user attribute e.g. extensionAttribute1 and move it to a standardised group based membership.
 As a result, the management and reporting on user access roles is standardised alongside other reporting processes and far simpler to update.


## Overview
Duo utilises [SimpleSAMLPHP](https://simplesamlphp.org) and therefore the Authentication [Processing Filter](https://simplesamlphp.org/docs/1.5/simplesamlphp-authproc) **attributealter** is used to manipulate the SAMLResponse sent to CloudHealth.

This is achieved by the SimpleSAMLPHP library querying the groups assigned to the user in Active Directory and performs a regex query against them removing anything that doesn't fit the CloudHealth naming convention of "cloudhealth-ROLENAME" e.g. "cloudhealth-administrator"

## Getting Started

1. Create a new Application in the Duo Web Admin console as per usual with the correct settings
2. Download the IKEY.json file from this repo
3. Download the Duo CloudHealth Application config from the Duo Admin Console
4. Open both and substitute the Jinja variables with the values in the downloaded config from Duo Admin Console
5. Create AD groups matching the role ID's found in the CloudHealth admin console.  E.g.  
    - cloudhealth-administrator  
    - cloudhealth-standard  
    - cloudhealth-power
6. Add users to your AD groups and allow Duo to sync with Active Directory
7. Import your updated IKEY.json file in to your Duo Access Gateway console
8. Test logging in to CloudHealth via Duo

__Ensure your users are a member of a single cloudhealth-* Active Directory group__