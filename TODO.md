Platform testing todos
============

ahdis
=====

- ATNA: Connection does not yet work with openssl s_client -connect adapter.test.emedo.ch:20001 -cert mtls_caraikit_int.cer -key mtls_caraikit_int.key -CAfile emedo_EMO-SRV01_CA.pem (QL retries, see also index.hmtml


BINT questions
==============

Major:
- Problem using STS Provider with [TCU](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)
- PIX V3 Feed process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/9dd19e38-c691-4846-a826-6e14b24c5cb0):

Normal:
- Problem using STS Provider with [HIN](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)

Minor:
- No Webservice CH:PPQ endpoint available ?
- No Webservice CH:ATC endpoint available? 
- No Webservice SVS endpoint available? 

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
      - What is the process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/6889628d-6f9c-4e87-805f-088964e8a0e4):
         Patient id unknown assigning authority OID: Unknown OID:2.16.756.5.30.1.145, now using 2.16.756.5.30.1.191.999.10 for IKIT

- 4. Query and retrieve documents for a patient from the EPR

- 4.1 Authorization
  - https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8
  - https://ikit.cara.ch/dep/#/transaction/084aa6c0-fca2-4cce-b1c7-033703d29819

            <![CDATA[ERROR <Ens>ErrBPTerminated: Terminating BP BINT.AD.XUA.Process.AssertionProviderProcess # due to error: ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1
  > ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1]]>
          </wst:Reason>

  Blocked until we get the Authorization token


- 5. Publish documents for a patient by a healthcare professional

- 5.1 provide a document with a technical user (TCU)

    Problem generating STS [see request](https://ikit.cara.ch/dep/#/transaction/6889628d-6f9c-4e87-805f-088964e8a0e4):

```
<![CDATA[ERROR <Ens>ErrBPTerminated: Terminating BP BINT.AD.XUA.Process.AssertionProviderProcess # due to error: ERROR #5002: ObjectScript error: <SUBSCRIPT>GetGroupsForHCP+20^BINT.AD.XUA.WebServices.1 *tGroupsArr() Subscript 1 is "" > ERROR #5002: ObjectScript error: <SUBSCRIPT>GetGroupsForHCP+20^BINT.AD.XUA.WebServices.1 *tGroupsArr() Subscript 1 is ""]]>
```

- 7.1 Query entries
- 7.2 Add an entry
- 7.3 Modify an entry
- 7.4 Delete an entry

  All HPD transactions have been tested