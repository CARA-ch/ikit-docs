### migration to emedo platform

to migrate to the emedo platform from the existing integration platform the following new points have to be taken into considerations:

1. Two new test patients are available for validation [link](testpatients)
2. use new client certificates and adapt endpoints [config](ikit-config/)
3. configure your new patient assigning authority source oid with CARA
4. configure your IdP (e.g. HIN SAML NameID) with CARA for document access

You can download the [IKIT.postman_collection.json](../assets/IKIT.postman_collection.json) for example requests.

Please note a few different platform behaviours:

#### PDQ V3 ITI-47 
If more than 5 results are available, the result with a success message will contain the first five results  and 
indicate with a reasonOf/detectedIssueEvent entry that more specific search criteria should be specified. The existing platform had an en error message with acceptAckCode code set to NE. [example](https://ikit.cara.ch/dep/#/transaction/3fb82e89-4a8e-41a6-97e2-19563f963bc2)

#### STS XUA token response for XDS calls

The namespace declarations for xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' and xmlns:s='http://www.w3.org/2001/XMLSchema' are in the outer xml block in the response, meaning that if you extract the saml:Assertion by text it will be invalid xml without the above namespaces declared (this might not be the case if you reuse it directly). Verify for follow up requests that you have xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:s='http://www.w3.org/2001/XMLSchema' declared before.
[example](https://ikit.cara.ch/dep/#/transaction/d95ed4e6-2e75-4926-b43b-129deb3c9b3d). 

In addition the display names for the coded claims have to be provided, otherwise a follow up usage of the token can fail (open issue EPR-1404: SAML token validation failure: saml2:Assertion/saml2:AttributeStatement/saml2:Attribute[@Name='urn:oasis:names:tc:xspa:1.0:subject:purposeofuse']/saml2:AttributeValue/PurposeOfUse@displayName attribute required)

#### XDS

Ensure that start-info is in the http content-type header: (e.g. content-type: multipart/related; boundary=uuid:71766996-d9d7-484d-868d-8658c0c85d9a;type="application/xop+xml";start-info="application/soap+xml; charset=utf-8"), [example request](https://ikit.cara.ch/dep/#/transaction/58e93b31-0539-4ddf-b8e9-814076a7ec59)
[example](https://ikit.cara.ch/dep/#/transaction/d95ed4e6-2e75-4926-b43b-129deb3c9b3d)

#### HPD queries

HPD queries need to have scope="wholeSubtree", singleLevel does not work.

#### XDS: ITI-18/43 Requests to Initiating Gateway sufficient (no Document Registry / Repository calls necessary)

An ITI-18 Query to the Initiating Gateway will return all document entries in all communities including document entries in the community of the Initiating Gateway. This means a separate request to the ITI-18 registry is not necessary, or otherwise duplicates would need to be filtered out. Equivalent an ITI-43 retrieve to the Initiating Gateway can handle also document retrieve within the own community, not only for the external communities. 