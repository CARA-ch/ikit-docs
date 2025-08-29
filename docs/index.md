# Primary system integration with CARA

!!! note

    28.08.2025 ikit.cara.ch for emedo: This release  documents the integration with the emedo platform and the documentation is in progress, 
    IdP integration needs manual configuration
    see [changelog](changelog.md)


This documentation describes how the [Integration Kit](https://ikit.cara.ch/dep/) can be used to test
the integration of a primary system with the [CARA](https://www.cara.ch/) integration system.

CARA offers different services:

- EPR [https://portal.test.emedo.ch](https://portal.test.emedo.ch/login)

To access the integration system you will need to sign a contract/CGUE with [CARA](https://www.cara.ch/) and provide

- an OID concept for your organization,
- define a OID for the patient assigning authority (needs to be configured manually by emedo/ofac)

in return you will get:

- an HCP test user for which you need an online authentication yourself (e.g. HIN ID) and connect that HCP test user
  with your online authentication
- two test patients for you with patient access, public test patients are listed [here](testpatients.md)

This will allow you to start the integration of the primary system.

The [Integration Kit](https://ikit.cara.ch/dep/) (short **IKIT**) provides the
following [functionality](usecases.md):

- Authenticate an User and obtain an IdP assertion or a TCU assertion
- Proxy and log IHE transactions without client certificates and with basic validation of request / response

<figure markdown>
  ![Image title](img/eprik-architecture.png){ width="499" }
  <figcaption>Integration architecture</figcaption>
</figure>

This allows a primary system to do a stepwise integration. The integration kit is only
an add-on during development, testing and **CANNOT BE** used with a production environment.

!!! danger

    Use only test data and no real patient data! IKIT is completely open 
    and every request / response to the integration system made is retrievable.

## Testing the TLS connection with CARA INT

There are two different TLS connections with CARA INT you can test: the Syslog connection (to send ATNA messages) 
and the webservices connection (to send IHE requests).

In these tests, you have to use your own certificate and private key.
Note that they may be stored in the same _[.pem](https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail)_ file.

### Syslog connection

You can test the Syslog connection with `openssl`:
```bash
openssl s_client -connect adapter.test.emedo.ch:7003 -cert mtls_caraikit_int.cer -key mtls_caraikit_int.key

Connecting to 194.209.244.46
CONNECTED(00000005)
... 

---
SSL handshake has read 7909 bytes and written 2704 bytes
Verification: OK
---
New, TLSv1.3, Cipher is TLS_AES_128_GCM_SHA256
Protocol: TLSv1.3
Server public key is 4096 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 0 (ok)
---

```


If the command returns, and/or the last output line is "_closed_", then the connection failed.
In case of error, you can increase the log levels with the parameters `-state -debug -msg -prexit`.

### Webservice connection

You can test the webservices connection with `curl`:
```bash
curl -v --cert cert.pem --key private_key.key  \
  -H "Content-Type: application/soap+xml;charset=UTF-8" \
  -d '' \
  https://adapter.test.emedo.ch/
```

In case of success, you will see the content of the "HTTP 404 - Not Found" page of EMEDO.
In case of error, you may see an error like "_curl: (56) OpenSSL SSL_read: error:14094410:SSL 
routines:ssl3_read_bytes:sslv3 alert handshake failure, errno 0_".
