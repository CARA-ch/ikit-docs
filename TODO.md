Platform testing todos
============

- Manual configuration for IdPs for using STS Provider with [HIN](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)
- No Webservice CH:PPQ / CH:ATC or SVS  endpoint  

Verified and udpated IKIT requests
==================================

-  2.1 Check if the patient has an EPR based on AHVN13/NAVS
-  2.2 Demographics Query verified, open Issues
       - Not an error if more than 5 results: https://ikit.cara.ch/dep/#/transaction/3fb82e89-4a8e-41a6-97e2-19563f963bc2
- 3. Register a patient from the primary system in the community and query the patient community id
- 3.1 Register local patient Id in the community
- 4. Query and retrieve documents for a patient from the EPR
- 4.1 Authorization
  - https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8
  - https://ikit.cara.ch/dep/#/transaction/084aa6c0-fca2-4cce-b1c7-033703d29819

            <![CDATA[ERROR <Ens>ErrBPTerminated: Terminating BP BINT.AD.XUA.Process.AssertionProviderProcess # due to error: ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1
  > ERROR #5001: Failed to load user:HIN_8a48175e776d770c414b37f1236b4a03553f6da1a94ccb7d990fe3c1b75941c1]]>
          </wst:Reason>

  Configured manually, waiting for that STS accepts also GLN from HIN, same issue with TrustId which has no GLN.

  NOTE: STS Request, if you extract the saml:Assertion the two namespace definitions are missing and need to be added:  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:s="http://www.w3.org/2001/XMLSchema" into wsse:security or above

  4.2a Query documents from the CARA community
  4.3a Retrieve documents from the CARA community
  4.2b Query documents from remote communities
  4.3b Retrieve documents from remote communities
  
  see above comments apply (prefix, start-info)

- 5. Publish documents for a patient by a healthcare professional

TCU tested with Ludovic and Oliver

- 7.1 Query entries
- 7.2 Add an entry
- 7.3 Modify an entry
- 7.4 Delete an entry


TODO
 - change metadata of existing documents (2.223)

