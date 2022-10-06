The common requirement for the processing of any ATLAS Service registration process is the following:

- client_id/client_secret (may be the same than the ones provided during service validation)
- A login/password to an account on the service, or the possibility to self register


Additional requirements for services requiring configuration:
Web url of service where a user can login to his account with a browser and access proprietary visualization / configuration features.

It is important to remember that service pairing is ALWAYS performed in the context of a user account. I.e. different users may pair to different ATLAS services, and even when many users utilize
a common service implementation, the pairing is unique to each user as it connects an account he owns on your service to a different account
he owns on a third-party ATLAS service. It is not acceptable to "hard-code" any pairing since pairings are unique and different for each user and require a secure login & consent in the target
service's authentication server.  Consequently, since pairing unequivocally REQUIRES user interactions, any service that needs to communicate with another ATLAS service (e.g. a field_data service), MUST provide a user interface
where it is possible for its users to pair/unpair with the ATLAS service(s) of their choice (for a given ATLAS service template).


Basic checklist:
- Perform an Oauth2 grant_code login to obtain access/refresh tokens
- Perform an Oauth2 token refresh and verify that a refresh_token with a newer expiration is returned
- Verify that pairings can be established and cancelled at will and that only the information that is private to a user will be accessible from
a paired service.
- In case of field_data, test what happens when a urn to an archived field (where applicable) is passed. It should fail
- Generally that the http error codes conform to the specifications, typically for 400, 404, 401, 403 and that the json error body is compliant (it has often occurred that the json body shows the correct error code but the http code remains 200)
- Where gpkg files are generated, check their format against the specifications in fine details
- Check each and every endpoint for compliance specifications; verify the behavior for invalid/unknown parameters. In the case of advisors, check behavior with one application_ref and with many application_ref as well
- Check notifications where relevant
