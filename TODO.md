Platform testing todos
============

ahdis
=====

- ATNA: Connection does not yet work with openssl s_client -connect adapter.test.emedo.ch:20001 -cert mtls_caraikit_int.cer -key mtls_caraikit_int.key -CAfile emedo_EMO-SRV01_CA.pem (QL retries, see also index.hmtml


CARA Open issues
================

- Need to add DNS Entry for atna.ikit.cara.ch to IP 83.228.202.234)

BINT questions
==============


Major:
- Problem using STS Provider with [TCU](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)
- PIX V3 Feed process to add an organization into the facility registry and add the unknown assigning authority (see https://ikit.cara.ch/dep/#/transaction/9dd19e38-c691-4846-a826-6e14b24c5cb0):

Normal:
- Problem using STS Provider with [HIN](https://ikit.cara.ch/dep/#/transaction/18cf8487-927a-4b99-ab44-06beaf8541f8)
- Can we somewhere see the ATNA AuditEvents in the platform?

Minor:
- No Webservice CH:PPQ endpoint available ?
- No Webservice CH:ATC endpoint available? 
- No Webservice SVS endpoint available? 
- PDQ V3 behaviour more than 5 results (see below)

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




TCU issues (TCU cert from )

openssl x509 -in tcu.cer -text -noout
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            02:d9:16:e7:ef:9a:90:25:4e:da:fd:be:6d:cc:d1:10
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=US, O=DigiCert Inc., CN=DigiCert Private SSL SHA256 CA - G2
        Validity
            Not Before: May 23 00:00:00 2025 GMT
            Not After : May 23 23:59:59 2026 GMT
        Subject: C=CH, L=Epalinges, O=Association CARA, OU=2000010660018, CN=tcu_caraikit_int, emailAddress=integration@cara.ch
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (3072 bit)
                Modulus:
                    00:aa:39:bf:84:06:64:9f:49:39:b2:32:66:76:87:
                    70:b7:32:5c:37:2d:3d:b5:ab:01:ca:e1:eb:b2:3d:
                    8d:8e:4e:05:38:35:a5:00:b4:f9:c4:9b:d9:eb:fc:
                    b0:85:eb:0e:8a:21:e8:c1:ca:ae:bf:f0:c3:d6:ae:
                    25:40:dc:9a:5c:97:b3:26:c6:c7:54:1c:e3:17:21:
                    0f:ae:44:cc:97:43:63:06:2e:22:21:8d:f5:a1:55:
                    2d:05:cd:92:ae:d3:db:b4:34:80:19:d5:fb:6e:97:
                    58:bd:11:9a:ff:2b:b8:a0:91:9a:b0:ac:54:56:85:
                    a1:19:13:54:d2:db:2d:8a:1f:dc:5a:14:44:03:9e:
                    b7:9d:ee:07:62:e0:4c:fc:22:6d:fc:e5:98:62:81:
                    46:4b:29:8d:d6:6f:ff:88:05:b0:ea:8e:b3:0d:fd:
                    c0:0c:7f:a2:58:31:23:3c:51:93:2d:80:fd:4b:ee:
                    03:04:27:ce:82:3c:6a:08:52:19:f0:b4:e1:0f:7b:
                    cc:ba:ae:d6:81:b4:78:35:c2:30:5a:7a:15:a8:d2:
                    03:de:3e:c9:de:35:b7:92:f2:03:da:80:46:77:03:
                    65:fd:0e:19:8c:fc:9d:16:3a:e8:07:65:46:f1:15:
                    b4:8b:af:06:2a:da:5e:5e:7d:93:62:85:90:92:12:
                    70:1e:c4:0f:2a:05:b4:03:d5:66:7b:0e:4f:cf:79:
                    29:f3:a3:fe:e8:55:b9:94:2a:68:36:f4:13:5b:a1:
                    17:ac:a4:a4:08:64:a8:ed:65:e7:bf:70:4f:ef:89:
                    5d:06:d1:d2:53:e8:9a:77:34:f1:4c:6f:3a:5c:5d:
                    f1:44:73:12:df:be:31:2c:e5:6e:a9:6d:e5:cb:d4:
                    c2:35:3f:63:56:b0:e3:ee:1c:49:37:80:f2:2b:04:
                    59:86:0d:d5:86:fe:65:68:a3:15:b2:55:eb:53:1f:
                    91:ba:da:b2:b2:32:12:23:e1:9c:20:cc:6d:78:b5:
                    9f:f7:45:6a:7a:85:45:28:cc:95
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Authority Key Identifier:
                56:ED:86:14:09:7A:13:CD:DC:09:73:C3:03:F1:9D:B7:DA:76:2B:14
            X509v3 Subject Key Identifier:
                48:CF:74:FF:09:4D:A3:24:CF:6F:A9:62:8F:30:38:B7:AF:AC:82:DD
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Alternative Name:
                email:integration@cara.ch
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Client Authentication, E-mail Protection
            X509v3 Certificate Policies:
                Policy: 2.16.840.1.114412.4.1.2
                  CPS: https://www.digicert.com/CPS
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://crl3.digicert.com/DigiCertPrivateSSLSHA256CA-G2.crl

                Full Name:
                  URI:http://crl4.digicert.com/DigiCertPrivateSSLSHA256CA-G2.crl

            Authority Information Access:
                OCSP - URI:http://ocsp.digicert.com
                CA Issuers - URI:http://cacerts.digicert.com/DigiCertPrivateSSLSHA256CA-G2.crt
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        af:09:c5:78:db:1b:43:03:ea:79:b9:84:3c:79:e1:2b:75:8d:
        fd:5d:bc:c5:02:f9:43:9f:8c:1c:3a:ea:f1:c0:00:37:8d:f4:
        57:8d:6a:46:1e:19:7a:c3:1d:ec:da:76:99:5c:a6:86:51:12:
        55:8d:38:9f:9a:7c:1f:06:28:e3:1e:d6:83:52:62:c7:0d:c1:
        81:77:69:64:f3:de:3c:9a:b5:64:7c:52:32:55:47:4f:73:f4:
        fc:e0:45:39:08:b9:7d:af:bf:ec:2e:3d:96:ed:00:f7:9f:4a:
        f2:7b:0f:14:24:60:d3:7d:06:dd:f5:c7:b9:ad:01:5d:8a:2e:
        d7:29:95:0f:d5:dc:6b:a3:f2:89:0f:40:12:1b:d1:6c:c6:58:
        e0:ee:33:0a:35:5f:6f:2a:06:a6:0f:db:4d:0b:cd:db:3b:85:
        92:8e:f5:98:07:9a:13:71:8c:82:de:38:56:5a:76:02:f2:cf:
        4c:45:12:3d:f3:71:58:cd:e1:15:28:9a:b8:56:ec:9a:f1:7d:
        3a:db:f2:fd:19:fb:e9:97:67:9f:73:fa:ae:3b:a4:f4:23:81:
        23:46:ab:71:bc:73:08:d5:75:5b:ff:44:3c:7e:94:bf:70:c0:
        f8:cf:b2:18:08:66:b4:8c:61:ea:2a:05:f4:12:1a:e0:36:05:
        d3:0a:86:89