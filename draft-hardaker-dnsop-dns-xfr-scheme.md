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

normative:
  RFC8976:
  BCP237:
  RFC8499:
  RFC4033:
  RFC8198:
  RFC5936:
  RFC9103:

informative:
  RFC5936:  # DNS Zone Transfer
  RFC7766:  # DNS Transport over TCP
  RFC9156:  # QNAME Minimisation
  RFC9110:  # HTTP Semantics

--- abstract

The DNS protocol provides an in-band mechanism for transferring the
contents of a zone from a server to a client.  This is most frequently
used when secondary servers are transferring the DNS zone content from
their configured primary server.

This document defines a URI scheme for use when referencing DNS
servers that a zone can be transferred from.

--- middle

# Introduction

The DNS protocol provides an in-band mechanism for transferring the
contents of a zone from a server to a client.  This is most frequently
used when secondary servers are transferring the DNS zone content from
their configured primary server.

This document defines a URI scheme for use when referencing DNS
servers that a zone can be transferred from.

Current DNS transfer protocols exist in three fundamental forms:
Authoratative Transfers (AXFR) {{RFC5936}}, Incremental Zone Transfers
(IXFR) {{RFC5936}} and XFR over TLS (XoT) {{RFC9103}}.  This document
defines URI schemes for all three of these DNS transfer protocols.

# Conventions and Definitions {#definitions}

{::boilerplate bcp14-tagged}

# Operational Considerations

TBD

# Security Considerations

TBD

# IANA Considerations

TBD

--- back

# Acknowledgments
{:numbered="false"}

TBD

