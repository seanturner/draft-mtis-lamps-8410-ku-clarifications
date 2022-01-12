---
title: Clarifications for Ed25519, Ed448, X25519, and X448 Algorithm Identifiers
abbrev: curve25519, curve448 ECC Clarifications
category: std
updates: 8410

docname: draft-mtis-lamps-8410-ku-clarifications-latest
ipr: trust200902
keyword: Internet-Draft
area: Security
workgroup:
venue:
  github: seanturner/draft-mtis-lamps-8410-ku-clarifications

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs, docmapping]

author:
 -
    ins: S. Turner
    name: Sean Turner
    organization: sn3rd
    email: sean@sn3rd.com
 -
    ins: S. Josefsson
    name: Simon Josefsson
    organization: SJD AB
    email: simon@josefsson.org
 -
    ins: D. McCarney
    name: Daniel McCarney
    organization: Square Inc.
    email: daniel@binaryparadox.net
 -
    ins: T. Ito
    name: Tadahiko Ito
    organization: SECOM CO., LTD.
    email: tadahiko.ito.public@gmail.com

normative:

informative:
    ERRATA:
      title: Errata 5696
      author:
        -
          ins: L. Liao
          name: Lijun Liao
      date: 2019-04-17
      target: https://www.rfc-editor.org/errata/eid5696

--- abstract

This document updates RFC 8410 to clarify existing and specify
missing semantics for key usage bits when used in certificates
that support the Ed25519, Ed448, X25519, and X448 Elliptic Curve
Cryptography algorithms.

--- middle

# Introduction

{{!RFC8410}} specifies the syntax and semantics for the Subject Public
Key Information field in certificates that support Ed25519, Ed448,
X25519, and X448 Elliptic Curve Cryptography (ECC) algorithms.  As part
of these semantics, it defines what combinations are permissible for the
values of the key usage extension {{!RFC5280}}.  {{RFC8410}} did not
define what values are not permissible nor did it refer to
keyEncipherment or dataEncipherment. {{ERRATA}} has also been submitted
to clarify that keyCertSign is always set in certification authority
certificates. To address these changes, this document replaces Section 5
of {{RFC8410}} with {{replace}}.

# Terminology

{::boilerplate bcp14-tagged}

# New Section 5 for RFC 8410 {#replace}

The intended application for the key is indicated in the keyUsage
certificate extension.

If the keyUsage extension is present in a certificate that indicates
id-X25519 or id-X448 in SubjectPublicKeyInfo, then the following MUST
be present:

~~~
  keyAgreement;
~~~

one of the following MAY also be present:

~~~
  encipherOnly; or
  decipherOnly;
~~~

and the following MUST NOT be present:

~~~
  digitalSignature;
  nonRepudiation;
  keyEncipherment;
  dataEncipherment;
  keyCertSign; and
  cRLSign.
~~~

If the keyUsage extension is present in an end-entity certificate
that indicates id-Ed25519 or id-Ed448 in SubjectPublicKeyInfo, then
the keyUsage extension MUST contain one or both of the following:

~~~
  nonRepudiation; and
  digitalSignature;
~~~

the following MAY also be present:

~~~
  cRLSign;
~~~

~~~
and the following MUST NOT be present:

  keyEncipherment;
  dataEncipherment;
  keyAgreement;
  keyCertSign;
  encipherOnly; and
  decipherOnly.
~~~

If the keyUsage extension is present in a certification authority
certificate that indicates id-Ed25519 or id-Ed448 in
SubjectPublicKeyInfo, then the keyUsage extension MUST contain
keyCertSign, and zero, or more of the following:

~~~
  nonRepudiation;
  digitalSignature; and
  cRLSign;
~~~

and the following MUST NOT be present:

~~~
  keyEncipherment;
  dataEncipherment;
  keyAgreement;
  encipherOnly; and
  decipherOnly.
~~~

# Security Considerations

This document introduces no new security considerations beyond those
found in {{RFC8410}}.

# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
