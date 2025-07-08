Open issues:
============

ahdis
=====

- ATNA: Connection does not yet work with openssl s_client -connect adapter.test.emedo.ch:20001 -cert mtls_caraikit_int.cer -key mtls_caraikit_int.key -CAfile emedo_EMO-SRV01_CA.pem (QL retries, see also index.hmtml


CARA Open issues
================

- Need to add DNS Entry for atna.ikit.cara.ch to IP 83.228.202.234)
- oegger access rights to https://github.com/CARA-ch/ikit-docs

BINT questions
==============

- What capability have the two services (documented in excel from samir, maybe the proxy for UPI)?
   - https://adapter.test.emedo.ch/wsproxy/services/SpidQueryService2/ 
   - https://adapter.test.emedo.ch/wsproxy/services/SpidManagementService/
- Can we somewhere see the ATNA AuditEvents in the platform?
- No CH:PPQ endpoint available ?
- No CH:ATC endpoint available? 
- No SVS endpoint available? 
- What should be the HL7 v3 Receiver Device ID for PIXV3, PDQV3
- PDQ V3 behaviour more than 5 results (see below)
- PIX V3 Feed process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/9dd19e38-c691-4846-a826-6e14b24c5cb0):
- Problem using STS Provider with [HIN](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)
- Problem using STS Provider with [TCU](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)


Verified and udpated IKIT requests
==================================

-  2.1 Check if the patient has an EPR based on AHVN13/NAVS
   
   - https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXPDQV3ManagerService and https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXV3ManagerService has the same behaviour

-  2.2 Demographics Query verified, open Issues
       - Not an error if more than 5 results: https://ikit.cara.ch/dep/#/transaction/3fb82e89-4a8e-41a6-97e2-19563f963bc2
       - Validation Error on response if no telecom https://ikit.cara.ch/dep/#/transaction/38635a48-56cc-4348-89b8-ecd8c3eabb38 (minor)
       - see [#1](https://github.com/CARA-ch/ikit-docs/issues/1)
       - Problem with Querying WEI... [#2](https://github.com/CARA-ch/ikit-docs/issues/2)
       - https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXPDQV3ManagerService and https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PDQV3ManagerService have the same behaviour


- 3. Register a patient from the primary system in the community and query the patient community id

- 3.1 Register local patient Id in the community
      - What is the process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/9dd19e38-c691-4846-a826-6e14b24c5cb0):
         1. Provider organization is unknown but is required:Unknown OID:2.16.756.5.30.1.145. Please add to the Facility Registry
         2. Patient id unknown assigning authority OID: Unknown OID:2.16.756.5.30.1.145, now using 2.16.756.5.30.1.191.999.10 for IKIT

- 4. Query and retrieve documents for a patient from the EPR

- 4.1 Authorization
  - https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8
  - https://ikit.cara.ch/dep/#/transaction/084aa6c0-fca2-4cce-b1c7-033703d29819

            <![CDATA[ERROR <Ens>ErrBPTerminated: Terminating BP BINT.AD.XUA.Process.AssertionProviderProcess # due to error: ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1
  > ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1]]>
          </wst:Reason>

  Blocked until we get the Authorization token


- 5. Publish documents for a patient by a healthcare professional

  Blocked until we get the Authorization token

- 5.1 provide a document with a technical user (TCU)

   we can get the TCU assertion here: https://ikit.cara.ch/idp/tcu
   However when using it it returns an error
   https://ikit.cara.ch/dep/#/transaction/b48879c0-831f-4191-8b5e-7467a61da89c
   Request Rejected_ The requested URL was rejected. Please consult with your administrator.
   Your support ID is: 11943732372851740539
   To which organization is the TCU assigned with the NameId 2.16.756.5.30.1.999.9.1.1.1?
   Do we have a HCP for this organization?


- 7.1 Query entries
- 7.2 Add an entry
- 7.3 Modify an entry
- 7.4 Delete an entry

  All HPD transactions have been tested
