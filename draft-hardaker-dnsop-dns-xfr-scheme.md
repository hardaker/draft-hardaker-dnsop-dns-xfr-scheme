---
###
# Internet-Draft Markdown Template
#
# Rename this file from draft-todo-yourname-protocol.md to get started.
# Draft name format is "draft-<yourname>-<workgroup>-<name>.md".
#
# For initial setup, you only need to edit the first block of fields.
# Only "title" needs to be changed; delete "abbrev" if your title is short.
# Any other content can be edited, but be careful not to introduce errors.
# Some fields will be set automatically during setup if they are unchanged.
#
# Don't include "-00" or "-latest" in the filename.
# Labels in the form draft-<yourname>-<workgroup>-<name>-latest are used by
# the tools to refer to the current version; see "docname" for example.
#
# This template uses kramdown-rfc: https://github.com/cabo/kramdown-rfc
# You can replace the entire file if you prefer a different format.
# Change the file extension to match the format (.xml for XML, etc...)
#
###
title: "The DNS XFR URI Schemes"
abbrev: "DNS XFR URI Schemes"
category: std

docname: draft-hardaker-dnsop-dns-xfr-scheme-latest
submissiontype: IETF
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Domain Name System Operations"
keyword:
 - DNS
 - DNSSEC
 - zone transfer
 - axfr
 - ixfr
venue:
  group: "Domain Name System Operations"
  type: "Working Group"
  mail: "dnsop@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/dnsop/"
  github: "https://github.com/hardaker/draft-hardaker-dnsop-dns-xfr-scheme"
  latest: "https://github.io/hardker/draft-hardaker-dnsop-dns-xfr-scheme/draft-hardaker-dnsop-dns-xfr-scheme.html"

author:
  -
    fullname: Wes Hardaker
    organization: Google, Inc.
    email: ietf@hardakers.net
  -
    fullname: Warren Kumari
    organization: Google, Inc.
    email: warren@kumari.net

normative:
  RFC3986:
  RFC4395:
  RFC5234:
  RFC5936:  # DNS Zone Transfer
  RFC8499:
  RFC9103:

informative:
  RFC7766:  # DNS Transport over TCP

--- abstract

The DNS protocol provides an in-band mechanism for transferring the
contents of a zone from a server to a client.  This is most frequently
used when secondary servers are transferring the DNS zone content from
their configured primary server.

This document defines a Uniform Resource Identifier (URI) scheme for
referencing DNS servers from which DNS zone contents can be transferred.

--- middle

# Introduction

The DNS protocol provides an in-band mechanism for transferring the
contents of a zone from a server to a client.  This is most frequently
used when secondary servers are transferring the DNS zone content from
their configured primary server.

This document defines a Uniform Resource Identifier (URI) {{RFC3986}} scheme for
referencing DNS servers from which DNS zone contents can be transferred.

# Conventions and Definitions {#definitions}

{::boilerplate bcp14-tagged}

# Syntax of a DNS Transfer Protocol URI {#syntax}

Current DNS transfer protocols exist in three fundamental forms:
Authoratative Transfers (AXFR) {{RFC5936}}, Incremental Zone Transfers
(IXFR) {{RFC5936}} and XFR over TLS (XoT) {{RFC9103}}.  This document
defines URI schemes for all three of these DNS transfer protocols.

This document uses the Augmented Backus-Naur Form (ABNF) of
{{RFC5234}}.

~~~
    xfr-URI = scheme ":" host [ ":" port ] "/" zone

    scheme = "axfr" / "ixfr" / "xot"

    zone = TBD
~~~

host and port are specified in {{RFC3986}}.

The 'scheme' signifies which DNS zone transfer protocol should be used
(AXFR {{RFC5936}}, IXFR {{RFC5936}} or XoT {{RFC9103}}).  While these
two ABNF productions are defined in [RFC3986] as components of the
generic hierarchical URI, this does not imply that the "axfr", "ixfr"
and "xot" URI schemes are hierarchical URIs.  Developers MUST NOT use
a generic hierarchical URI parser to parse a "axfr", "ixfr" or "xot" URI.


# URI Scheme Semantics {#semantics}

The "axfr", "ixfr" or "xot" URI schemes are used to refer to a DNS
server that offers zone transfer support.  These three protocols each
specify the details of how transfers are performed within their
respective specifications and are beyond the scope of this document.

The required 'host' part of the xfr URI denotes the DNS server host.

As specified in each transfer protocols specifications, the 'port'
part, if present, denotes the port on which the DNS server is awaiting
requests.  If absent for the axfr and ixfr transfer protocols, this
SHOULD be TCP port 53.  If absent for the xot transfer protocol, the
default port SHOULD be TCP port 853.

The 'zone' signifies the zone to be transferred and MUST be a fully
qualified domain name.  Note that 'zone' MAY be "." to refer to the
DNS root zone.  When not referring to the root zone, the 'zone' SHOULD
have a trailing "." (for example "zone.example.").

# Security Considerations {#security}

The "axfr", "ixfr" or "xot" URI schemes do not introduce new security
considerations beyond what is specified in their respective RFCs (AXFR
{{RFC5936}}, IXFR {{RFC5936}} or XoT {{RFC9103}}).  These schemes are
intended for use in documentation and configuration files that refer
to servers offering DNS zone transfers.  Documentation and
configuration files should carefully consider which protocol is most
suitable for use, and if possible the "xot" protocol should be
preferred if privacy or integrity of the zone contents are a concern.

# IANA Considerations

This section contains the registration information for the "axfr",
"ixfr" or "xot" URI schemes (in accordance with {{RFC4395}}).

## "axfr" URI Registration

URI scheme name: axfr

Status: permanent

URI scheme syntax: See Section {{syntax}}

URI scheme semantics: See Section {{semantics}}

Encoding considerations: There are no encoding considerations beyond
those in {{RFC3986}}.

Applications/protocols that use this URI scheme name:

   The "axfr" URI scheme is intended to be used by applications with
   a need to identify a DNS server supporting authoritative transfer
   over DNS using the AXFR protocol for a zone.

Interoperability considerations: N/A

Security considerations: See Section {{security}}

Contact: Wes Hardaker <ietf@hardakers.net>

## "ixfr" URI Registration

URI scheme name: ixfr

Status: permanent

URI scheme syntax: See Section {{syntax}}

URI scheme semantics: See Section {{semantics}}

Encoding considerations: There are no encoding considerations beyond
those in {{RFC3986}}.

Applications/protocols that use this URI scheme name:

   The "ixfr" URI scheme is intended to be used by applications with
   a need to identify a DNS server supporting authoritative transfer
   over DNS using the IXFR protocol for a zone.

Interoperability considerations: N/A

Security considerations: See Section {{security}}

Contact: Wes Hardaker <ietf@hardakers.net>

## "xot" URI Registration

URI scheme name: xot

Status: permanent

URI scheme syntax: See Section {{syntax}}

URI scheme semantics: See Section {{semantics}}

Encoding considerations: There are no encoding considerations beyond
those in {{RFC3986}}.

Applications/protocols that use this URI scheme name:

   The "xot" URI scheme is intended to be used by applications with
   a need to identify a DNS server supporting authoritative transfer
   over DNS using the XoT protocol for a zone.

Interoperability considerations: N/A

Security considerations: See Section {{security}}

Contact: Wes Hardaker <ietf@hardakers.net>

--- back

# Acknowledgments
{:numbered="false"}

# Examples
{:numbered="false"}

The following are example XFR URIs specifying an 'axfr' URI for the
DNS root zone, an 'ixfr' URI for example.com, and a 'xot' URI for
zone.example on port 8853:

- axfr:b.root-servers.net/.
- ixfr:ns.example.com/example.com.
- xot:ns.zone.example:8853/zone.example.


