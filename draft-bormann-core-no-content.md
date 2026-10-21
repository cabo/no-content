---
title: >
  CoAP: The "No Content" Success Response Code
abbrev: >
  "No Content" Response Code
category: std

docname: draft-bormann-core-no-content-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Web and Internet Transport"
workgroup: "Constrained RESTful Environments"
keyword:
 - TODO
venue:
  mail: "core@ietf.org"
  github: "cabo/no-content"

author:
- name: Carsten Bormann
  org: Universität Bremen TZI
  street: Postfach 330440
  city: Bremen
  code: D-28359
  country: Germany
  phone: +49-421-218-63921
  email: cabo@tzi.org

normative:
  RFC7252: coap

informative:
  RFC7641: observe

...

--- abstract

Resources on a CoAP server may go through periods when the resource
itself already is established but does not yet (or for a period of
later) provide a representation of the intended type, e.g., during
initialization or when previous content becomes stale.
Responding to requests with an error response code such as 4.04 makes
it impossible for clients to sustain an RFC 7641 observation of the
resource and get notified when these periods end.

This document defines a new successful response code, 2.xx No Content,
that can be used by the server during these periods to allow the
client to sustain an observation interest.

--- middle

# Introduction {#intro}

TODO Introduction (please see abstract)

## Conventions and Definitions

{::boilerplate bcp14-tagged-bcp14}


## Discussion

Some media types might provide one or more representations that have semantics related to the No Content responder se code, e.g., empty (or explicitly null or undefined) values.
The specifics are dependent on the media type and may be hard to retrofit to existing media types.

The server might also send a different media type to indicate absence of content in a response; this would howver conflict with an Accept option in the request.
(The present specification could attempt to introduce such a “null media type” and modify the semantics of Accept to allow the server sending it in any response or notification.)
RFC 8710 could be used to encapsulate a choice between a media type indicating the “No Content” state and the intended media type for full responses into a single instance of the application/multipart-core media type, but that would essentially neuter the Accept request option.

### Interaction with other CoAP Options

TO DO: Etag, …

### Transition

TO DO: Describe how the new response code can be incrementally introduced on clients, servers, and proxies.


# Security Considerations {#security}

TODO Security


# IANA Considerations {#iana}

IANA is requested to register a response code in the CoAP Response
Codes registry in {{?IANA.core-parameters}}.

   o  The methods the Response Code applies to.

   o  Whether payload is required, optional, or not allowed.

   o  The semantics of the payload.  For example, the payload of a 2.05
      (Content) response is a representation of the target resource; the
      payload in an error response is a human-readable diagnostic
      payload.

   o  The format of the payload.  For example, the format in a 2.05
      (Content) response is indicated by the Content-Format Option; the
      format of the payload in an error response is always Net-Unicode
      text.

   o  Whether the response is cacheable according to the freshness
      model.

   o  Whether the response is validatable according to the validation
      model.

   o  Whether the response causes a cache to mark responses stored for
      the request URI as not fresh.

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
