TLS and Request Confidentiality
===============================

This document describes how to accomplish confidentiality of EWP HTTP requests
with the use of TLS transport.

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Introduction
------------

This is a pretty standard method of achieving HTTP request confidentiality. It
simply requires TLS (HTTPS) to be used. Is assumes that such requests cannot
be overheard, and **it doesn't apply any additional request body encryption**.


Implementing a server
---------------------

You MUST acquire a CA-signed certificate for your domain(s), and install it on
your servers. These are just the "regular" domain-validated certificates. You
MUST serve your API via HTTPS.


Implementing a client
---------------------

Not much more to describe here. You simply MUST make your requests via HTTPS
protocol.


Security considerations
-----------------------

### Main security questions

The [Authentication and Security][sec-intro] document
[requires][sec-method-rules] each request encryption method to explicitly
answer a couple of questions:

> How the server publishes his encryption key? How the client retrieves it
> securely?

The client uses HTTPS server certificate validation to make sure that it is
communicating with the proper party. It receives all required encryption keys
during the TLS handshake and trusts root CAs for the security of this exchange.

Note, that this only works when the clients can trust their CA certificate
stores.

> How to encrypt and decrypt the request? Which parts are covered by the
> encryption and which are not?

HTTPS does that on its own. All parts of the request are covered, including
all headers, and the request target (URL's path).


[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management/blob/stable-v1/README.md#statuses
[sec-intro]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro
[sec-method-rules]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro#rules
