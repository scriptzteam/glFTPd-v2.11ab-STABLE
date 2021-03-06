# glFTPd-v2.11ab-STABLE
Using Openssl 1.1.1k

Mar 31, 2021:  	glFTPd v2.11a(b) compiled against openssl-1.1.1k, fixing a security issue. 

OpenSSL Security Advisory [25 March 2021]
=========================================

CA certificate check bypass with X509_V_FLAG_X509_STRICT (CVE-2021-3450)
========================================================================

Severity: High

The X509_V_FLAG_X509_STRICT flag enables additional security checks of the
certificates present in a certificate chain. It is not set by default.

Starting from OpenSSL version 1.1.1h a check to disallow certificates in
the chain that have explicitly encoded elliptic curve parameters was added
as an additional strict check.

An error in the implementation of this check meant that the result of a
previous check to confirm that certificates in the chain are valid CA
certificates was overwritten. This effectively bypasses the check
that non-CA certificates must not be able to issue other certificates.

If a "purpose" has been configured then there is a subsequent opportunity
for checks that the certificate is a valid CA.  All of the named "purpose"
values implemented in libcrypto perform this check.  Therefore, where
a purpose is set the certificate chain will still be rejected even when the
strict flag has been used. A purpose is set by default in libssl client and
server certificate verification routines, but it can be overridden or
removed by an application.

In order to be affected, an application must explicitly set the
X509_V_FLAG_X509_STRICT verification flag and either not set a purpose
for the certificate verification or, in the case of TLS client or server
applications, override the default purpose.

OpenSSL versions 1.1.1h and newer are affected by this issue. Users of these
versions should upgrade to OpenSSL 1.1.1k.

OpenSSL 1.0.2 is not impacted by this issue.

This issue was reported to OpenSSL on 18th March 2021 by Benjamin Kaduk
from Akamai and was discovered by Xiang Ding and others at Akamai. The fix was
developed by Tom???? Mr??z.


NULL pointer deref in signature_algorithms processing (CVE-2021-3449)
=====================================================================

Severity: High

An OpenSSL TLS server may crash if sent a maliciously crafted renegotiation
ClientHello message from a client. If a TLSv1.2 renegotiation ClientHello omits
the signature_algorithms extension (where it was present in the initial
ClientHello), but includes a signature_algorithms_cert extension then a NULL
pointer dereference will result, leading to a crash and a denial of service
attack.

A server is only vulnerable if it has TLSv1.2 and renegotiation enabled (which
is the default configuration). OpenSSL TLS clients are not impacted by this
issue.

All OpenSSL 1.1.1 versions are affected by this issue. Users of these versions
should upgrade to OpenSSL 1.1.1k.

OpenSSL 1.0.2 is not impacted by this issue.

This issue was reported to OpenSSL on 17th March 2021 by Nokia. The fix was
developed by Peter K??stle and Samuel Sapalski from Nokia.

Note
====

OpenSSL 1.0.2 is out of support and no longer receiving public updates. Extended
support is available for premium support customers:
https://www.openssl.org/support/contracts.html

OpenSSL 1.1.0 is out of support and no longer receiving updates of any kind.
The impact of these issues on OpenSSL 1.1.0 has not been analysed.

Users of these versions should upgrade to OpenSSL 1.1.1.

References
==========

URL for this Security Advisory:
https://www.openssl.org/news/secadv/20210325.txt

Note: the online version of the advisory may be updated with additional details
over time.

For details of OpenSSL severity classifications please see:
https://www.openssl.org/policies/secpolicy.html
