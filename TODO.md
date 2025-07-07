Open issues:
============

[] ATNA: Check necessity of CA File for TLS connection (see open issue in index.html)
[] Should we / do we expose https://adapter.test.emedo.ch/UPIProxy/services/PDQV3ManagerService separately https://adapter.test.emedo.ch/UPIProxy/services/PIXV3ManagerService over the IKIT? (ikit-config.md)
[] No CH:PPQ endpoint available ? (ikit-config.md)
[] No CH:ATC endpoint available? (ikit-config.md)
[] No SVS endpoint available?
[] Is TCU SAML2 endpoint configured for /eprik-cara/camel/tcu (ikit-config.md)?
[] atna.ikit.cara.ch:8080 or :80 (currently 83.228.202.234), we need to define the DNS entry in CARA DNS?
[] What capability have the two services (documented in excel from samir)?
   - https://adapter.test.emedo.ch/wsproxy/services/SpidQueryService2/ 
   - https://adapter.test.emedo.ch/wsproxy/services/SpidManagementService/

[] Configure IdP's as a separate IdP application under https://ikit.cara.ch/idp -> Quentin Todo
   - Use the IdP Assertion from IKIT -> update text to new setup
   - reference it it via the HTTP header (replace x-eprik-idp-assertion-id with
value received after authenticating --> this would be probably not supported anymore (or will we add an API for that?)

[] home community assigning authority for emedo 2.16.756.5.30.1.177.2.2.1.1 	



Verified and udpated IKIT requests
==================================

-  2.1 Check if the patient has an EPR based on AHVN13/NAVS
-  2.2 Demographics Query verified, open Issues
       - Not an error if more than 5 results: https://ikit.cara.ch/dep/#/transaction/3fb82e89-4a8e-41a6-97e2-19563f963bc2
       - Validation Error on response if no telecom https://ikit.cara.ch/dep/#/transaction/38635a48-56cc-4348-89b8-ecd8c3eabb38 (minor)
       - see [#1](https://github.com/CARA-ch/ikit-docs/issues/1)


- 3. Register a patient from the primary system in the community and query the patient community id

- 3.1 Register local patient Id in the community
      - What is the process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/9dd19e38-c691-4846-a826-6e14b24c5cb0):
         1. Provider organization is unknown but is required:Unknown OID:2.16.756.5.30.1.145. Please add to the Facility Registry
         2. Patient id unknown assigning authority OID: Unknown OID:2.16.756.5.30.1.145, now using 2.16.756.5.30.1.191.999.10 for IKIT

   - Support response in PDQ V3 request:
      - https://ikit.cara.ch/dep/#/transaction/a372bca7-4f0e-40fb-8c53-282fc661883e
      - The requested URL was rejected. Please consult with your administrator.


- 4. Query and retrieve documents for a patient from the EPR

- 4.1 Authorization
  - https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8
  - https://ikit.cara.ch/dep/#/transaction/084aa6c0-fca2-4cce-b1c7-033703d29819

            <![CDATA[ERROR <Ens>ErrBPTerminated: Terminating BP BINT.AD.XUA.Process.AssertionProviderProcess # due to error: ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1
  > ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1]]>
          </wst:Reason>
  
- TCU capability: How do I do with EPRIK?
