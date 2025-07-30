Platform testing todos
============

ahdis
=====

- ATNA: Connection does not yet work with openssl s_client -connect adapter.test.emedo.ch:20001 -cert mtls_caraikit_int.cer -key mtls_caraikit_int.key -CAfile emedo_EMO-SRV01_CA.pem (setup will be checked)


BINT/OFAC questions
==============

High:
- STS response
  1. The namespace declarations are int the outer xml block, meaning that if you extract the saml2:assertion by text it will be invalid xml (see https://ikit.cara.ch/dep/#/transaction/3ee6a610-43fb-42e0-b429-88ba4b282eda, Response Tab xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:s='http://www.w3.org/2001/XMLSchema' are introduced on top but are also used within the saml2:assertion:

      <saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:subject-id">
            <saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">
                Ludovic Frehner
            </saml:AttributeValue>
        </saml:Attribute>

        <saml:Attribute Name="urn:ihe:iti:xca:2010:homeCommunityId">
            <saml:AttributeValue xsi:type="s:string">
                urn:oid:2.16.756.5.30.1.177
            </saml:AttributeValue>
        </saml:Attribute>

          <saml:Attribute Name="urn:e-health-suisse:principal-name">
            <saml:AttributeValue xsi:type="s:string">
                Frehner, Ludovic, emedoint:eb0850e0-8557-4411-9d28-1b71dfde7444
            </saml:AttributeValue>
         </saml:Attribute>

```xml
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="Id-8256E941-6C94-11F0-81D4-0050568D7D0A" IssueInstant="2025-07-29T15:55:54.617Z" Version="2.0"><saml:Issuer Format="urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified">2.16.756.5.30.1.177.2.2.1.1.8</saml:Issuer><Signature xmlns="http://www.w3.org/2000/09/xmldsig#" Id="Id-82605061-6C94-11F0-81D4-0050568D7D0A"><SignedInfo><CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"></CanonicalizationMethod><SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"></SignatureMethod><Reference URI="#Id-8256E941-6C94-11F0-81D4-0050568D7D0A"><Transforms><Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"></Transform><Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"></Transform></Transforms><DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"></DigestMethod><DigestValue>3h/4nF162XmKsFV8UvPH9OAyiFf3BiBicYlxUhfgGwc=</DigestValue></Reference></SignedInfo><SignatureValue>eiUqnBxBUG+Id/F9qWervaoSLg0Dzi5CVr9FrFUwtYMpJgLs9TXQjvhRD3P5rt+HwghfxFbg9xZI/Bw8A2LpPQEcSm7nG98MVqywTa3IrtbVTtS4kaTy6mnT8jrq6iebk6Y4QUEvEIMWPCqJ52eRyYbjfk73uKf5t9wrszwcZPzxIuTHmZeHzGrPVajlxpGOkZ1uY+g321sxwrCktI4i16hQTdWfyDA0bHGdCwZayj9yQ9+F6PMTnlvGWrNrgh582Q0S2X87VJ4+alWAEyNjuSJ0t6wjq5s40gg3rzi+NH5BU6xwiceM8Jz5q9RuxjWzCkwru/k+0vr4+lzKRaz38jHIGll4KimCrJ5/zQLcNFyfFIQEIrDMyduI3brt9jXIu/1qLUQFZP9CTTzog9XnkZ4VwdYE6jOr5jLXQYXUY9q52SF7iMJgOZh/3lgaUvc83mmiQuLlNY0u86bDXn+EQCUzkmqcihJ7Gg6sWOuueBzNt9Jw3mwRn22mfp/TwWsakThfBT/7NCr1qlFYyRiwhllW8gnF122Y6VLqot12vlhO517TbtQgdH8g/22EQKH024JeiHsxs2LQmlLycmGv2gYJ3rFnO8a90EOJ/2bdazb6+Ugg2Jf9Ypn6JFh0kko8m3RF9Lh5+UXyqG2x5hY/CI9IT6o57Kwegs5//or+FYA=</SignatureValue><KeyInfo><X509Data><X509Certificate>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</X509Certificate></X509Data></KeyInfo></Signature><saml:Subject><saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent" NameQualifier="urn:gs1:gln">2012345681729</saml:NameID><saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer"><saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent" NameQualifier="urn:e-health-suisse:technical-user-id">2.16.756.5.30.1.191.999.10</saml:NameID><saml:SubjectConfirmationData><saml:AttributeStatement xmlns:s="http://www.w3.org/2001/XMLSchema" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:subject-id"><saml:AttributeValue xsi:type="s:string">Ludovic Frehner</saml:AttributeValue></saml:Attribute></saml:AttributeStatement></saml:SubjectConfirmationData></saml:SubjectConfirmation></saml:Subject><saml:Conditions NotBefore="2025-07-29T15:55:54.619Z" NotOnOrAfter="2025-07-29T16:10:54.620005089Z"><saml:Condition xmlns:del="urn:oasis:names:tc:SAML:2.0:conditions:delegation" xsi:type="del:DelegationRestrictionType"><del:Delegate ConfirmationMethod="urn:oasis:names:tc:SAML:1.0:cm:sender-vouches" DelegationInstant="2025-07-29T15:55:54.619Z"><saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent" NameQualifier="urn:e-health-suisse:technical-user-id">2.16.756.5.30.1.191.999.10</saml:NameID></del:Delegate></saml:Condition><saml:AudienceRestriction><saml:Audience>urn:e-health-suisse:token-audience:all-communities</saml:Audience></saml:AudienceRestriction></saml:Conditions><saml:AuthnStatement AuthnInstant="2025-07-29T15:50:54.62Z"><saml:SubjectLocality DNSName="emo-adqe.emedo.local.EMEDO"></saml:SubjectLocality><saml:AuthnContext><saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</saml:AuthnContextClassRef></saml:AuthnContext></saml:AuthnStatement><saml:AttributeStatement><saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:subject-id"><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">Ludovic Frehner</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:ihe:iti:xca:2010:homeCommunityId"><saml:AttributeValue xsi:type="s:string">urn:oid:2.16.756.5.30.1.177</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:oasis:names:tc:xacml:2.0:resource:resource-id"><saml:AttributeValue xsi:type="s:string">761337612097656117^^^&amp;2.16.756.5.30.1.127.3.10.3&amp;ISO</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:purposeofuse"><saml:AttributeValue><hl7:PurposeOfUse xmlns:hl7="urn:hl7-org:v3" code="AUTO" codeSystem="2.16.756.5.30.1.127.3.10.5" codeSystemName="eHealth Suisse Verwendungszweck" displayName="Normal Access" xsi:type="hl7:CE"></hl7:PurposeOfUse></saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:oasis:names:tc:xacml:2.0:subject:role"><saml:AttributeValue><Role xmlns="urn:hl7-org:v3" xmlns:hl7="urn:hl7-org:v3" code="HCP" codeSystem="2.16.756.5.30.1.127.3.10.6" codeSystemName="eHealth Suisse EPR Actors" displayName="HealthCare Professional" xsi:type="hl7:CE"></Role></saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:organization"><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">OrgB</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">OrgB1Gr</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">Hôpital Daler</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">CARA</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">Stargate II</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">CARA-CabinetTest</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">CARA-CabinetTest-O</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:oasis:names:tc:xspa:1.0:subject:organization-id"><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:1.1.44.17.201.101</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:1.1.44.17.201.101.1</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:1.1.44.17.208</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:1.1.44.17.298</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:1.9.1</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:2.16.756.5.30.1.191.10.1</saml:AttributeValue><saml:AttributeValue xmlns:s01="http://www.w3.org/2001/XMLSchema" xsi:type="s01:string">urn:oid:2.16.756.5.30.1.191.10.1.1</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:e-health-suisse:principal-id"><saml:AttributeValue xsi:type="s:string">2012345681729</saml:AttributeValue></saml:Attribute><saml:Attribute Name="urn:e-health-suisse:principal-name"><saml:AttributeValue xsi:type="s:string">Frehner, Ludovic, emedoint:eb0850e0-8557-4411-9d28-1b71dfde7444</saml:AttributeValue></saml:Attribute></saml:AttributeStatement></saml:Assertion>
```

  2. The text extracted saml2:assertion does not validate against saml https://www.samltool.io/

Normal:
- Problem using STS Provider with [HIN](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)

Minor:
- Webservice CH:PPQ endpoint 
- Webservice CH:ATC endpoint  
- Webservice SVS endpoint 

Verified and udpated IKIT requests
==================================

-  2.1 Check if the patient has an EPR based on AHVN13/NAVS
   
   - https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXPDQV3ManagerService and https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXV3ManagerService have the same behaviour

-  2.2 Demographics Query verified, open Issues
       - Not an error if more than 5 results: https://ikit.cara.ch/dep/#/transaction/3fb82e89-4a8e-41a6-97e2-19563f963bc2
       - Validation Error on response if no telecom https://ikit.cara.ch/dep/#/transaction/38635a48-56cc-4348-89b8-ecd8c3eabb38 (minor)
       - see [#1](https://github.com/CARA-ch/ikit-docs/issues/1)
       - Problem with Querying WEI... [#2](https://github.com/CARA-ch/ikit-docs/issues/2)
       - https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PIXPDQV3ManagerService and https://ikit.cara.ch/dep/proxy/cara/ahdis/UPIProxy/services/PDQV3ManagerService have the same behaviour

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

  ok, see above comment to add namespace definition for prefixes

  4.3a Retrieve documents from the CARA community

  ok, see above comment to add namespace definition for prefixes
  in difference to the ith platform start-info needs to be added: start-info="application/soap+xml; charset=utf-8"

  4.2b Query documents from remote communities
  ok, see above comments apply (prefix, start-info)

  4.3b Retrieve documents from remote communities
  ok, see above comments apply (prefix, start-info)
  in addition there seems to be a connection problem to abilis? https://ikit.cara.ch/dep/#/transaction/cb9fd22c-9e63-4bee-bf77-f812bc175660 No response from ABILIS_XCARetrieve

- 5. Publish documents for a patient by a healthcare professional

- 5.1 provide a document with a technical user (TCU)

TODO

metadata:
 - TODO: check confidentiality code behviour for publication on plattform (create two paitents with conf code (restricted accessible)	and secret
 - change metadata of existing documents (2.223)
 - replace documents

TCU tested with Ludovic, works with caveats to also adapt STS response and add start-info

- 7.1 Query entries
- 7.2 Add an entry
- 7.3 Modify an entry
- 7.4 Delete an entry

  All HPD transactions have been tested



  IdP integration
  ===============

  http header integration for Idp Token?

   or [IKIT-httpheader](requests/sts-idp-httpheader-eprik.http)