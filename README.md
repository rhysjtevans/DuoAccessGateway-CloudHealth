# DuoAccessGateway (SimpleSAMLPHP) & CloudHealth

This JSON file will allow the mapping of AD Groups to manage user roles/permissions with [CloudHealth](https://www.cloudhealthtech.com) using the Duo Access Gateway as an SSO endpoint instead of manually specifying the name of the role in each user accounts Active Directory attribute.

It does this by querying the groups assigned to the user in Active Directory and performs a regex query against them removing anything that doesn't fit the CloudHealth naming convention of "cloudhealth-ROLENAME" e.g. "cloudhealth-administrator"

The [SimpleSAMLPHP](https://simplesamlphp.org) Authentication [Processing Filter](https://simplesamlphp.org/docs/1.5/simplesamlphp-authproc) **attributealter** is used to manipulate the SAMLResponse.

This guide applies to the [Duo Access Gateway](https://duo.com/docs/dag) however the AuthProc can be modified to suit your needs.

Synchornising groups and users to Duo is outside scope.

## Getting Started

1. Create a new Application in the Duo Web Admin console as per usual with the correct settings
2. Download the IKEY.json file from this repo
3. Download the Duo CloudHealth Application config from the Duo Admin Console
4. Open both and substitue the Jinja variables with the values in the downloaded config from Duo Admin Console
5. Create AD groups matching the role ID's found in the CloudHealth admin console.  E.g.  
    - cloudhealth-administrator  
    - cloudhealth-standard  
    - cloudhealth-power
6. Add users to your AD groups and allow Duo to sync with Active Directory
7. Import your updated IKEY.json file in to your Duo Access Gateway console
8. Test logging in to CloudHealth via Duo
