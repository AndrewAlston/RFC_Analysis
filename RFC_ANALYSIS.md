# RFC analysis: contradictions, ambiguities and possible errata {#rfc_analysis}

A review of 407 RFCs (with a note on a few related registry and NIST texts) covering BGP, IS-IS, MPLS, LDP, RSVP-TE, PCEP, PIM, BFD, pseudowires, measurement protocols and supporting IP and security specifications. Each finding names the RFC and section, quotes the text briefly, explains the contradiction, ambiguity or error, and gives the status of any existing erratum. Findings that look like errata not yet reported carry a proposed report in the RFC Editor's format (Original Text, Corrected Text, Notes). Prepared 2026-11-09.

## Summary {#ra_summary}

109 findings in 54 RFCs; 77 match an existing erratum report; **16 are proposed new errata**. 61 RFCs were read in depth or in part; the other 346 were covered by mechanical checks only (see [Method and limits](#ra_method)).

### Counts by severity {#ra_counts_sev}

| Severity | Findings | Existing erratum | Proposed erratum |
|---|---|---|---|
| error | 30 | 25 | 5 |
| contradiction | 12 | 7 | 4 |
| ambiguity | 34 | 19 | 3 |
| editorial | 33 | 26 | 4 |
| **total** | **109** | **77** | **16** |

"error" includes security gaps (marked "Security gap"). "Existing erratum" counts findings that match an erratum report of any status, including rejected reports that leave a question open.

### Counts by area {#ra_counts_area}

| Area | RFCs | Read in depth or in part | Findings | Proposed errata | error | contradiction | ambiguity | editorial |
|---|---|---|---|---|---|---|---|---|
| [BGP, L3VPN, MVPN and BGP-LS](#ra_bgp) | 72 | 10 | 32 | 3 | 5 | 4 | 16 | 7 |
| [IS-IS, IGP TE, Segment Routing and IP FRR](#ra_isis) | 62 | 9 | 12 | 4 | 2 | 2 | 3 | 5 |
| [MPLS, LDP and mLDP](#ra_ldp) | 44 | 7 | 9 | 2 | 1 | 0 | 4 | 4 |
| [Pseudowires, VPLS and ICCP](#ra_pw) | 20 | 5 | 6 | 1 | 3 | 0 | 2 | 1 |
| [RSVP, RSVP-TE and GMPLS](#ra_rsvp) | 44 | 7 | 12 | 0 | 5 | 1 | 1 | 5 |
| [PCEP and PCE](#ra_pcep) | 36 | 6 | 12 | 3 | 3 | 3 | 3 | 3 |
| [Multicast: PIM, IGMP, MLD and MVPN](#ra_mcast) | 22 | 4 | 6 | 1 | 2 | 1 | 0 | 3 |
| [BFD, LSP ping, measurement and time](#ra_oam) | 30 | 8 | 10 | 2 | 4 | 0 | 4 | 2 |
| [IP, ICMP, neighbour discovery, transport and security](#ra_ip) | 77 | 5 | 10 | 0 | 5 | 1 | 1 | 3 |

### Proposed errata {#ra_proposed}

| ID | RFC, section | Type | Summary |
|---|---|---|---|
| [RA-0007](#ra_rfc4271) | RFC 4271 5 (vs RFC 7606 5.1) | Technical | Ascending attribute order conflicts with RFC 7606 5.1 (MP_REACH / MP_UNREACH first). |
| [RA-0016](#ra_rfc4724) | RFC 4724 4.2 | Technical | Clarify which stale routes are deleted on a consecutive restart, and when. |
| [RA-0026](#ra_rfc7606) | RFC 7606 4 | Technical | The zero-length rule cannot be applied to unrecognized attributes. |
| [RA-0036](#ra_rfc5120) | RFC 5120 7.1 | Technical | MT #0 is required of every MT router; "has to" is not a keyword; the 127-MT limit is per TLV. |
| [RA-0037](#ra_rfc5305) | RFC 5305 3, 4 | Technical | Path metric clamp at MAX_PATH_METRIC conflicts with ISO 10589 "unreachable" semantics. |
| [RA-0038](#ra_rfc5305) | RFC 5305 4 | Editorial | Typo "then"; nonexistent "paragraph 3.0". |
| [RA-0041](#ra_rfc5310) | RFC 5310 3.3 | Technical | Key preparation differs from RFC 2104 for L < key length <= B; Ko / Ipad length mismatch; SHA-224 block size missing. |
| [RA-0048](#ra_rfc3212) | RFC 3212 3.4 | Technical | Reference to nonexistent Section 4.11 (status codes are in 5.3). |
| [RA-0052](#ra_rfc5036) | RFC 5036 3.5.11 (and the other message figures) | Editorial | Message Type / Message Length boundary drawn one bit early in the message figures. |
| [RA-0060](#ra_rfc8338) | RFC 8338 3.2.1 | Technical | Reference to nonexistent Section 2.3 (typed wildcard FEC is 3.3). |
| [RA-0073](#ra_rfc5088) | RFC 5088 7.2 | Editorial | Reference to nonexistent Section 4.1.5 (PCE-CAP-FLAGS is 4.5). |
| [RA-0078](#ra_rfc8231) | RFC 8231 7.3.2, 7.3.4 | Technical | Erratum 6289 also applies to 7.3.4: TLV Length is the value length. |
| [RA-0084](#ra_rfc8664) | RFC 8664 4.3.1 vs 5.2.1 | Technical | NT "MUST be ignored" (even as corrected by 6753) conflicts with the validation rules of 5.2.1. |
| [RA-0085](#ra_rfc2236) | RFC 2236 2, 3 | Technical | References to sections 1.4, 7.3 and 7.8 should be 2.4, 8.3 and 8.8. |
| [RA-0098](#ra_rfc6038) | RFC 6038 4.3 | Editorial | Reference to nonexistent Section 4.1.2. |
| [RA-0099](#ra_rfc6426) | RFC 6426 7.2 | Technical | IANA table cites nonexistent Sections 2.4.1 / 2.4.2 (should be 2.3.1 / 2.3.2). |

### Most significant findings {#ra_significant}

Contradictions and errors with interoperability impact, whether or not an erratum exists:

- [RA-0077](#ra_rfc8231) RFC 8231 8.5 (Error-Type 19 value 1, Error-Type 20 value 1): The IANA text for PCErr 19/1 and 20/1 puts an LSP object in a message whose grammar has no place for it (verified errata 5970, 6231).
- [RA-0016](#ra_rfc4724) RFC 4724 4.2: "A route previously marked as stale MUST be deleted" on consecutive restarts is easy to misread; implementations keep or flush different sets of routes.
- [RA-0089](#ra_rfc7761) RFC 7761 4.4.2, 4.11: The RP's Keepalive Timer after a Register-Stop differs between the pseudocode and the text by 25 s with default timers (verified erratum 5342).
- [RA-0037](#ra_rfc5305) RFC 5305 3, 4: Clamping path metrics at MAX_PATH_METRIC contradicts ISO 10589's "unreachable above MaxPathMetric".
- [RA-0041](#ra_rfc5310) RFC 5310 3.3: Key preparation differs from RFC 2104 HMAC for keys longer than the digest but not longer than the block size, so such keys do not interoperate between implementations.
- [RA-0007](#ra_rfc4271) RFC 4271 5 (vs RFC 7606 5.1): Two encoding rules for path attribute order that a sender cannot both satisfy.
- [RA-0084](#ra_rfc8664) RFC 8664 4.3.1 vs 5.2.1: Even with erratum 6753, the NT field is "ignored" in one section and validated in another.
- [RA-0093](#ra_rfc5880) RFC 5880 6.7.3, 6.7.4: Authentication sequence state updated before the digest check (verified errata 7082, 7083): a security gap in implementations that follow the original text.
- [RA-0071](#ra_rfc4875) RFC 4875 8.2: Two paragraphs give different RESV_CONFIRM rules for a merging transit LSR (erratum 2485, held).
- [RA-0036](#ra_rfc5120) RFC 5120 7.1: Every multi-topology router is required to be in MT #0, which excludes routers that run only another topology (for example IPv6 only, MT #2).
- [RA-0078](#ra_rfc8231) RFC 8231 7.3.2, 7.3.4: The TLV Length error fixed by erratum 6289 in 7.3.2 remains in 7.3.4.
- [RA-0105](#ra_rfc4861) RFC 4861 6.2.1: The default MinRtrAdvInterval violates the MUST in the same definition for small MaxRtrAdvInterval (verified erratum 3154).

## Method and limits {#ra_method}

**Scope.** 407 RFC texts, grouped into nine areas. The texts were taken as published (plain-text RFCs);
errata were not applied to them. A few related texts (IANA registries for PCEP, RSVP and RSVP-TE, one
Internet-Draft and NIST SP 800-38D) were used as references only and are not analysed.

**Mechanical checks, all 407 RFCs.** Every text was scanned by script for: references to sections that
do not exist in the same document (section headings and table-of-contents entries compared with every
"Section N.N" reference not attributed to another document); mixed-case or non-RFC 2119 keyword forms
("MAY NOT", "MUST not", "SHOULD not"); leftover placeholders ("TBD", "TBA", "XXX"); and packet diagrams
whose field boundaries do not fall on bit boundaries. Each hit was then read in context; most were
false positives (references to other documents split across lines, bit-ruler artefacts). The confirmed
ones are listed as findings. Mixed-case or non-keyword forms occur in 23 RFCs (RFC 1191, 1812, 2212, 3212, 3473, 3479, 3719,
3787, 4090, 4105, 4271, 4446, 4447, 4448, 4656, 4875, 5130, 5305, 5308, 5357, 8338, 8439, 9350); they are
listed once (RFC 1191) unless the case changes the meaning, which is so only for "MAY NOT" in RFC 4271.

**Targeted reading, 56 RFCs.** The protocol cores and their most-used extensions were read in the
sections where implementers have to make choices: state machines, error handling, timers and
constants, encodings and their figures, IANA tables, and the interaction with the RFCs they update or
are updated by. "Deep" and "part" in the index mean this kind of targeted reading, not a complete line-by-line
review; no RFC over a few hundred lines was read end to end. Long background documents
(frameworks, requirements, informational, HTTP, QUIC, TLS, X.509, hash and cipher specifications)
were covered by the mechanical checks only.

**Errata.** The RFC Editor errata pages were consulted for 43 RFCs, plus RFC 3107 and RFC 7810 (predecessors
of RFC 8277 and RFC 8570); for 9 more a search found no errata page. Pages were read one by one (no
bulk export was reachable), and each erratum is recorded with id, status and type. For the other RFCs the entry says "errata not
checked", or "no errata page in search results" where a search found none. Existing errata are cited
by id; a finding that matches a rejected report is still listed when the question it raised remains
open in the text. Proposed errata are new reports in the RFC Editor's format; they have not been
filed, and several are clarifications that would normally be "Held for Document Update".

**Limits.** Quotes are kept to one or two lines and may be abridged with "..."; line breaks are
removed. Findings come from reading, not from testing implementations. A finding marked "ambiguity"
means the text supports more than one reasonable reading, not that implementations are known to
differ, unless the issue text says so. Absence of a finding for an RFC means that nothing was found by
the depth of review stated, not that the RFC is free of problems.

## BGP, L3VPN, MVPN and BGP-LS {#ra_bgp}

72 RFCs in this area; 32 findings, 3 of them proposed errata.

### RFC 4271: A Border Gateway Protocol 4 (BGP-4) {#ra_rfc4271}

Reading: targeted reading of the relevant sections. Errata: errata checked: 21 (9 verified, 7 held, 5 rejected, 0 open). Obsoletes: RFC 1771.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0001 | 6.3 | "If an error is detected, the attribute MUST be discarded, and the Error Subcode MUST be set to Optional Attribute Error." | Discarding the attribute and sending a NOTIFICATION (which closes the session) are given together; the discard is meaningless once the session ends. RFC 7606 replaces this rule for most attributes, so the text only still governs attributes whose own specification does not name an error-handling approach. | contradiction | 1633 (Verified) |
| RA-0002 | 9.1.1 | "If the return value indicates the route is ineligible, the route MAY NOT serve as an input to the next phase" | "MAY NOT" is not an RFC 2119 keyword; read literally it permits an ineligible route to be used. The errata read it as MUST NOT, which is the only coherent reading. | ambiguity | 5000, 4496 (Held) |
| RA-0003 | 5 | "Others are discretionary and MAY or MAY NOT be sent in a particular UPDATE message." | Same non-keyword "MAY NOT"; here the intent is plain lower-case "may not". | editorial | 5001 (Held) |
| RA-0004 | 8.2.2 | "If the HoldTimer_Expires event occurs (Event 10), the local system: - sends a NOTIFICATION message with the Error Code Hold Timer Expired," | The Established-state action list for HoldTimer_Expires omits "deletes all routes associated with this connection", which every other session-ending event in Established lists. An implementation transcribing the table would keep the peer's routes. | error | 2838 (Verified) |
| RA-0005 | 4.5, 6.1-6.3 | "Message Header Error subcodes: 1 - Connection Not Synchronized. 2 - Bad Message Length. 3 - Bad Message Type." | The subcode lists start at 1; the erratum adds subcode 0 ("Unspecific") to the Header, OPEN and UPDATE lists. Receivers must accept subcode 0 rather than treat it as an unknown subcode. | ambiguity | 4493 (Verified) |
| RA-0006 | 8.2.2 | "- remains in the OpenConfirmed state." | There is no state "OpenConfirmed"; the state is OpenConfirm. | editorial | 5421 (Held) |
| RA-0007 | 5 (vs RFC 7606 5.1) | "The sender of an UPDATE message SHOULD order path attributes within the UPDATE message in ascending order of attribute type." | RFC 7606 5.1 (which updates RFC 4271) says MP_REACH_NLRI / MP_UNREACH_NLRI (types 14 / 15) "SHALL be encoded as the very first path attribute", which breaks ascending order for every UPDATE that carries ORIGIN (1), AS_PATH (2) and so on. A sender cannot satisfy both; RFC 7606, being later and more specific, should win, but RFC 4271 is not marked as changed on this point. | contradiction | none; **proposed erratum below** |
| RA-0008 | 8.2.2 (OpenSent, event 25) | "In response to any other event (Events 9, 11-13, 20, 25-28), the local system: - sends the NOTIFICATION with the Error Code Finite State Machine Error," | Taken literally, a received NOTIFICATION (event 25) in some states is answered with a NOTIFICATION, against sections 6 and 6.4 and RFC 6608. | contradiction | none |
| RA-0009 | 9.2.2.2 | "Routes that have different MULTI_EXIT_DISC attributes SHALL NOT be aggregated." | The aggregation rules cover only ORIGIN, AS_PATH, NEXT_HOP, MED, ATOMIC_AGGREGATE and AGGREGATOR; nothing says what to do with communities, LOCAL_PREF or later attributes, or which MED to keep when aggregation is forced by configuration. | ambiguity | none |
| RA-0010 | 9.1.2.1 | "BGP speakers SHOULD exclude unresolvable routes from the Phase 2 decision." | "Resolvable" is defined recursively against the Routing Table without saying whether BGP routes may resolve BGP next hops or what happens when the resolving route changes. | ambiguity | none |
| RA-0011 | 6.3 | "If the NEXT_HOP attribute is semantically incorrect, the error SHOULD be logged, and the route SHOULD be ignored." | "Ignored" does not say whether a previously stored path for the same prefix from that peer is kept or removed. | ambiguity | none |

Proposed erratum RA-0007 (RFC 4271, Section 5 (vs RFC 7606 5.1); type: Technical):

```
Original Text
-------------
   The sender of an UPDATE message SHOULD order path attributes
   within the UPDATE message in ascending order of attribute type.

Corrected Text
--------------
   The sender of an UPDATE message SHOULD order path attributes
   within the UPDATE message in ascending order of attribute type,
   except that the MP_REACH_NLRI or MP_UNREACH_NLRI attribute, if
   present, is encoded first (see RFC 7606, Section 5.1).

Notes
-----
   RFC 7606 Section 5.1 (which updates this document) requires
   MP_REACH_NLRI
   MP_UNREACH_NLRI to be the very first path attribute, which
   conflicts with ascending order whenever lower-numbered attributes
   are present. Suggested as Held for Document Update for a future
   revision of RFC 4271.
```

### RFC 4364: BGP/MPLS IP Virtual Private Networks (VPNs) {#ra_rfc4364}

Reading: targeted reading of the relevant sections. Errata: errata checked: 9 records (1 verified editorial, 7 held, 2 rejected; none technical in substance). Obsoletes: RFC 2547.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0012 | 4.3.4 | "... unlabeled VPN-IPv4 addresses ..." | VPN-IPv4 routes are always labelled (SAFI 128); "unlabeled IPv4 addresses" is meant. | editorial | 7180 (Held) |
| RA-0013 | 4.3.2 | "... is encoded as a VPN-IPv4 address with an RD of 0" | Receipt of a next hop with a non-zero RD is not covered. | ambiguity | none |

### RFC 4456: BGP Route Reflection: An Alternative to Full Mesh Internal BGP (IBGP) {#ra_rfc4456}

Reading: targeted reading of the relevant sections. Errata: errata checked: 2 (1 held editorial, 1 rejected technical question). Obsoletes: RFC 2796, RFC 1966.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0014 | 8 | "When an RR reflects a route, it MUST prepend the local CLUSTER_ID to the CLUSTER_LIST." | The RFC does not say what a receiver does with an IBGP route that carries ORIGINATOR_ID without CLUSTER_LIST, or CLUSTER_LIST without ORIGINATOR_ID (only a reflector could have added either). The erratum asking this was rejected as a question for the working group, so it stays open. RFC 7606 7.9 / 7.10 only cover malformed lengths. | ambiguity | 3898 (Rejected, question) |
| RA-0015 | 5 | "The Non-Client peer must be fully meshed" | Plural intended ("Non-Client peers"). | editorial | 3778 (Held) |

### RFC 4724: Graceful Restart Mechanism for BGP {#ra_rfc4724}

Reading: targeted reading of the relevant sections. Errata: errata checked: 3 (1 reported technical, 1 held technical, 1 held editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0016 | 4.2 | "To deal with possible consecutive restarts, a route (from the peer) previously marked as stale MUST be deleted." | The sentence means that when the session fails again before the peer re-advertised a route, routes still stale from the previous restart are deleted, not re-marked. "Consecutive restarts" is not defined (before End-of-RIB? within the Restart Time?). | ambiguity | none; **proposed erratum below** |
| RA-0017 | 4.2, 5 | "See Section 8 for a description of this behavior in terms of the BGP finite state machine." | Section 8 is the Security Considerations; the FSM changes are in section 5. The reported erratum adds that the RFC changes the RFC 4271 FSM and should have been marked "Updates: 4271". | error | 7915 (Reported), 4193 (Held) |
| RA-0018 | 4.2 | "To put an upper bound on the amount of time a router retains the stale routes, an implementation MAY support a (configurable) timer" | Without that timer a peer that reconnects but never sends End-of-RIB keeps stale routes forever; the RFC sets no default. | ambiguity | none |
| RA-0019 | 7 | "Since with this proposal a new connection can cause an old one to be terminated, it might seem to open the door to denial of service" | Security gap: Section 7 discusses only the new-connection case. An on-path attacker can send a forged NOTIFICATION making the peer retry without the GR capability (RFC 5492 fallback), silently disabling graceful restart. The RFC does not mention it. | error | 6217 (Held) |

Proposed erratum RA-0016 (RFC 4724, Section 4.2; type: Technical):

```
Original Text
-------------
   To deal with possible consecutive restarts, a route (from the
   peer) previously marked as stale MUST be deleted.

Corrected Text
--------------
   To deal with possible consecutive restarts, a route (from the
   peer) that is still marked as stale from a previous restart (that
   is, it has not been re-advertised by the peer since that restart)
   MUST be deleted when the TCP session terminates again.

Notes
-----
   Clarification only. The original sentence does not say when the
   deletion happens or which routes are meant; it is easily read as
   "delete all stale routes" or as not applying until the Restart
   Time expires.
```

### RFC 4760: Multiprotocol Extensions for BGP-4 {#ra_rfc4760}

Reading: targeted reading of the relevant sections. Errata: errata checked: 5 (1 verified technical, 4 held editorial). Obsoletes: RFC 2858.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0020 | 4 | "(MP_UNREACH_NLRI, AFI:) identifies the set of Network Layer protocols to which the address carried in the Next Hop field must belong" | MP_UNREACH_NLRI has no Next Hop field; the AFI/SAFI only qualify the withdrawn routes. Copy-and-paste from section 3. | error | 1573 (Verified) |
| RA-0021 | 3 | "... the MP_NLRI attribute ..." | There is no "MP_NLRI" attribute; MP_REACH_NLRI (or its NLRI field) is meant. | editorial | 3848, 3849 (Held) |
| RA-0022 | 5 | "The Network Layer Reachability information is encoded as one or more 2-tuples of the form <length, prefix>" | The <length, prefix> encoding is written as if it applies to every SAFI; it applies only to SAFI 1 and 2. Labelled, VPN, MVPN, BGP-LS and SR Policy NLRI use their own encodings. | ambiguity | 5120 (Held) |
| RA-0023 | 7, 8 | "... the speaker MUST delete all the BGP routes received from that neighbor whose AFI/SAFI is the same as the one carried in the incorrect ... attribute." | Silent on an MP attribute for a family that was never negotiated, and offers two incompatible reactions (reset or "AFI/SAFI disable") for a malformed one. | ambiguity | none |

### RFC 5492: Capabilities Advertisement with BGP-4 {#ra_rfc5492}

Reading: partial reading. Errata: errata checked: 1 (3882 rejected, technical). Obsoletes: RFC 3392.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0024 | 3 | "In this case, the speaker SHOULD attempt to re-establish a BGP connection with the peer without sending to the peer the Capabilities Optional Parameter." | A speaker that needs capabilities (for example to exchange only IPv6 routes, or four-octet AS numbers) gains nothing from a session without them, and the fallback is the downgrade path an attacker can trigger with a forged NOTIFICATION (see RFC 4724). The erratum asking to make the retry a local choice was rejected because the SHOULD already allows it; the text gives no guidance on when not to retry. | ambiguity | 3882 (Rejected) |

### RFC 6793: BGP Support for Four-Octet Autonomous System (AS) Number Space {#ra_rfc6793}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (held, technical, section 8 MIB reference). Obsoletes: RFC 4893. Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0025 | 8 | "If the BGP4-MIB [RFC4273] is supported, there are no additional manageability concerns that arise from the use of four-octet AS numbers" | RFC 4273 types AS numbers as Integer32 (0..65535), so it cannot carry four-octet AS numbers. | error | 4538 (Held) |

### RFC 7606: Revised Error Handling for BGP UPDATE Messages {#ra_rfc7606}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (held, editorial: 7.16 "treat as withdraw" spelling). Updates: RFC 1997, RFC 4271, RFC 4360, RFC 4456, RFC 4760, RFC 5543, RFC 5701, RFC 6368.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0026 | 4 | "For all path attributes other than those specified as having an attribute length that may be zero, it SHALL be considered a syntax error for the attribute to have a length of zero." | For an unrecognized optional attribute the receiver cannot know whether zero length is allowed, so the rule either applies to every unrecognized attribute (making a zero-length unknown attribute malformed, with no stated approach) or to none. The sentence that follows limits the claim to "the path attributes considered in this specification". | ambiguity | none; **proposed erratum below** |
| RA-0027 | 3 (h) | "Otherwise, the approach with the strongest action MUST be used." | "Strongest" is not defined as an order. The order is implied by section 2 (session reset > AFI/SAFI disable > treat-as-withdraw > attribute discard), but "AFI/SAFI disable" against "treat-as-withdraw" is never compared explicitly. | ambiguity | none |
| RA-0028 | 5.1 | "The MP_REACH_NLRI or MP_UNREACH_NLRI attribute (if present) SHALL be encoded as the very first path attribute in an UPDATE message." | See RFC 4271 5: conflicts with the SHOULD ascending order there. Also, "MUST NOT contain more than one of" Withdrawn Routes, NLRI, MP_REACH and MP_UNREACH forbids the common legacy practice of IPv4 withdrawals and announcements in one UPDATE; receivers MUST still accept it. | contradiction | none |
| RA-0029 | 7.11 | "thus, the "session reset" or "AFI/SAFI disable" approach MUST be used." | Two approaches are permitted without a rule for choosing. | ambiguity | none |

Proposed erratum RA-0026 (RFC 7606, Section 4; type: Technical):

```
Original Text
-------------
   For all path attributes other than those specified as having an
   attribute length that may be zero, it SHALL be considered a
   syntax error for the attribute to have a length of zero.

Corrected Text
--------------
   For all path attributes recognized by the receiver, other than
   those specified as having an attribute length that may be zero,
   it SHALL be considered a syntax error for the attribute to have a
   length of zero. An unrecognized optional attribute of length zero
   is handled as specified in RFC 4271 Section 5 for unrecognized
   attributes.

Notes
-----
   A receiver cannot know whether an unrecognized attribute may have
   length zero; the rule as written either makes every zero-length
   unrecognized attribute malformed (with no stated approach) or
   cannot be applied.
```

### RFC 7911: Advertisement of Multiple Paths in BGP {#ra_rfc7911}

Reading: mechanical checks only. Errata: errata not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0030 | 3 | "If a BGP speaker receives a message to withdraw a prefix with a Path Identifier not seen before, it SHOULD silently ignore it." | Nothing is said about an UPDATE whose NLRI cannot be parsed because the two sides disagree on whether ADD-PATH applies to a family; with ADD-PATH the 4-octet Path Identifier makes misparsing likely to look valid. RFC 7606 5.3 does not cover it. | ambiguity | errata not checked |

### RFC 8277: Using BGP to Bind MPLS Labels to Address Prefixes {#ra_rfc8277}

Reading: targeted reading of the relevant sections. Errata: errata: none found in search (errata page not listed); RFC 3107, which it obsoletes, has 6 (2 verified technical, 1 held technical 4582 on withdrawal, 3 rejected). Obsoletes: RFC 3107.

Nothing notable found.

### RFC 9552: Distribution of Link-State and Traffic Engineering Information Using BGP {#ra_rfc9552}

Reading: targeted reading of the relevant sections. Errata: errata checked: 2 (both verified, editorial). Obsoletes: RFC 7752, RFC 9029.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0032 | 5.3.1.1 | "\|O\|T\|E\|B\|R\|V\|   \|   (Figure 15) against Table 7: 'A' \| Attached Bit \| [ISO10589]" | The figure names the second bit "T"; Table 7 calls it "A" (IS-IS Attached bit). The erratum corrects the figure. An implementer working from the figure gets the bit name wrong but the position right. | editorial | 7789 (Verified) |
| RA-0033 | 5.2.2 | "... and in the case of links having only IPv6 link-local addressing ..." | Stray "and" makes the sentence read as a third case. | editorial | 8766 (Verified) |

### Other RFCs in this area {#ra_bgp_other}

Mechanical checks only, no hit: RFC 1997 (BGP Communities Attribute), RFC 2042 (Registering New BGP Attribute Types), RFC 2385 (Protection of BGP Sessions via the TCP MD5 Signature Option), RFC 2545 (Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing), RFC 2918 (Route Refresh Capability for BGP-4), RFC 3765 (NOPEER Community for Border Gateway Protocol (BGP) Route Scope Control), RFC 4360 (BGP Extended Communities Attribute), RFC 4486 (Subcodes for BGP Cease Notification Message), RFC 4659 (BGP-MPLS IP Virtual Private Network (VPN) Extension for IPv6 VPN), RFC 4798 (Connecting IPv6 Islands over IPv4 MPLS Using IPv6 Provider Edge Router), RFC 5004 (Avoid BGP Best Path Transitions from One External to Another), RFC 5065 (Autonomous System Confederations for BGP), RFC 5291 (Outbound Route Filtering Capability for BGP-4), RFC 5398 (Autonomous System (AS) Number Reservation for Documentation Use), RFC 5543 (BGP Traffic Engineering Attribute), RFC 5668 (4-Octet AS Specific BGP Extended Community), RFC 5701 (IPv6 Address Specific BGP Extended Community Attribute), RFC 6286 (Autonomous-System-Wide Unique BGP Identifier for BGP-4), RFC 6368 (Internal BGP as the Provider/Customer Edge Protocol for BGP/MPLS IP Vi), RFC 6608 (Subcodes for BGP Finite State Machine Error), RFC 6938 (Deprecation of BGP Path Attributes: DPA, ADVERTISER, and RCID_PATH / C), RFC 6996 (Autonomous System (AS) Reservation for Private Use), RFC 7153 (IANA Registries for BGP Extended Communities), RFC 7300 (Reservation of Last Autonomous System (AS) Numbers), RFC 7311 (The Accumulated IGP Metric Attribute for BGP), RFC 7313 (Enhanced Route Refresh Capability for BGP-4), RFC 7447 (Deprecation of BGP Entropy Label Capability Attribute), RFC 7607 (Codification of AS 0 Processing), RFC 7611 (BGP ACCEPT_OWN Community Attribute), RFC 7947 (Internet Exchange BGP Route Server), RFC 7948 (Internet Exchange BGP Route Server Operations), RFC 7999 (BLACKHOLE Community), RFC 8092 (BGP Large Communities Attribute), RFC 8093 (Deprecation of BGP Path Attribute Values 30, 31, 129, 241, 242, and 24), RFC 8205 (BGPsec Protocol Specification), RFC 8212 (Default External BGP (EBGP) Route Propagation Behavior without Policie), RFC 8326 (Graceful BGP Session Shutdown), RFC 8538 (Notification Message Support for BGP Graceful Restart), RFC 8571 (BGP - Link State (BGP-LS) Advertisement of IGP Traffic Engineering Per), RFC 8654 (Extended Message Support for BGP), RFC 8669 (Segment Routing Prefix Segment Identifier Extensions for BGP), RFC 8814 (Signaling Maximum SID Depth (MSD) Using the Border Gateway Protocol - ), RFC 8950 (Advertising IPv4 Network Layer Reachability Information (NLRI) with an), RFC 9003 (Extended BGP Administrative Shutdown Communication), RFC 9012 (The BGP Tunnel Encapsulation Attribute), RFC 9015 (BGP Control Plane for the Network Service Header in Service Function C), RFC 9072 (Extended Optional Parameters Length for BGP OPEN Message), RFC 9085 (Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment R), RFC 9086 (Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment R), RFC 9088 (Signaling Entropy Label Capability and Entropy Readable Label Depth Us), RFC 9104 (Distribution of Traffic Engineering Extended Administrative Groups Usi), RFC 9234 (Route Leak Prevention and Detection Using Roles in UPDATE and OPEN Mes), RFC 9384 (A BGP Cease NOTIFICATION Subcode for Bidirectional Forwarding Detectio), RFC 9494 (Long-Lived Graceful Restart for BGP), RFC 9514 (Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment R), RFC 9687 (Border Gateway Protocol 4 (BGP-4) Send Hold Timer), RFC 9774 (Deprecation of AS_SET and AS_CONFED_SET in BGP), RFC 9793 (BGP Extensions for Bit Index Explicit Replication (BIER)), RFC 9830 (Advertising Segment Routing Policies in BGP), RFC 9831 (Segment Type Extensions for BGP Segment Routing (SR) Policy), RFC 10039 (Interconnecting EVPN and IPVPN Domains).

## IS-IS, IGP TE, Segment Routing and IP FRR {#ra_isis}

62 RFCs in this area; 12 findings, 4 of them proposed errata.

### RFC 1142: OSI IS-IS Intra-domain Routing Protocol {#ra_rfc1142}

Reading: targeted reading of the relevant sections. Errata: errata not checked; RFC 3719 lists the known ISO 10589 interoperability issues. 

Nothing notable found.

### RFC 1195: Use of OSI IS-IS for Routing in TCP/IP and Dual Environments {#ra_rfc1195}

Reading: targeted reading of the relevant sections. Errata: errata checked: 2 (both held: 683 technical, 3741 editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0034 | 3.3 | "DFI       1 octet       value "xx"  /  AA        3 octets      value "xx xx xx"" | The values are given as placeholders that are neither valid decimal nor hexadecimal, so the derived NSAP is not specified. | ambiguity | 683 (Held) |
| RA-0035 | 5.3.5 | "7 IP Internal Reachability Information -- IP addresses within the routing domain reachable directly via one or more interfaces" | The level 2 description omits that entries may be reached indirectly through level 1 routing (section 5.3.2 says so); RFCs 3719 and 3787 clarify. | editorial | 3741 (Held) |

### RFC 5120: M-ISIS: Multi Topology (MT) Routing in Intermediate System to Intermediate Systems (IS-ISs) {#ra_rfc5120}

Reading: partial reading. Errata: errata not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0036 | 7.1 | "If a router advertises MT TLV, it has to advertise all the MTs it participates in, specifically including topology ID #0 also." | Read with "Lack of MT TLV ... MUST be interpreted as participation ... in MT ID #0 only", this means that every MT router is in MT 0, which excludes IPv6-only (MT 2 only) routers that the rest of the document allows. "has to" is not a 2119 keyword, "This MT TLV can advertise up to 127 MTs" reads as a global limit although the TLV may repeat, and an odd LENGTH ("SHOULD be 2 times the number") has no stated handling. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0036 (RFC 5120, Section 7.1; type: Technical):

```
Original Text
-------------
   If a router advertises MT TLV, it has to advertise all the MTs it
   participates in, specifically including topology ID #0 also.

Corrected Text
--------------
   If a router advertises the MT TLV, it MUST advertise all the MTs
   it participates in, including MT ID #0 if it participates in MT
   ID #0.

Notes
-----
   As written, every MT-capable router must be in MT #0, which
   excludes routers that participate only in other topologies (for
   example MT #2 only). "has to" is not an RFC 2119 keyword. The
   limit of 127 MTs applies to one TLV instance, since the TLV may
   appear more than once.
```

### RFC 5305: IS-IS Extensions for Traffic Engineering {#ra_rfc5305}

Reading: targeted reading of the relevant sections. Errata: errata: no errata page in search results (errata not confirmed). Obsoletes: RFC 3784.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0037 | 3, 4 | "all metrics greater than or equal to MAX_PATH_METRIC SHALL be considered to have a metric of MAX_PATH_METRIC." | Section 3 (and 4) clamp a path metric at MAX_PATH_METRIC (0xFE000000), which leaves the destination reachable at that cost. ISO 10589 (C.2) drops a path whose cost exceeds MaxPathMetric, and section 4 itself says a prefix advertised with a metric above MAX_PATH_METRIC "MUST NOT be considered during the normal SPF computation". Whether a path whose sum overflows is usable (clamped) or unreachable (ISO behaviour) is therefore read both ways; RFC 5308 3 repeats the clamp for IPv6. | contradiction | none found; **proposed erratum below** |
| RA-0038 | 4 | "If a prefix is advertised with a metric larger then MAX_PATH_METRIC (0xFE000000, see paragraph 3.0), this prefix MUST NOT be considered" | "larger then" for "larger than"; "paragraph 3.0" is not a section (section 3 defines MAX_PATH_METRIC). The rule also leaves a prefix metric exactly equal to 0xFE000000 usable, unlike the 2^24 - 1 link rule, which excludes the maximum value itself. | editorial | none found; **proposed erratum below** |
| RA-0039 | 3 | "If a link is advertised with the maximum link metric (2^24 - 1), this link MUST NOT be considered during the normal SPF computation." | The exclusion applies to "the normal SPF"; whether the link is still used for TE (CSPF) and for flex-algorithm computations with a TE or delay metric is left open (RFC 9350 later answers it for flex-algo only). | ambiguity | none found |

Proposed erratum RA-0037 (RFC 5305, Section 3, 4; type: Technical):

```
Original Text
-------------
   To preclude overflow within a traffic engineering Shortest Path
   First (SPF) implementation, all metrics greater than or equal to
   MAX_PATH_METRIC SHALL be considered to have a metric of
   MAX_PATH_METRIC.

Corrected Text
--------------
   (No single correction; the working group should state which is
   intended.) Either: "... a path whose metric would exceed
   MAX_PATH_METRIC SHALL be considered unreachable." Or: "... SHALL
   be considered to have a metric of MAX_PATH_METRIC and remains
   usable."

Notes
-----
   ISO 10589 discards paths whose cost exceeds MaxPathMetric, while
   this text clamps the cost; Section 4 separately excludes prefixes
   advertised above MAX_PATH_METRIC. RFC 5308 Section 3 repeats the
   clamp for IPv6. Implementations differ.
```

Proposed erratum RA-0038 (RFC 5305, Section 4; type: Editorial):

```
Original Text
-------------
   If a prefix is advertised with a metric larger then
   MAX_PATH_METRIC (0xFE000000, see paragraph 3.0), this prefix MUST
   NOT be considered

Corrected Text
--------------
   If a prefix is advertised with a metric larger than
   MAX_PATH_METRIC (0xFE000000, see Section 3), this prefix MUST NOT
   be considered

Notes
-----
   Typo ("then") and a reference to a nonexistent "paragraph 3.0";
   MAX_PATH_METRIC is defined in Section 3.
```

### RFC 5308: Routing IPv6 with IS-IS {#ra_rfc5308}

Reading: partial reading. Errata: errata not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0040 | 2 | "than MAX_V6_PATH_METRIC (0xFE000000), this prefix MUST not be considered during the normal Shortest Path First (SPF) computation." | "MUST not" written in mixed case; the intent is MUST NOT. | editorial | not checked |

### RFC 5310: IS-IS Generic Cryptographic Authentication {#ra_rfc5310}

Reading: targeted reading of the relevant sections. Errata: errata not checked (no errata page in search results for 5305/5310; 5310 not searched separately). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0041 | 3.3 | "In this application, Ko is always L octets long. ... If the Authentication Key (K) is more than L octets long, then Ko is set to H(K)." | The key is hashed when it is longer than the digest length L, while RFC 2104 HMAC hashes it only when it is longer than the block size B. "Ko XOR Ipad" then combines an L-octet Ko with a B-octet Ipad without saying how (zero extension is implied). Implementations that use a plain HMAC library produce different MACs for keys with L < \|K\| <= B (for HMAC-SHA-256: 33 to 64 octets), so such keys do not interoperate across implementations even though both claim RFC 5310. | ambiguity | not checked; **proposed erratum below** |
| RA-0042 | 3.3 | "For SHA-1 and SHA-256: B == 64 / For SHA-384 and SHA-512: B == 128" | SHA-224, one of the five algorithms the RFC defines, has no block size listed (it is 64). | editorial | not checked |
| RA-0043 | 3.5, 5 | "the remaining lifetime of the LSP MUST be set to zero before computing the authentication, thus this field is not authenticated." | Security gap stated by the RFC itself: an on-path attacker can change Remaining Lifetime (for example to purge an LSP early or keep a dead one alive) without breaking the MAC. RFC 6232 / 6233 add purge originator identification and authenticated purges but do not close the lifetime gap for non-zero values. | error | not checked |

Proposed erratum RA-0041 (RFC 5310, Section 3.3; type: Technical):

```
Original Text
-------------
   In this application, Ko is always L octets long.

Corrected Text
--------------
   In this application, Ko is always L octets long. Note that this
   differs from HMAC [RFC2104], which hashes the key only when it is
   longer than the block size B; for keys longer than L but not
   longer than B the two computations give different results. Before
   the XOR with Ipad and Opad, Ko is extended with zeros to B
   octets.

Notes
-----
   Implementations built on a standard HMAC library do not
   interoperate with implementations that follow this section for
   key lengths L < |K| <= B. The text also does not say how an
   L-octet Ko is combined with B-octet Ipad
   Opad. The block size of SHA-224 (B == 64) is missing from the
   list.
```

### RFC 8570: IS-IS Traffic Engineering (TE) Metric Extensions {#ra_rfc8570}

Reading: partial reading. Errata: errata checked via the obsoleted RFC 7810: 5293 (held, editorial), fixed in RFC 8570 section 11. Obsoletes: RFC 7810.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0044 | 4.5 to 4.7, 11 | "The length specified was 4, which did not include the RESERVED field shown in the figures." | RFC 7810 drew a RESERVED octet that its Length (4) did not count; implementations split on length 4 against 5. RFC 8570 removes the field. A receiver may still meet length-5 sub-TLVs 37 to 39 from old RFC 7810 speakers. | error | RFC 7810: 5293 (Held) |

### RFC 8667: IS-IS Extensions for Segment Routing {#ra_rfc8667}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (7722 verified, editorial heading). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0045 | 2.1.1.1 | "2.1.1.1.  V-Flag and L-Flag" | The heading should also name the SID/Index/Label field, whose size depends on the flags (4-octet index or 3-octet label). Other flag combinations "are invalid" and the advertisement MUST be ignored. | editorial | 7722 (Verified) |

### RFC 8706: Restart Signaling for IS-IS {#ra_rfc8706}

Reading: targeted reading of the relevant sections. Errata: errata: no errata page in search results. Obsoletes: RFC 5306.

Nothing notable found.

### Other RFCs in this area {#ra_isis_other}

Mechanical checks only, no hit: RFC 3358 (Optional Checksums in Intermediate System to Intermediate System (ISIS), RFC 3630 (Traffic Engineering (TE) Extensions to OSPF Version 2), RFC 3719 (Recommendations for Interoperable Networks using Intermediate System t), RFC 3787 (Recommendations for Interoperable IP Networks using Intermediate Syste), RFC 3906 (Calculating Interior Gateway Protocol (IGP) Routes Over Traffic Engine), RFC 4444 (Management Information Base for Intermediate System to Intermediate Sy), RFC 5089 (IS-IS Protocol Extensions for Path Computation Element (PCE) Discovery), RFC 5130 (A Policy Control Mechanism in IS-IS Using Administrative Tags), RFC 5286 (Basic Specification for IP Fast Reroute: Loop-Free Alternates), RFC 5301 (Dynamic Hostname Exchange Mechanism for IS-IS), RFC 5302 (Domain-Wide Prefix Distribution with Two-Level IS-IS), RFC 5303 (Three-Way Handshake for IS-IS Point-to-Point Adjacencies), RFC 5304 (IS-IS Cryptographic Authentication), RFC 5306 (Restart Signaling for IS-IS), RFC 5307 (IS-IS Extensions in Support of Generalized Multi-Protocol Label Switch), RFC 5311 (Simplified Extension of Link State PDU (LSP) Space for IS-IS), RFC 5316 (ISIS Extensions in Support of Inter-Autonomous System (AS) MPLS and GM), RFC 6119 (IPv6 Traffic Engineering in IS-IS), RFC 6213 (IS-IS BFD-Enabled TLV), RFC 6232 (Purge Originator Identification TLV for IS-IS), RFC 6233 (IS-IS Registry Extension for Purges), RFC 7308 (Extended Administrative Groups in MPLS Traffic Engineering (MPLS-TE)), RFC 7490 (Remote Loop-Free Alternate (LFA) Fast Reroute (FRR)), RFC 7775 (IS-IS Route Preference for Extended IP and IPv6 Reachability), RFC 7794 (IS-IS Prefix Attributes for Extended IPv4 and IPv6 Reachability), RFC 7811 (An Algorithm for Computing IP/LDP Fast Reroute Using Maximally Redunda), RFC 7812 (An Architecture for IP/LDP Fast Reroute Using Maximally Redundant Tree), RFC 7981 (IS-IS Extensions for Advertising Router Information), RFC 8102 (Remote-LFA Node Protection and Manageability), RFC 8202 (IS-IS Multi-Instance), RFC 8333 (Micro-loop Prevention by Introducing a Local Convergence Delay), RFC 8402 (Segment Routing Architecture), RFC 8405 (Shortest Path First (SPF) Back-Off Delay Algorithm for Link-State IGPs), RFC 8491 (Signaling Maximum SID Depth (MSD) Using IS-IS), RFC 8660 (Segment Routing with the MPLS Data Plane), RFC 8661 (Segment Routing MPLS Interworking with LDP), RFC 8668 (Advertising Layer 2 Bundle Member Link Attributes in IS-IS), RFC 8754 (IPv6 Segment Routing Header (SRH)), RFC 8986 (Segment Routing over IPv6 (SRv6) Network Programming), RFC 9256 (Segment Routing Policy Architecture), RFC 9294 (Application-Specific Link Attributes Advertisement Using the Border Ga), RFC 9346 (IS-IS Extensions in Support of Inter-Autonomous System (AS) MPLS and G), RFC 9350 (IGP Flexible Algorithm), RFC 9352 (IS-IS Extensions to Support Segment Routing over the IPv6 Data Plane), RFC 9377 (IS-IS Flood Reflection), RFC 9479 (IS-IS Application-Specific Link Attributes), RFC 9502 (IGP Flexible Algorithm in IP Networks), RFC 9800 (Compressed SRv6 Segment List Encoding), RFC 9843 (IGP Flexible Algorithms: Bandwidth, Delay, Metrics, and Constraints), RFC 9855 (Topology Independent Fast Reroute Using Segment Routing), RFC 9885 (Multi-Part TLVs in IS-IS), RFC 9917 (IGP Flexible Algorithms Reverse Affinity Constraint), RFC 9929 (IGP Unreachable Prefix Announcement).

## MPLS, LDP and mLDP {#ra_ldp}

44 RFCs in this area; 9 findings, 2 of them proposed errata.

### RFC 3032: MPLS Label Stack Encoding {#ra_rfc3032}

Reading: targeted reading of the relevant sections. Errata: errata checked: 4 (3 verified, 1 held; all editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0046 | 2.3.2 | "Since an ICMP message is  never sent as a result of" | Overstates RFC 1122: only ICMP error messages must not be sent in response to ICMP error messages. An LSR generating ICMP for a labelled Echo Request that expires must still be allowed to send Time Exceeded. | ambiguity | 982 (Verified) |
| RA-0047 | 4.2 | "hex 8281 (MPLS)." | The PPP protocol number 0x8281 is the MPLS Control Protocol (MPLSCP); 0x0281 is MPLS unicast. | editorial | 2166 (Verified) |

### RFC 3212: Constraint-Based LSP Setup using LDP {#ra_rfc3212}

Reading: mechanical checks only. Errata: errata not checked (CR-LDP, background only). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0048 | 3.4 | "New status codes are defined in Section 4.11 to signal error notifications associated with the establishment of a CR-LSP" | There is no section 4.11; the new status codes are in the IANA section (5.3, "Status Code Space"). | error | not checked; **proposed erratum below** |

Proposed erratum RA-0048 (RFC 3212, Section 3.4; type: Technical):

```
Original Text
-------------
   New status codes are defined in Section 4.11 to signal error
   notifications associated with the establishment of a CR-LSP

Corrected Text
--------------
   New status codes are defined in Section 5.3 to signal error
   notifications associated with the establishment of a CR-LSP

Notes
-----
   There is no Section 4.11; the status codes are listed in Section
   5.3 (Status Code Space). The document is Historic in practice
   (CR-LDP was abandoned, RFC 3468).
```

### RFC 3478: Graceful Restart Mechanism for Label Distribution Protocol {#ra_rfc3478}

Reading: partial reading. Errata: errata: no errata page in search results. 

Nothing notable found.

### RFC 5036: LDP Specification {#ra_rfc5036}

Reading: targeted reading of the relevant sections. Errata: errata checked: 11 (1 verified, 6 held, 4 rejected; all editorial or rejected questions). Obsoletes: RFC 3036.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0049 | 2.6.3, 3.5.3 | "Each interface on an LSR is configured to operate in either Downstream Unsolicited or Downstream on Demand advertisement mode." | Section 2.6.3 makes the advertisement mode a per-interface property, while 3.5.3 negotiates it once per session (the A bit), and a session can cover several interfaces or be targeted. The erratum reporting the conflict was rejected as needing consensus, so the text stands; RFC 7358 and RFC 7032 later treat the mode per session (and per FEC type). | ambiguity | 4465 (Rejected) |
| RA-0050 | 3.5.8 | "Specifies the LSRs along the LSR being set up by the Label Request" | "LSR" is written where "LSP" (the path being set up) is meant. | editorial | 3156 (Verified) |
| RA-0051 | 3.5.3 | "D, Loop Detection  Indicates whether Loop Detection based on Path Vectors is enabled." | The rules for resolving a disagreement are given for the A bit but not for the D bit. | ambiguity | none found |
| RA-0052 | 3.5.11 (and the other message figures) | "\|0\|   Label Release (0x0403)   \|      Message Length            \|" | In the message figures the field boundary after the 15-bit Message Type is drawn one bit early (column 31 instead of 32), so the figure shows a 14-bit type and a 17-bit length. The text (U bit, 15-bit type, 16-bit length) is correct. The same misdrawing appears in RFC 3036, RFC 3212 and RFC 3270. | editorial | none found; **proposed erratum below** |

Proposed erratum RA-0052 (RFC 5036, Section 3.5.11 (and the other message figures); type: Editorial):

```
Original Text
-------------
   |0|   Label Release (0x0403)   |      Message Length            |

Corrected Text
--------------
   |0|   Label Release (0x0403)    |      Message Length           |

Notes
-----
   In the message figures the boundary between Message Type and
   Message Length is drawn at bit 15 instead of bit 16. Editorial;
   the text gives the field sizes correctly. The same drawing
   appears in RFC 3036, RFC 3212 and RFC 3270.
```

### RFC 6388: Label Distribution Protocol Extensions for Point-to-Multipoint and Multipoint-to-Multipoint Label Switched Paths {#ra_rfc6388}

Reading: partial reading. Errata: errata: no errata page in search results. 

Nothing notable found.

### RFC 6790: The Use of Entropy Labels in MPLS Forwarding {#ra_rfc6790}

Reading: partial reading. Errata: errata checked: 1 (3431 held, technical). Updates: RFC 3031, RFC 3107, RFC 3209, RFC 5036.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0053 | 5.2 | "attribute of value 28.  The inclusion of this attribute with an NLRI indicates that the advertising BGP router can process entropy labels" | The Entropy Label Capability attribute is described only as "of value 28"; the text does not say that its length is zero and it carries no data. Together with RFC 7606 section 4 (a zero-length attribute is a syntax error unless its specification allows length zero), a receiver can treat every ELC attribute as malformed. RFC 7447 has since deprecated the attribute, but old speakers may still send it. | ambiguity | 3431 (Held) |

### RFC 7552: Updates to LDP for IPv6 {#ra_rfc7552}

Reading: partial reading. Errata: errata checked: 1 (5690 verified, editorial). Updates: RFC 5036, RFC 6720.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0054 | 6.1.1 | "Dual-Stack capability: TLV code point (Ox0701)" | The Dual-Stack capability TLV code point is printed with a letter O ("Ox0701"); it is 0x0701. | editorial | 5690 (Verified) |

### Other RFCs in this area {#ra_ldp_other}

Mechanical checks only, no hit: RFC 3036 (LDP Specification), RFC 3429 (Assignment of the 'OAM Alert Label' for Multiprotocol Label Switching ), RFC 3443 (Time To Live (TTL) Processing in Multi-Protocol Label Switching (MPLS)), RFC 3468 (The Multiprotocol Label Switching (MPLS) Working Group decision on MPL), RFC 3479 (Fault Tolerance for the Label Distribution Protocol (LDP)), RFC 4950 (ICMP Extensions for Multiprotocol Label Switching), RFC 5283 (LDP Extension for Inter-Area Label Switched Paths (LSPs)), RFC 5331 (MPLS Upstream Label Assignment and Context-Specific Label Space), RFC 5332 (MPLS Multicast Encapsulations), RFC 5443 (LDP IGP Synchronization), RFC 5561 (LDP Capabilities), RFC 5586 (MPLS Generic Associated Channel), RFC 5918 (Label Distribution Protocol (LDP) 'Typed Wildcard' Forward Equivalence), RFC 5919 (Signaling LDP Label Advertisement Completion), RFC 6138 (LDP IGP Synchronization for Broadcast Networks), RFC 6370 (MPLS Transport Profile (MPLS-TP) Identifiers), RFC 6378 (MPLS Transport Profile (MPLS-TP) Linear Protection), RFC 6389 (MPLS Upstream Label Assignment for LDP), RFC 6512 (Using Multipoint LDP When the Backbone Has No Route to the Root), RFC 6667 (LDP 'Typed Wildcard' Forwarding Equivalence Class (FEC) for PWid and G), RFC 6720 (The Generalized TTL Security Mechanism (GTSM) for the Label Distributi), RFC 6826 (Multipoint LDP In-Band Signaling for Point-to-Multipoint and Multipoin), RFC 7032 (LDP Downstream-on-Demand in Seamless MPLS), RFC 7140 (LDP Extensions for Hub and Spoke Multipoint Label Switched Path), RFC 7246 (Multipoint Label Distribution Protocol In-Band Signaling in a Virtual ), RFC 7274 (Allocating and Retiring Special-Purpose MPLS Labels), RFC 7307 (LDP Extensions for Multi-Topology), RFC 7349 (LDP Hello Cryptographic Authentication), RFC 7358 (Label Advertisement Discipline for LDP Forwarding Equivalence Classes ), RFC 7438 (Multipoint LDP (mLDP) In-Band Signaling with Wildcards), RFC 7473 (Controlling State Advertisements of Non-negotiated LDP Applications), RFC 7715 (Multipoint LDP (mLDP) Node Protection), RFC 8223 (Application-Aware Targeted LDP), RFC 8320 (LDP Extensions to Support Maximally Redundant Trees), RFC 8356 (Experimental Codepoint Allocation for the Path Computation Element Com), RFC 9658 (Multipoint LDP Extensions for Multi-Topology Routing), RFC 9789 (MPLS Network Actions (MNAs) Framework).

## Pseudowires, VPLS and ICCP {#ra_pw}

20 RFCs in this area; 6 findings, 1 of them proposed errata.

### RFC 4385: Pseudowire Emulation Edge-to-Edge (PWE3) Control Word for Use over an MPLS PSN {#ra_rfc4385}

Reading: partial reading. Errata: errata checked: 1 (1743 verified, technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0055 | 4, 4.1, 4.2 | "The sequence number that follows 65535 (maximum unsigned 16-bit number) is one." | The rules that exclude zero (wrap from 65535 to 1, zero meaning "not used") are written for every PW type, but TDM pseudowires (SAToP, CESoPSN, TDMoIP) use zero as an ordinary sequence number. The erratum limits the zero-excluding rules to non-TDM PWs and says a zero sequence number on a non-TDM PW is treated as in order. | error | 1743 (Verified) |

### RFC 4762: Virtual Private LAN Service (VPLS) Using Label Distribution Protocol (LDP) Signaling {#ra_rfc4762}

Reading: targeted reading of the relevant sections. Errata: errata checked: 2 (4144 verified editorial, 4834 held editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0056 | Appendix A | "In a VPLS, we use a VCID (which, when using the PWid FEC, has been substituted with a more general identifier (AGI)" | The PWid FEC (FEC 128) has a PW ID, not a VCID field, and the AGI belongs to the Generalized PWid FEC (FEC 129), not the PWid FEC. Read literally, the sentence mixes the two encodings. | editorial | 4144 (Verified) |

### RFC 6870: Pseudowire Preferential Forwarding Status Bit {#ra_rfc6870}

Reading: targeted reading of the relevant sections. Errata: errata checked: 3656 (held, editorial; all "Section 15" references). Updated by RFC 7771, which is not in rfcs/. Updates: RFC 4447.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0057 | 1, 5 | "Section 15 shows in detail how the mechanisms described in this document are used to achieve the desired protection schemes" | There is no section 15; the applications are in Appendix A ("Applications of PW Redundancy Procedures"), the numbering of the draft. Eight references are affected, including the recommendation "it is recommended to use the independent mode of operation as in the application described in Section 15.2" (Appendix A.2). | error | 3656 (Held) |
| RA-0058 | header | "(no RFC text: the RFC Editor page for RFC 6870 states "Updated by RFC 7771")" | RFC 7771 ("Switching Provider Edge (S-PE) Protection for MS-PWs") updates RFC 6870 but is not in rfcs/, so the copy the code is checked against misses its changes to the Preferential Forwarding procedures for MS-PWs. | ambiguity | none |

### RFC 8077: Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) {#ra_rfc8077}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 shown (5243 rejected, technical, 6.1 Group ID example). Obsoletes: RFC 4447, RFC 6723.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0059 | 6.1 | "... wildcard label withdrawals and status notifications ... to remote PEs upon physical port failure." | The Group ID example names only physical port failure; whether a PE may (or should) use Group-ID wildcards for other shared failures, such as a transport tunnel going down, is left implicit. The erratum asking for it was rejected because the sentence is an example. | ambiguity | 5243 (Rejected) |

### RFC 8338: Signaling Root-Initiated Point-to-Multipoint Pseudowire Using LDP {#ra_rfc8338}

Reading: targeted reading of the relevant sections. Errata: errata not checked. Updates: RFC 7385.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0060 | 3.2.1 | "Alternatively, typed wildcard FEC described in Section 2.3, can be used to achieve the same or to have better filtering." | Section 2.3 does not exist (2 is Terminology); the typed wildcard FEC is section 3.3. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0060 (RFC 8338, Section 3.2.1; type: Technical):

```
Original Text
-------------
   typed wildcard FEC described in Section 2.3, can be used to

Corrected Text
--------------
   typed wildcard FEC described in Section 3.3, can be used to

Notes
-----
   Section 2.3 does not exist; the Typed Wildcard FEC format is
   Section 3.3.
```

### Other RFCs in this area {#ra_pw_other}

Mechanical checks only, no hit: RFC 4446 (IANA Allocations for Pseudowire Edge to Edge Emulation (PWE3)), RFC 4447 (Pseudowire Setup and Maintenance Using the Label Distribution Protocol), RFC 4448 (Encapsulation Methods for Transport of Ethernet over MPLS Networks), RFC 4623 (Pseudowire Emulation Edge-to-Edge (PWE3) Fragmentation and Reassembly), RFC 4761 (Virtual Private LAN Service (VPLS) Using BGP for Auto-Discovery and Si), RFC 5003 (Attachment Individual Identifier (AII) Types for Aggregation), RFC 5085 (Pseudowire Virtual Circuit Connectivity Verification (VCCV): A Control), RFC 6073 (Segmented Pseudowire), RFC 6074 (Provisioning, Auto-Discovery, and Signaling in Layer 2 Virtual Private), RFC 6391 (Flow-Aware Transport of Pseudowires over an MPLS Packet Switched Netwo), RFC 6718 (Pseudowire Redundancy), RFC 7267 (Dynamic Placement of Multi-Segment Pseudowires), RFC 7275 (Inter-Chassis Communication Protocol for Layer 2 Virtual Private Netwo), RFC 7338 (Requirements and Framework for Point-to-Multipoint Pseudowires over MP), RFC 7361 (LDP Extensions for Optimized MAC Address Withdrawal in a Hierarchical ).

## RSVP, RSVP-TE and GMPLS {#ra_rsvp}

44 RFCs in this area; 12 findings, 0 of them proposed errata.

### RFC 2205: Resource ReSerVation Protocol (RSVP) -- Version 1 Functional Specification {#ra_rfc2205}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (4732 held, editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0061 | A.5 | "Its contents depend upon the Error Type." | "Error Type" is not defined anywhere in the RFC; the field that qualifies Error Value is the Error Code. | editorial | 4732 (Held) |

### RFC 2747: RSVP Cryptographic Authentication {#ra_rfc2747}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (4313 verified, technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0062 | 3.2 | "The remaining 32 bits are filled with the 32 least significant bits of the timestamp." | The example puts the low-order timestamp bits in the high half of the sequence number; the erratum says the 32 most significant bits of the timestamp are meant (the counter supplies the low half). With a timestamp finer than one second the literal text would make sequence numbers repeat or go backwards. | error | 4313 (Verified) |

### RFC 2961: RSVP Refresh Overhead Reduction Extensions {#ra_rfc2961}

Reading: partial reading. Errata: errata: no errata page in search results. 

Nothing notable found.

### RFC 3209: RSVP-TE: Extensions to RSVP for LSP Tunnels {#ra_rfc3209}

Reading: targeted reading of the relevant sections. Errata: errata checked: 2 (2669 verified, 4733 held; both editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0063 | 4.3.3.1 | "The path between a loose node and its preceding node MAY include other network nodes that are not part of the strict node or its preceding abstract node." | The paragraph describes a loose node; "strict" inverts the meaning of the ERO check for a loose hop. | editorial | 2669 (Verified) |
| RA-0064 | 4.3.2 | "set of abstract nodes to be traversed." | An explicit route is ordered; "set" suggests otherwise. | editorial | 4733 (Held) |

### RFC 3473: Generalized Multi-Protocol Label Switching (GMPLS) Signaling Resource ReserVation Protocol-Traffic Engineering (RSVP-TE) Extensions {#ra_rfc3473}

Reading: targeted reading of the relevant sections. Errata: errata checked: 7 (all verified; 3 technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0065 | 4.2.1 | "The Notify_Request Class-Number is 195 (of form 11bbbbbb).  The format of a Notify Request is:" | The text gives Class-Num 195 but the object figures put the C-Type value in the Class-Num position; an implementer copying the figure would send the wrong class. | error | 1518 (Verified) |
| RA-0066 | 5.2.1 | "when labels are recorded for bidirectional LSPs, label ERO subobjects" | Labels are recorded in the RRO; "label ERO subobjects" should read "label RRO subobjects". | error | 4585 (Verified) |
| RA-0067 | 2.4 | "Waveband switching uses the same format as the generalized label, see section 2.2." | Wrong cross-reference: waveband switching is section 2.3. | editorial | 4467 (Verified) |

### RFC 4090: Fast Reroute Extensions to RSVP-TE for LSP Tunnels {#ra_rfc4090}

Reading: targeted reading of the relevant sections. Errata: errata checked: 3 (4203, 6203, 6939; all verified, technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0068 | 6 | "... the "local protection available", "local protection in use"," | When the PLR may set "local protection available" in the RRO was unclear; the erratum says only once a bypass (or detour) has been chosen and the forwarding state to use it is installed. | ambiguity | 4203 (Verified) |
| RA-0069 | 6 | ""bandwidth protection guaranteed" flag is set, the PLR SHOULD try to" | There is no "bandwidth protection guaranteed" flag; the SESSION_ATTRIBUTE flag is "bandwidth protection desired" (0x08). | error | 6203 (Verified) |
| RA-0070 | 4.4 | "requested, we define two new flags in the RRO IPv4 sub-object." | The two new RRO flags are defined only for the IPv4 subobject; the erratum extends them to the IPv6 subobject. | error | 6939 (Verified) |

### RFC 4875: Extensions to Resource Reservation Protocol - Traffic Engineering (RSVP-TE) for Point-to-Multipoint TE Label Switched Paths (LSPs) {#ra_rfc4875}

Reading: targeted reading of the relevant sections. Errata: errata checked: 15 records (2 verified, 10 held, 3 rejected; 1 held technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0071 | 8.2 | "If the Sub-Group Originator ID is its own address, then it MUST set the receiver address in the RESV_CONFIRM object to this address, else it MUST propagate the object unchanged." | The second paragraph of 8.2 is an earlier version of the third: it omits the merge case, where the third paragraph says the LSR MUST put its own Router ID in RESV_CONFIRM when it merges several Resvs carrying one. Read together they give two different MUSTs for a merging transit LSR. | contradiction | 2485 (Held) |
| RA-0072 | 17 | "section 24, PE1 can set up a P2P LSP to P1 and use that as a LSP" | "Figure 2 in section 24" should be "Figure 2 in Appendix A"; section 24 is not in the document. Erratum 2483 corrects a similar wrong reference in 6.1 (4.1 for 5.1). | editorial | 2490 (Verified) |

### Other RFCs in this area {#ra_rsvp_other}

Mechanical checks only, no hit: RFC 2209 (Resource ReSerVation Protocol (RSVP) -- Version 1 Message Processing R), RFC 2210 (The Use of RSVP with IETF Integrated Services), RFC 2211 (Specification of the Controlled-Load Network Element Service), RFC 2212 (Specification of Guaranteed Quality of Service), RFC 2750 (RSVP Extensions for Policy Control), RFC 3097 (RSVP Cryptographic Authentication -- Updated Message Type Value), RFC 3175 (Aggregation of RSVP for IPv4 and IPv6 Reservations), RFC 3270 (Multi-Protocol Label Switching (MPLS) Support of Differentiated Servic), RFC 3471 (Generalized Multi-Protocol Label Switching (GMPLS) Signaling Functiona), RFC 3472 (Generalized Multi-Protocol Label Switching (GMPLS) Signaling Constrain), RFC 3475 (Documentation of IANA assignments for Constraint-Based LSP setup using), RFC 3477 (Signalling Unnumbered Links in Resource ReSerVation Protocol - Traffic), RFC 3988 (Maximum Transmission Unit Signalling Extensions for the Label Distribu), RFC 4105 (Requirements for Inter-Area MPLS Traffic Engineering), RFC 4124 (Protocol Extensions for Support of Diffserv-aware MPLS Traffic Enginee), RFC 4125 (Maximum Allocation Bandwidth Constraints Model for Diffserv-aware MPLS), RFC 4126 (Max Allocation with Reservation Bandwidth Constraints Model for Diffse), RFC 4127 (Russian Dolls Bandwidth Constraints Model for Diffserv-aware MPLS Traf), RFC 4206 (Label Switched Paths (LSP) Hierarchy with Generalized Multi-Protocol L), RFC 4561 (Definition of a Record Route Object (RRO) Node-Id Sub-Object), RFC 4726 (A Framework for Inter-Domain Multiprotocol Label Switching Traffic Eng), RFC 4872 (RSVP-TE Extensions in Support of End-to-End Generalized Multi-Protocol), RFC 4873 (GMPLS Segment Recovery), RFC 4874 (Exclude Routes - Extension to Resource ReserVation Protocol-Traffic En), RFC 4920 (Crankback Signaling Extensions for MPLS and GMPLS RSVP-TE), RFC 5063 (Extensions to GMPLS Resource Reservation Protocol (RSVP) Graceful Rest), RFC 5150 (Label Switched Path Stitching with Generalized Multiprotocol Label Swi), RFC 5151 (Inter-Domain MPLS and GMPLS Traffic Engineering -- Resource Reservatio), RFC 5152 (A Per-Domain Path Computation Method for Establishing Inter-Domain Tra), RFC 5284 (User-Defined Errors for RSVP), RFC 5420 (Encoding of Attributes for MPLS LSP Establishment Using Resource Reser), RFC 5495 (Description of the Resource Reservation Protocol - Traffic-Engineered ), RFC 5712 (MPLS Traffic Engineering Soft Preemption), RFC 6107 (Procedures for Dynamically Signaled Hierarchical Label Switched Paths), RFC 7570 (Label Switched Path (LSP) Attribute in the Explicit Route Object (ERO)), RFC 8169 (Residence Time Measurement in MPLS Networks), RFC 8271 (Updates to the Resource Reservation Protocol for Fast Reroute of Traff).

## PCEP and PCE {#ra_pcep}

36 RFCs in this area; 12 findings, 3 of them proposed errata.

### RFC 5088: OSPF Protocol Extensions for Path Computation Element (PCE) Discovery {#ra_rfc5088}

Reading: mechanical checks only. Errata: errata not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0073 | 7.2 | "the PCE-CAP-FLAGS TLV referenced in Section 4.1.5." | There is no section 4.1.5; the PCE-CAP-FLAGS sub-TLV is section 4.5. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0073 (RFC 5088, Section 7.2; type: Editorial):

```
Original Text
-------------
   the PCE-CAP-FLAGS TLV referenced in Section 4.1.5.

Corrected Text
--------------
   the PCE-CAP-FLAGS sub-TLV defined in Section 4.5.

Notes
-----
   Section 4.1.5 does not exist; the sub-TLV is defined in Section
   4.5.
```

### RFC 5440: Path Computation Element (PCE) Communication Protocol (PCEP) {#ra_rfc5440}

Reading: targeted reading of the relevant sections. Errata: errata checked: 6 (2 verified technical, 2 verified editorial, 2 held editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0074 | 5 | "All PCEP messages MUST be sent using the registered TCP port for the source and destination TCP port." | Read literally a PCC could not use an ephemeral source port, and two sessions between the same pair could not coexist. The erratum: the PCE MUST listen on 4189; the PCC SHOULD use it as source but MAY use an ephemeral port. A PCE must therefore not reject connections from ports other than 4189. | error | 2940 (Verified) |
| RA-0075 | 10.7.1 | "The PCE SHOULD NOT allow parallel TCP connections from the same PCC on the PCEP-registered port." | Section 10.7.1 weakens to SHOULD / SHOULD NOT what sections 5 and 4.2.1 make MUST; the erratum makes both MUST. | contradiction | 2941 (Verified) |
| RA-0076 | 6.9 | "send a PCErr message with Error-value=2 (capability not supported)." | "Error-value=2" is written where Error-Type 2 ("Capability not supported") is meant; there is no Error-value 2 without a type. | editorial | 4427 (Held) |

### RFC 8231: Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE {#ra_rfc8231}

Reading: targeted reading of the relevant sections. Errata: errata checked: 8 (4 verified technical, 2 verified editorial, 1 held technical, 1 rejected technical). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0077 | 8.5 (Error-Type 19 value 1, Error-Type 20 value 1) | "A PCE indicates to a PCC that it cannot process (an otherwise valid) LSP State Report.  The PCEP-ERROR object is followed by the LSP object that identifies the LSP." | The IANA text for 19/1 and 20/1 says an LSP object follows the PCEP-ERROR object, but the PCErr grammar of section 6.3 ("<error>::=[<request-id-list> \| <stateful-request-id-list>] <error-obj-list>", with <stateful-request-id-list>::=<SRP>...) has no place for an LSP object. Both verified errata remove the sentence: the LSP is identified by the SRP that precedes the PCEP-ERROR. | contradiction | 5970, 6231 (Verified) |
| RA-0078 | 7.3.2, 7.3.4 | "Length (16 bits): indicates the total length of the TLV in octets." | RFC 5440 7.1 defines TLV Length as the length of the value only. 7.3.2 (SYMBOLIC-PATH-NAME) says "total length", corrected by erratum 6289; 7.3.4 (RSVP-ERROR-SPEC TLV) has the same wording and no erratum, so it is still wrong in the RFC. | error | 6289 (Verified, 7.3.2 only); **proposed erratum below** |
| RA-0079 | 7.2 | "This means that the PCC may need to issue two PCUpd messages on detecting a wrap." | A PCC sends PCRpt, not PCUpd; the sentence should say two PCRpt messages (acknowledging the last SRP-ID-number before the wrap). | error | 5376 (Verified) |
| RA-0080 | 7.3.3 | "2        Limit reached for PCE-controlled LSPs" | The held erratum considers value 2 unusable (a PCC cannot report it meaningfully); the code point stays in the registry. | ambiguity | 5796 (Held) |
| RA-0081 | 6.4 | "<request>::= <RP> <END-POINTS> [<LSP>] [<LSPA>] [<BANDWIDTH>] [<metric-list>] ..." | The grammar does not place CLASSTYPE relative to LSP; the erratum proposing an order was rejected because the fix needs a consensus document. | ambiguity | 6627 (Rejected) |

Proposed erratum RA-0078 (RFC 8231, Section 7.3.2, 7.3.4; type: Technical):

```
Original Text
-------------
   Length (16 bits): indicates the total length of the TLV in
   octets.  The TLV MUST be zero-padded so that the TLV is 4-octet
   aligned.  (Section 7.3.4)

Corrected Text
--------------
   Length (16 bits): indicates the length of the value portion of
   the TLV in octets.  The TLV MUST be zero-padded so that the TLV
   is 4-octet aligned.

Notes
-----
   Same issue as Erratum 6289 (Section 7.3.2), which did not cover
   the identical text in Section 7.3.4 (RSVP-ERROR-SPEC TLV). RFC
   5440 Section 7.1 defines the TLV Length as the length of the
   value only.
```

### RFC 8253: PCEPS: Usage of TLS to Provide a Secure Transport for the Path Computation Element Communication Protocol (PCEP) {#ra_rfc8253}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (5180 held, editorial). Updates: RFC 5440.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0082 | 3.4 | "of the TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 [RFC6460] and" | RFC 6460 (Suite B profile) does not define these cipher suites; RFC 5289 does. | editorial | 5180 (Held) |

### RFC 8281: Path Computation Element Communication Protocol (PCEP) Extensions for PCE-Initiated LSP Setup in a Stateful PCE Model {#ra_rfc8281}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 shown (6301 verified, technical, grammar). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0083 | 5.1, 6 | "<PCE-initiated-lsp-deletion> ::= <SRP>" | The deletion production (SRP and LSP only) is also used for the delegation-reclaim request of section 6, which may carry more objects; the erratum renames it <PCE-initiated-lsp-deletion-or-reclamation>. | ambiguity | 6301 (Verified) |

### RFC 8664: Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing {#ra_rfc8664}

Reading: targeted reading of the relevant sections. Errata: errata checked: 1 (6753 verified, technical). Updates: RFC 8408.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0084 | 4.3.1 vs 5.2.1 | "If the F bit is set to zero (see below), then the NT field has no meaning and MUST be ignored by the receiver." | The text is inverted (the erratum: when F is one, NT has no meaning). Even corrected it conflicts with 5.2.1, where a PCC "MUST validate that the Length field, S bit, F bit, and NT field are consistent" and answers F = 1 with NT not 0 with 10/11; the F flag text says "The F bit MUST be set to 1 if NT=0; otherwise, it MUST be set to zero". | contradiction | 6753 (Verified); **proposed erratum below** |

Proposed erratum RA-0084 (RFC 8664, Section 4.3.1 vs 5.2.1; type: Technical):

```
Original Text
-------------
   If the F bit is set to zero (see below), then the NT field has no
   meaning and MUST be ignored by the receiver.

Corrected Text
--------------
   If the F bit is set to one (see below), then the NAI is absent
   and the NT field MUST be zero; the receiver validates NT, F, S
   and Length as described in Section 5.2.1.

Notes
-----
   Erratum 6753 corrects "zero" to "one" but keeps "MUST be
   ignored", which conflicts with Section 5.2.1 (a PCC MUST check
   that NT, F, S and Length are consistent and reject F = 1 with NT
   not 0) and with the F flag definition ("The F bit MUST be set to
   1 if NT=0; otherwise, it MUST be set to zero").
```

### Other RFCs in this area {#ra_pcep_other}

Mechanical checks only, no hit: RFC 5441 (A Backward-Recursive PCE-Based Computation (BRPC) Procedure to Compute), RFC 5520 (Preserving Topology Confidentiality in Inter-Domain Path Computation U), RFC 5521 (Extensions to the Path Computation Element Communication Protocol (PCE), RFC 5541 (Encoding of Objective Functions in the Path Computation Element Commun), RFC 5886 (A Set of Monitoring Tools for Path Computation Element (PCE)-Based Arc), RFC 6805 (The Application of the Path Computation Element Architecture to the De), RFC 7897 (Domain Subobjects for the Path Computation Element Communication Proto), RFC 8232 (Optimizations of Label Switched Path State Synchronization Procedures ), RFC 8233 (Extensions to the Path Computation Element Communication Protocol (PCE), RFC 8306 (Extensions to the Path Computation Element Communication Protocol (PCE), RFC 8408 (Conveying Path Setup Type in PCE Communication Protocol (PCEP) Message), RFC 8623 (Stateful Path Computation Element (PCE) Protocol Extensions for Usage ), RFC 8685 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 8697 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 8741 (Ability for a Stateful Path Computation Element (PCE) to Request and O), RFC 8745 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 8751 (Hierarchical Stateful Path Computation Element (PCE)), RFC 8779 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 8786 (Updated Rules for Processing Stateful PCE Request Parameters Flags), RFC 8800 (Path Computation Element Communication Protocol (PCEP) Extension for L), RFC 9005 (Path Computation Element Communication Protocol (PCEP) Extension for A), RFC 9050 (Path Computation Element Communication Protocol (PCEP) Procedures and ), RFC 9059 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 9357 (Label Switched Path (LSP) Object Flag Extension for Stateful PCE), RFC 9488 (Local Protection Enforcement in the Path Computation Element Communica), RFC 9603 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 9604 (Carrying Binding Label/SID in PCE-Based Networks), RFC 9757 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 9862 (Path Computation Element Communication Protocol (PCEP) Extensions for ), RFC 9933 (Carrying SR-Algorithm in Path Computation Element Communication Protoc).

## Multicast: PIM, IGMP, MLD and MVPN {#ra_mcast}

22 RFCs in this area; 6 findings, 1 of them proposed errata.

### RFC 2236: Internet Group Management Protocol, Version 2 {#ra_rfc2236}

Reading: mechanical checks only. Errata: errata not checked (obsoleted by RFC 3376, itself obsoleted by RFC 9776). Updates: RFC 1112.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0085 | 2, 3 | "as discussed in section 7.8.  It also allows tuning of the burstiness of IGMP traffic on a subnet, as discussed in section 7.3." | RFC 2236 has no section 7.8 or 7.3 in that sense (7 is the router state diagram; the timers are 8.8 and 8.3), and "described in section 1.4" a few lines earlier refers to the Group Address field, which is section 2.4. References from a draft numbering. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0085 (RFC 2236, Section 2, 3; type: Technical):

```
Original Text
-------------
   as discussed in section 7.8.  It also allows tuning of the
   burstiness of IGMP traffic on a subnet, as discussed in section
   7.3.

Corrected Text
--------------
   as discussed in section 8.8.  It also allows tuning of the
   burstiness of IGMP traffic on a subnet, as discussed in section
   8.3.

Notes
-----
   Section 7 is the router state diagram; the Last Member Query
   Interval and Query Response Interval are Sections 8.8 and 8.3.
   Likewise "described in section 1.4" (Group Address) should be
   Section 2.4. RFC 2236 is obsoleted, so this is recorded for
   completeness only.
```

### RFC 5059: Bootstrap Router (BSR) Mechanism for Protocol Independent Multicast (PIM) {#ra_rfc5059}

Reading: partial reading. Errata: errata checked: 3 (1321, 1322 verified editorial; 1323 held editorial). Obsoletes: RFC 2362. Updates: RFC 4601.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0086 | 3.1, 3.3 | "group range in the message, which can be any sub-range of 224/4." | Abbreviated prefix; 224.0.0.0/4 is meant. Erratum 1322 corrects the fragment RP count range ("1..m" for "1..n"). | editorial | 1321 (Verified) |

### RFC 6514: BGP Encodings and Procedures for Multicast in MPLS/BGP IP VPNs {#ra_rfc6514}

Reading: targeted reading of the relevant sections. Errata: errata checked: 3 (all held: 5724 technical, 3801 and 3802 editorial). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0087 | 11.1.3 | "The Source AS field in the C-multicast route is set to value of the Originating Router's IP Address field of the found Intra-AS I-PMSI A-D route." | The Source AS field is 4 octets; with RFC 6515 the Originating Router's IP Address may be a 16-octet IPv6 address, which cannot be stored. The held erratum limits the rule to IPv4 Originating Router addresses; nothing says what to use for IPv6. | error | 5724 (Held) |
| RA-0088 | 4.1, 4.2 | "Usage of Intra-AS I-PMSI A-D routes is described in Section 9.2." | The two references are swapped: intra-AS usage is section 9.1, inter-AS usage 9.2. | editorial | 3801, 3802 (Held) |

### RFC 7761: Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised) {#ra_rfc7761}

Reading: targeted reading of the relevant sections. Errata: errata checked: 4 (5342 verified technical, 7857 verified editorial, 5367 held technical, 5343 rejected). Obsoletes: RFC 4601.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0089 | 4.4.2, 4.11 | "set KeepaliveTimer(S,G) to RP_Keepalive_Period;" | The RP pseudocode sets the (S,G) Keepalive Timer to RP_Keepalive_Period alone, while section 4.11 says the KAT "is set to max(Keepalive_Period, RP_Keepalive_Period) when a Register-Stop is sent". With default timers RP_Keepalive_Period (3 x Register_Suppression_Time + Register_Probe_Time = 185 s) is shorter than Keepalive_Period (210 s), so the two readings differ. The verified erratum makes the pseudocode use the maximum; 5367 asks for the same in the restart value. | contradiction | 5342 (Verified), 5367 (Held), 5343 (Rejected) |
| RA-0090 | 4.6.5 | "(AssertWinnerMetric(S,G,I) is better than spt_assert_metric(S,I) )" | Unbalanced / excess parentheses in the lost_assert(S,G,I) pseudocode; no change of meaning. | editorial | 7857 (Verified) |

### Other RFCs in this area {#ra_mcast_other}

Mechanical checks only, no hit: RFC 2710 (Multicast Listener Discovery (MLD) for IPv6), RFC 3376 (Internet Group Management Protocol, Version 3), RFC 3810 (Multicast Listener Discovery Version 2 (MLDv2) for IPv6), RFC 4604 (Using Internet Group Management Protocol Version 3 (IGMPv3) and Multic), RFC 4607 (Source-Specific Multicast for IP), RFC 4610 (Anycast-RP Using Protocol Independent Multicast (PIM)), RFC 5015 (Bidirectional Protocol Independent Multicast (BIDIR-PIM)), RFC 5771 (IANA Guidelines for IPv4 Multicast Address Assignments), RFC 6037 (Cisco Systems' Solution for Multicast in BGP/MPLS IP VPNs), RFC 6513 (Multicast in MPLS/BGP IP VPNs), RFC 6515 (IPv4 and IPv6 Infrastructure Addresses in BGP Updates for Multicast VP), RFC 6625 (Wildcards in Multicast VPN Auto-Discovery Routes), RFC 7385 (IANA Registry for P-Multicast Service Interface (PMSI) Tunnel Type Cod), RFC 7442 (Carrying Protocol Independent Multicast - Sparse Mode (PIM-SM) in Any-), RFC 7524 (Inter-Area Point-to-Multipoint (P2MP) Segmented Label Switched Paths (), RFC 9026 (Multicast VPN Fast Upstream Failover), RFC 9776 (Internet Group Management Protocol, Version 3), RFC 9777 (Multicast Listener Discovery Version 2 (MLDv2) for IPv6).

## BFD, LSP ping, measurement and time {#ra_oam}

30 RFCs in this area; 10 findings, 2 of them proposed errata.

### RFC 5357: A Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc5357}

Reading: partial reading. Errata: errata checked: 13 (6 verified, 4 of them technical; 6 held; 1 rejected). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0091 | 4.1.2, 4.2.1 | "unauthenticated mode is 41 octets, and 104 octets in both" | The minimum authenticated / encrypted TWAMP-Test packet is 112 octets, not 104, and sender padding is at least 64 octets, not 56 ("least 56 octets"). Implementations sizing buffers or validating lengths from the text reject valid packets. | error | 5045, 5046 (Verified) |
| RA-0092 | 8.1, 8.2 | "document.  Thus, this registry may contain sixteen possible values." | The Command Number field is one octet, so the registry has 256 values. | error | 1593 (Verified) |

### RFC 5880: Bidirectional Forwarding Detection (BFD) {#ra_rfc5880}

Reading: targeted reading of the relevant sections. Errata: errata checked: 8 (4 verified: 2530, 7082, 7083 technical, 6926 editorial; 3 held: 5205, 7240 technical, 4410 editorial; 1 rejected). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0093 | 6.7.3, 6.7.4 | "Otherwise (bfd.AuthSeqKnown is 0), bfd.AuthSeqKnown MUST be set to 1, and bfd.RcvAuthSeq MUST be set to the value of the received Sequence Number field." | In the MD5 and SHA1 procedures the sequence variables are updated before the digest is checked, so a forged packet with a bad digest can still move bfd.RcvAuthSeq and make later genuine packets fall outside the window. The errata move the update after a successful check. Security gap in the original text. | error | 7082, 7083 (Verified) |
| RA-0094 | 6.8.4 | "Detection Time passes without receiving a BFD Control packet from the remote system, and bfd.SessionState is Init or Up, the session has gone down" | In Down state an expired Detection Time changes nothing here, although 6.8.1 requires bfd.RemoteDiscr to be zeroed whenever a Detection Time passes without a valid packet, so the timer must still run in Down. The held erratum would drop the "Init or Up" condition and always set Diag 1; that is not yet the text. | ambiguity | 5205 (Held) |
| RA-0095 | 6.8.1 | "The diagnostic code specifying the reason for the most recent change in the local session state." | Whether bfd.LocalDiag returns to 0 when the session comes Up again is not said; implementations differ (some keep the last failure reason while Up). The erratum was held for a future revision without text. | ambiguity | 7240 (Held) |

### RFC 5884: Bidirectional Forwarding Detection (BFD) for MPLS Label Switched Paths (LSPs) {#ra_rfc5884}

Reading: targeted reading of the relevant sections. Errata: errata checked: 3 (5085 verified technical; 5087, 5088 held editorial). Updates: RFC 1122.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0096 | 6 | "The egress LSR MAY respond with an LSP Ping Echo reply message that carries the local discriminator assigned by it for the BFD session." | The MAY can be read as making the Echo Reply itself optional, while RFC 8029 requires the egress to report the verification result; the erratum makes only the discriminator optional. RFC 7726 also clarifies the bootstrap procedure. | ambiguity | 5085 (Verified) |
| RA-0097 | 7 | "from the 0:0:0:0:0:FFFF:7F00/104 range for IPv6 with the following" | "0:0:0:0:0:FFFF:7F00/104" has only seven groups and is not a valid IPv6 prefix; 0:0:0:0:0:FFFF:7F00:0/104 (::ffff:127.0.0.0/104) is meant. Erratum 5088 also corrects "[5085]" to RFC 5885. | editorial | 5087 (Held) |

### RFC 6038: Two-Way Active Measurement Protocol (TWAMP) Reflect Octets and Symmetrical Size Features {#ra_rfc6038}

Reading: mechanical checks only. Errata: errata not checked. Updates: RFC 5357.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0098 | 4.3 | "Section 4.1.2 defines how Server octets MUST be included in the TWAMP-Test packet padding" | This document has no section 4.1.2 (section 4.1 has no subsections); the Reflect Octets packet formats are in 5.1.2. The reference may instead mean RFC 5357 4.1.2 (sender padding), but the sentence does not name that document. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0098 (RFC 6038, Section 4.3; type: Editorial):

```
Original Text
-------------
   o  Section 4.1.2 defines how Server octets MUST be included in
   the

Corrected Text
--------------
   o  Section 5.1.2 defines how Server octets MUST be included in
   the

Notes
-----
   There is no Section 4.1.2 in this document. Section 5.1.2
   ("Reflect Octets: Packet Formats and Contents") describes the
   padding contents. If RFC 5357 Section 4.1.2 was meant, the
   reference should say so.
```

### RFC 6426: MPLS On-Demand Connectivity Verification and Route Tracing {#ra_rfc6426}

Reading: mechanical checks only. Errata: errata not checked. Updates: RFC 4379.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0099 | 7.2 | "22       Static LSP              this document (Section 2.4.1)" | The IANA table points to sections 2.4.1 and 2.4.2, which do not exist; the Static LSP and Static Pseudowire sub-TLVs are defined in 2.3.1 and 2.3.2. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0099 (RFC 6426, Section 7.2; type: Technical):

```
Original Text
-------------
   22       Static LSP              this document (Section 2.4.1)
   23       Static Pseudowire       this document (Section 2.4.2)

Corrected Text
--------------
   22       Static LSP              this document (Section 2.3.1)
   23       Static Pseudowire       this document (Section 2.3.2)

Notes
-----
   Sections 2.4.1 and 2.4.2 do not exist; the sub-TLVs are defined
   in Sections 2.3.1 and 2.3.2. The IANA registry may carry the same
   wrong references.
```

### RFC 7130: Bidirectional Forwarding Detection (BFD) on Link Aggregation Group (LAG) Interfaces {#ra_rfc7130}

Reading: partial reading. Errata: errata checked: 2 (both held, editorial IEEE names). 

Nothing notable found.

### RFC 8029: Detecting Multiprotocol Label Switched (MPLS) Data-Plane Failures {#ra_rfc8029}

Reading: targeted reading of the relevant sections. Errata: errata checked: 5 (7639 verified technical, 7892 verified editorial, 8788 reported technical, 5102 and 5103 held editorial). Obsoletes: RFC 4379, RFC 6424, RFC 6829, RFC 7537. Updates: RFC 1122.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0100 | 3.4, 3.7, 3.8, A.2 | "If an LSR does not know the IP address of its neighbor, then it MUST set the Address Type to either IPv4 Unnumbered or IPv6 Unnumbered." | "IPv6 Unnumbered" (Router ID plus interface index) has no defined IPv6 Router ID semantics; the open erratum proposes deprecating the IPv6 Unnumbered address types and also reports a K-octets mismatch in Appendix A.2. Until it is resolved, what to send and accept for IPv6 unnumbered links is unclear. | ambiguity | 8788 (Reported) |

### RFC 8762: Simple Two-Way Active Measurement Protocol {#ra_rfc8762}

Reading: partial reading. Errata: errata: none for RFC 8762 found in search; RFC 8972 has 8591 (verified, editorial). 

Nothing notable found.

### Other RFCs in this area {#ra_oam_other}

Mechanical checks only, no hit: RFC 2330 (Advanced Network & Services), RFC 4656 (A One-way Active Measurement Protocol (OWAMP)), RFC 5618 (Mixed Security Mode for the Two-Way Active Measurement Protocol (TWAMP), RFC 5881 (Bidirectional Forwarding Detection (BFD) for IPv4 and IPv6 (Single Hop), RFC 5882 (Generic Application of Bidirectional Forwarding Detection (BFD)), RFC 5883 (Bidirectional Forwarding Detection (BFD) for Multihop Paths), RFC 5885 (Bidirectional Forwarding Detection (BFD) for the Pseudowire Virtual Ci), RFC 5905 (Network Time Protocol Version 4: Protocol and Algorithms Specification), RFC 5938 (Individual Session Control Feature for the Two-Way Active Measurement ), RFC 6425 (Detecting Data-Plane Failures in Point-to-Multipoint MPLS - Extensions), RFC 7110 (Return Path Specified Label Switched Path (LSP) Ping), RFC 7506 (IPv6 Router Alert Option for MPLS Operations, Administration, and Main), RFC 7679 (A One-Way Delay Metric for IP Performance Metrics (IPPM)), RFC 7680 (A One-Way Loss Metric for IP Performance Metrics (IPPM)), RFC 7717 (IKEv2-Derived Shared Secret Key for the One-Way Active Measurement Pro), RFC 7726 (Clarifying Procedures for Establishing BFD Sessions for MPLS Label Swi), RFC 7750 (Differentiated Service Code Point and Explicit Congestion Notification), RFC 7820 (UDP Checksum Complement in the One-Way Active Measurement Protocol (OW), RFC 8186 (Support of the IEEE 1588 Timestamp Format in a Two-Way Active Measurem), RFC 8287 (Label Switched Path (LSP) Ping/Traceroute for Segment Routing (SR) IGP), RFC 8545 (Well-Known Port Assignments for the One-Way Active Measurement Protoco), RFC 8972 (Simple Two-Way Active Measurement Protocol Optional Extensions).

## IP, ICMP, neighbour discovery, transport and security {#ra_ip}

77 RFCs in this area; 10 findings, 0 of them proposed errata.

### RFC 1191: Path MTU Discovery {#ra_rfc1191}

Reading: mechanical checks only. Errata: errata not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0101 | 3, 6.3 | "A host MUST not increase its estimate of the Path MTU in response to" | Mixed-case "MUST not" (three times in RFC 1191; also RFC 1812 "A router MUST not believe any ARP reply"). The intent is MUST NOT; listed once here for the whole group (see Method). | editorial | not checked |

### RFC 1812: Requirements for IP Version 4 Routers {#ra_rfc1812}

Reading: targeted reading of the relevant sections. Errata: errata checked: 5 (2 verified, 2 held, 1 reported; all editorial). Obsoletes: RFC 1716, RFC 1009.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0102 | 4.3.3.4 | "is reduced to 0, the requirements of section [5.2.3.8] apply." | Section 5.2.3.8 does not cover TTL expiry; the TTL rules are in 5.3.1. | error | 5553 (Held) |
| RA-0103 | 4.3.3.6 | "an ICMP Echo Request datagram at least as the maximum of 576 and the" | Missing words: "at least as large as the maximum of 576 and the MTUs of the connected networks". | editorial | 2704 (Held) |

### RFC 4443: Internet Control Message Protocol (ICMPv6) for the Internet Protocol Version 6 (IPv6) Specification {#ra_rfc4443}

Reading: partial reading. Errata: errata checked: 6 (1 reported technical, 1 held technical, 3 held editorial, 1 rejected). Obsoletes: RFC 2463. Updates: RFC 2780.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0104 | 3.1 | "beyond the scope of the source address, the Code field is set to 2." | "Scope" is used where RFC 4007 defines scope zones; read literally, Code 2 would apply to any global destination when the source is link-local, rather than only when forwarding would cross the source's zone boundary. The report is still open; a related report on Codes 0 and 6 was rejected. | ambiguity | 6153 (Reported), 4445 (Rejected) |

### RFC 4861: Neighbor Discovery for IP version 6 (IPv6) {#ra_rfc4861}

Reading: targeted reading of the relevant sections. Errata: errata checked: 9 (5 verified, 4 of them technical; 3 held, 2 technical; 1 rejected). Obsoletes: RFC 2461.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0105 | 6.2.1 | "MUST be no less than 3 seconds and no greater than .75 * MaxRtrAdvInterval.  Default: 0.33 * MaxRtrAdvInterval If MaxRtrAdvInterval >= 9 seconds; otherwise, the Default is MaxRtrAdvInterval." | For MaxRtrAdvInterval below 9 seconds the stated default (equal to MaxRtrAdvInterval) violates the MUST in the same definition (at most 0.75 x MaxRtrAdvInterval). The erratum makes the default 0.75 x MaxRtrAdvInterval. | contradiction | 3154 (Verified) |
| RA-0106 | Appendix C | "This appendix contains a summary of the rules specified in Sections 7.2 and 7.3." | The summary table disagrees with 7.2.5: it has no row for a solicited NA without a target link-layer address in PROBE (so a reachable neighbour can be discarded), and labels a Solicited = 1 row INCOMPLETE where PROBE is meant. An implementation built from the table rather than 7.2.5 gets NUD wrong. | error | 2709 (Verified), 2797 (Held) |

### RFC 5082: The Generalized TTL Security Mechanism (GTSM) {#ra_rfc5082}

Reading: partial reading. Errata: errata: no errata page in search results. Obsoletes: RFC 3682.

Nothing notable found.

### RFC 5925: The TCP Authentication Option {#ra_rfc5925}

Reading: targeted reading of the relevant sections. Errata: errata checked: 7 (3 verified technical, 1 reported technical, 1 held editorial, 2 rejected). Obsoletes: RFC 2385.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0107 | 6.2 | "&& (RCV.PREV_SEQ > 0x7fff) && (SEG.SEQ < 0x7fff)) {" | The Sequence Number Extension pseudocode compares 32-bit sequence numbers with a 16-bit midpoint; it must be 0x7fffffff. Taken literally the SNE increments at the wrong time and MACs fail after the first 2^15 octets of a connection crossing the midpoint. | error | 5672 (Verified) |
| RA-0108 | 7.6 | "This leaves 40 bytes for options, of which 15 are expected in current ... TCP-AO consumes 16 bytes, leaving 9 bytes for additional SYN options" | MSS was left out of the SYN option count, so the stated room left for other options is wrong (the erratum: 21 octets left, 5 for other SYN options). | error | 4365 (Verified) |
| RA-0109 | 5.1 (Figure 6) | "\|      Zero       \|   Next Header   \|" | The figure draws Zero and Next Header as 2 octets each; they are 3 and 1. An implementer building the MAC input from the figure computes a wrong MAC for IPv6. | editorial | 6406 (Held) |
| RA-0110 | 5.2 | "remote ISN), and the destination (remote) ISN is unknown (and so" | In the receive-SYN traffic key both ISNs are called "remote"; the destination ISN is the local one. The erratum is still open. | error | 7899 (Reported) |

### Other RFCs in this area {#ra_ip_other}

Mechanical checks only, no hit: RFC 768 (User Datagram Protocol), RFC 791 (INTERNET PROTOCOL), RFC 792 (Internet Control Message Protocol), RFC 826 (An Ethernet Address Resolution Protocol -- or -- Converting Network Pr), RFC 1042 (A Standard for the Transmission of IP Datagrams over IEEE 802 Networks), RFC 1071 (Computing the Internet Checksum), RFC 1122 (Requirements for Internet Hosts -- Communication Layers), RFC 1321 (The MD5 Message-Digest Algorithm), RFC 1624 (Computation of the Internet Checksum via Incremental Update), RFC 1858 (Security Considerations for IP Fragment Filtering), RFC 1982 (Serial Number Arithmetic), RFC 2104 (HMAC: Keyed-Hashing for Message Authentication), RFC 2113 (IP Router Alert Option), RFC 2202 (Test Cases for HMAC-MD5 and HMAC-SHA-1), RFC 2253 (Lightweight Directory Access Protocol (v3): UTF-8 String Representatio), RFC 2464 (Transmission of IPv6 Packets over Ethernet Networks), RFC 2711 (IPv6 Router Alert Option), RFC 2863 (The Interfaces Group MIB), RFC 3021 (Using 31-Bit Prefixes on IPv4 Point-to-Point Links), RFC 3174 (US Secure Hash Algorithm 1 (SHA1)), RFC 3339 (Date and Time on the Internet: Timestamps), RFC 3629 (UTF-8, a transformation format of ISO 10646), RFC 3971 (SEcure Neighbor Discovery (SEND)), RFC 4231 (Identifiers and Test Vectors for HMAC-SHA-224, HMAC-SHA-256, HMAC-SHA-), RFC 4291 (IP Version 6 Addressing Architecture), RFC 4648 (The Base16, Base32, and Base64 Data Encodings), RFC 4862 (IPv6 Stateless Address Autoconfiguration), RFC 4868 (Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec), RFC 4884 (Extended ICMP to Support Multi-Part Messages), RFC 5116 (An Interface and Algorithms for Authenticated Encryption), RFC 5227 (IPv4 Address Conflict Detection), RFC 5246 (The Transport Layer Security (TLS) Protocol Version 1.2), RFC 5280 (Internet X.509 Public Key Infrastructure Certificate and Certificate R), RFC 5424 (The Syslog Protocol), RFC 5480 (Elliptic Curve Cryptography Subject Public Key Information), RFC 5758 (Internet X.509 Public Key Infrastructure: Additional Algorithms and Id), RFC 5869 (HMAC-based Extract-and-Expand Key Derivation Function (HKDF)), RFC 5926 (Cryptographic Algorithms for the TCP Authentication Option (TCP-AO)), RFC 5952 (A Recommendation for IPv6 Address Text Representation), RFC 6040 (Tunnelling of Explicit Congestion Notification), RFC 6066 (Transport Layer Security (TLS) Extensions: Extension Definitions), RFC 6125 (Representation and Verification of Domain-Based Application Service Id), RFC 6234 (US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF)), RFC 6398 (IP Router Alert Considerations and Usage), RFC 6454 (The Web Origin Concept), RFC 6455 (The WebSocket Protocol), RFC 6583 (Operational Neighbor Discovery Problems), RFC 6890 (Special-Purpose IP Address Registries), RFC 6901 (JavaScript Object Notation (JSON) Pointer), RFC 6979 (Deterministic Usage of the Digital Signature Algorithm (DSA) and Ellip), RFC 6980 (Security Implications of IPv6 Fragmentation with IPv6 Neighbor Discove), RFC 7112 (Implications of Oversized IPv6 Header Chains), RFC 7525 (Recommendations for Secure Use of Transport Layer Security (TLS) and D), RFC 7748 (Elliptic Curves for Security), RFC 8017 (PKCS #1: RSA Cryptography Specifications Version 2.2), RFC 8032 (Edwards-Curve Digital Signature Algorithm (EdDSA)), RFC 8200 (Internet Protocol, Version 6 (IPv6) Specification), RFC 8201 (Path MTU Discovery for IP version 6), RFC 8259 (The JavaScript Object Notation (JSON) Data Interchange Format), RFC 8439 (ChaCha20 and Poly1305 for IETF Protocols), RFC 8446 (The Transport Layer Security (TLS) Protocol Version 1.3), RFC 8448 (Example Handshake Traces for TLS 1.3), RFC 9000 (QUIC: A UDP-Based Multiplexed and Secure Transport), RFC 9001 (Using TLS to Secure QUIC), RFC 9002 (QUIC Loss Detection and Congestion Control), RFC 9110 (HTTP Semantics), RFC 9112 (HTTP/1.1), RFC 9114 (HTTP/3), RFC 9204 (QPACK: Field Compression for HTTP/3), RFC 9325 (Recommendations for Secure Use of Transport Layer Security (TLS) and D), RFC 9525 (Service Identity in TLS).

## Index by RFC {#ra_index}

Every RFC reviewed. Depth: deep = targeted reading of the relevant sections; part = partial reading; scan = mechanical checks only.

| RFC | Title | Area | Depth | Findings | Proposed errata |
|---|---|---|---|---|---|
| RFC 768 | User Datagram Protocol | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 791 | INTERNET PROTOCOL | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 792 | Internet Control Message Protocol | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 826 | An Ethernet Address Resolution Protocol -- or -- Converting Network Protocol Addresses to  | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1042 | A Standard for the Transmission of IP Datagrams over IEEE 802 Networks | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1071 | Computing the Internet Checksum | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1122 | Requirements for Internet Hosts -- Communication Layers | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 1142](#ra_rfc1142) | OSI IS-IS Intra-domain Routing Protocol | [IS-IS](#ra_isis) | deep | 0 | 0 |
| [RFC 1191](#ra_rfc1191) | Path MTU Discovery | [IP](#ra_ip) | scan | 1 | 0 |
| [RFC 1195](#ra_rfc1195) | Use of OSI IS-IS for Routing in TCP/IP and Dual Environments | [IS-IS](#ra_isis) | deep | 2 | 0 |
| RFC 1321 | The MD5 Message-Digest Algorithm | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1624 | Computation of the Internet Checksum via Incremental Update | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 1812](#ra_rfc1812) | Requirements for IP Version 4 Routers | [IP](#ra_ip) | deep | 2 | 0 |
| RFC 1858 | Security Considerations for IP Fragment Filtering | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1982 | Serial Number Arithmetic | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 1997 | BGP Communities Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 2042 | Registering New BGP Attribute Types | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 2104 | HMAC: Keyed-Hashing for Message Authentication | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 2113 | IP Router Alert Option | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 2202 | Test Cases for HMAC-MD5 and HMAC-SHA-1 | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 2205](#ra_rfc2205) | Resource ReSerVation Protocol (RSVP) -- Version 1 Functional Specification | [RSVP](#ra_rsvp) | deep | 1 | 0 |
| RFC 2209 | Resource ReSerVation Protocol (RSVP) -- Version 1 Message Processing Rules | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 2210 | The Use of RSVP with IETF Integrated Services | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 2211 | Specification of the Controlled-Load Network Element Service | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 2212 | Specification of Guaranteed Quality of Service | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 2236](#ra_rfc2236) | Internet Group Management Protocol, Version 2 | [Multicast](#ra_mcast) | scan | 1 | 1 |
| RFC 2253 | Lightweight Directory Access Protocol (v3): UTF-8 String Representation of Distinguished N | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 2330 | Advanced Network & Services | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 2385 | Protection of BGP Sessions via the TCP MD5 Signature Option | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 2464 | Transmission of IPv6 Packets over Ethernet Networks | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 2545 | Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 2710 | Multicast Listener Discovery (MLD) for IPv6 | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 2711 | IPv6 Router Alert Option | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 2747](#ra_rfc2747) | RSVP Cryptographic Authentication | [RSVP](#ra_rsvp) | deep | 1 | 0 |
| RFC 2750 | RSVP Extensions for Policy Control | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 2863 | The Interfaces Group MIB | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 2918 | Route Refresh Capability for BGP-4 | [BGP](#ra_bgp) | scan | 0 | 0 |
| [RFC 2961](#ra_rfc2961) | RSVP Refresh Overhead Reduction Extensions | [RSVP](#ra_rsvp) | part | 0 | 0 |
| RFC 3021 | Using 31-Bit Prefixes on IPv4 Point-to-Point Links | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 3032](#ra_rfc3032) | MPLS Label Stack Encoding | [MPLS/LDP](#ra_ldp) | deep | 2 | 0 |
| RFC 3036 | LDP Specification | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 3097 | RSVP Cryptographic Authentication -- Updated Message Type Value | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 3174 | US Secure Hash Algorithm 1 (SHA1) | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 3175 | Aggregation of RSVP for IPv4 and IPv6 Reservations | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 3209](#ra_rfc3209) | RSVP-TE: Extensions to RSVP for LSP Tunnels | [RSVP](#ra_rsvp) | deep | 2 | 0 |
| [RFC 3212](#ra_rfc3212) | Constraint-Based LSP Setup using LDP | [MPLS/LDP](#ra_ldp) | scan | 1 | 1 |
| RFC 3270 | Multi-Protocol Label Switching (MPLS) Support of Differentiated Services | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 3339 | Date and Time on the Internet: Timestamps | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 3358 | Optional Checksums in Intermediate System to Intermediate System (ISIS) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 3376 | Internet Group Management Protocol, Version 3 | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 3429 | Assignment of the 'OAM Alert Label' for Multiprotocol Label Switching Architecture (MPLS)  | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 3443 | Time To Live (TTL) Processing in Multi-Protocol Label Switching (MPLS) Networks | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 3468 | The Multiprotocol Label Switching (MPLS) Working Group decision on MPLS signaling protocol | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 3471 | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Functional Description | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 3472 | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Constraint-based Routed Label | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 3473](#ra_rfc3473) | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Resource ReserVation Protocol | [RSVP](#ra_rsvp) | deep | 3 | 0 |
| RFC 3475 | Documentation of IANA assignments for Constraint-Based LSP setup using LDP (CR-LDP) Extens | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 3477 | Signalling Unnumbered Links in Resource ReSerVation Protocol - Traffic Engineering (RSVP-T | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 3478](#ra_rfc3478) | Graceful Restart Mechanism for Label Distribution Protocol | [MPLS/LDP](#ra_ldp) | part | 0 | 0 |
| RFC 3479 | Fault Tolerance for the Label Distribution Protocol (LDP) | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 3629 | UTF-8, a transformation format of ISO 10646 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 3630 | Traffic Engineering (TE) Extensions to OSPF Version 2 | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 3719 | Recommendations for Interoperable Networks using Intermediate System to Intermediate Syste | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 3765 | NOPEER Community for Border Gateway Protocol (BGP) Route Scope Control | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 3787 | Recommendations for Interoperable IP Networks using Intermediate System to Intermediate Sy | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 3810 | Multicast Listener Discovery Version 2 (MLDv2) for IPv6 | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 3906 | Calculating Interior Gateway Protocol (IGP) Routes Over Traffic Engineering Tunnels | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 3971 | SEcure Neighbor Discovery (SEND) | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 3988 | Maximum Transmission Unit Signalling Extensions for the Label Distribution Protocol | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 4090](#ra_rfc4090) | Fast Reroute Extensions to RSVP-TE for LSP Tunnels | [RSVP](#ra_rsvp) | deep | 3 | 0 |
| RFC 4105 | Requirements for Inter-Area MPLS Traffic Engineering | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4124 | Protocol Extensions for Support of Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4125 | Maximum Allocation Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4126 | Max Allocation with Reservation Bandwidth Constraints Model for Diffserv-aware MPLS Traffi | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4127 | Russian Dolls Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4206 | Label Switched Paths (LSP) Hierarchy with Generalized Multi-Protocol Label Switching (GMPL | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4231 | Identifiers and Test Vectors for HMAC-SHA-224, HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-51 | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 4271](#ra_rfc4271) | A Border Gateway Protocol 4 (BGP-4) | [BGP](#ra_bgp) | deep | 11 | 1 |
| RFC 4291 | IP Version 6 Addressing Architecture | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 4360 | BGP Extended Communities Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| [RFC 4364](#ra_rfc4364) | BGP/MPLS IP Virtual Private Networks (VPNs) | [BGP](#ra_bgp) | deep | 2 | 0 |
| [RFC 4385](#ra_rfc4385) | Pseudowire Emulation Edge-to-Edge (PWE3) Control Word for Use over an MPLS PSN | [PW](#ra_pw) | part | 1 | 0 |
| [RFC 4443](#ra_rfc4443) | Internet Control Message Protocol (ICMPv6) for the Internet Protocol Version 6 (IPv6) Spec | [IP](#ra_ip) | part | 1 | 0 |
| RFC 4444 | Management Information Base for Intermediate System to Intermediate System (IS-IS) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 4446 | IANA Allocations for Pseudowire Edge to Edge Emulation (PWE3) | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 4447 | Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 4448 | Encapsulation Methods for Transport of Ethernet over MPLS Networks | [PW](#ra_pw) | scan | 0 | 0 |
| [RFC 4456](#ra_rfc4456) | BGP Route Reflection: An Alternative to Full Mesh Internal BGP (IBGP) | [BGP](#ra_bgp) | deep | 2 | 0 |
| RFC 4486 | Subcodes for BGP Cease Notification Message | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 4561 | Definition of a Record Route Object (RRO) Node-Id Sub-Object | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4604 | Using Internet Group Management Protocol Version 3 (IGMPv3) and Multicast Listener Discove | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 4607 | Source-Specific Multicast for IP | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 4610 | Anycast-RP Using Protocol Independent Multicast (PIM) | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 4623 | Pseudowire Emulation Edge-to-Edge (PWE3) Fragmentation and Reassembly | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 4648 | The Base16, Base32, and Base64 Data Encodings | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 4656 | A One-way Active Measurement Protocol (OWAMP) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 4659 | BGP-MPLS IP Virtual Private Network (VPN) Extension for IPv6 VPN | [BGP](#ra_bgp) | scan | 0 | 0 |
| [RFC 4724](#ra_rfc4724) | Graceful Restart Mechanism for BGP | [BGP](#ra_bgp) | deep | 4 | 1 |
| RFC 4726 | A Framework for Inter-Domain Multiprotocol Label Switching Traffic Engineering | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 4760](#ra_rfc4760) | Multiprotocol Extensions for BGP-4 | [BGP](#ra_bgp) | deep | 4 | 0 |
| RFC 4761 | Virtual Private LAN Service (VPLS) Using BGP for Auto-Discovery and Signaling | [PW](#ra_pw) | scan | 0 | 0 |
| [RFC 4762](#ra_rfc4762) | Virtual Private LAN Service (VPLS) Using Label Distribution Protocol (LDP) Signaling | [PW](#ra_pw) | deep | 1 | 0 |
| RFC 4798 | Connecting IPv6 Islands over IPv4 MPLS Using IPv6 Provider Edge Routers (6PE) | [BGP](#ra_bgp) | scan | 0 | 0 |
| [RFC 4861](#ra_rfc4861) | Neighbor Discovery for IP version 6 (IPv6) | [IP](#ra_ip) | deep | 2 | 0 |
| RFC 4862 | IPv6 Stateless Address Autoconfiguration | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 4868 | Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 4872 | RSVP-TE Extensions in Support of End-to-End Generalized Multi-Protocol Label Switching (GM | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4873 | GMPLS Segment Recovery | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4874 | Exclude Routes - Extension to Resource ReserVation Protocol-Traffic Engineering (RSVP-TE) | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 4875](#ra_rfc4875) | Extensions to Resource Reservation Protocol - Traffic Engineering (RSVP-TE) for Point-to-M | [RSVP](#ra_rsvp) | deep | 2 | 0 |
| RFC 4884 | Extended ICMP to Support Multi-Part Messages | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 4920 | Crankback Signaling Extensions for MPLS and GMPLS RSVP-TE | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 4950 | ICMP Extensions for Multiprotocol Label Switching | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5003 | Attachment Individual Identifier (AII) Types for Aggregation | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 5004 | Avoid BGP Best Path Transitions from One External to Another | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5015 | Bidirectional Protocol Independent Multicast (BIDIR-PIM) | [Multicast](#ra_mcast) | scan | 0 | 0 |
| [RFC 5036](#ra_rfc5036) | LDP Specification | [MPLS/LDP](#ra_ldp) | deep | 4 | 1 |
| [RFC 5059](#ra_rfc5059) | Bootstrap Router (BSR) Mechanism for Protocol Independent Multicast (PIM) | [Multicast](#ra_mcast) | part | 1 | 0 |
| RFC 5063 | Extensions to GMPLS Resource Reservation Protocol (RSVP) Graceful Restart | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5065 | Autonomous System Confederations for BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| [RFC 5082](#ra_rfc5082) | The Generalized TTL Security Mechanism (GTSM) | [IP](#ra_ip) | part | 0 | 0 |
| RFC 5085 | Pseudowire Virtual Circuit Connectivity Verification (VCCV): A Control Channel for Pseudow | [PW](#ra_pw) | scan | 0 | 0 |
| [RFC 5088](#ra_rfc5088) | OSPF Protocol Extensions for Path Computation Element (PCE) Discovery | [PCEP](#ra_pcep) | scan | 1 | 1 |
| RFC 5089 | IS-IS Protocol Extensions for Path Computation Element (PCE) Discovery | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5116 | An Interface and Algorithms for Authenticated Encryption | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 5120](#ra_rfc5120) | M-ISIS: Multi Topology (MT) Routing in Intermediate System to Intermediate Systems (IS-ISs | [IS-IS](#ra_isis) | part | 1 | 1 |
| RFC 5130 | A Policy Control Mechanism in IS-IS Using Administrative Tags | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5150 | Label Switched Path Stitching with Generalized Multiprotocol Label Switching Traffic Engin | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5151 | Inter-Domain MPLS and GMPLS Traffic Engineering -- Resource Reservation Protocol-Traffic E | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5152 | A Per-Domain Path Computation Method for Establishing Inter-Domain Traffic Engineering (TE | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5227 | IPv4 Address Conflict Detection | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 5246 | The Transport Layer Security (TLS) Protocol Version 1.2 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 5280 | Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 5283 | LDP Extension for Inter-Area Label Switched Paths (LSPs) | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5284 | User-Defined Errors for RSVP | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5286 | Basic Specification for IP Fast Reroute: Loop-Free Alternates | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5291 | Outbound Route Filtering Capability for BGP-4 | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5301 | Dynamic Hostname Exchange Mechanism for IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5302 | Domain-Wide Prefix Distribution with Two-Level IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5303 | Three-Way Handshake for IS-IS Point-to-Point Adjacencies | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5304 | IS-IS Cryptographic Authentication | [IS-IS](#ra_isis) | scan | 0 | 0 |
| [RFC 5305](#ra_rfc5305) | IS-IS Extensions for Traffic Engineering | [IS-IS](#ra_isis) | deep | 3 | 2 |
| RFC 5306 | Restart Signaling for IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5307 | IS-IS Extensions in Support of Generalized Multi-Protocol Label Switching (GMPLS) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| [RFC 5308](#ra_rfc5308) | Routing IPv6 with IS-IS | [IS-IS](#ra_isis) | part | 1 | 0 |
| [RFC 5310](#ra_rfc5310) | IS-IS Generic Cryptographic Authentication | [IS-IS](#ra_isis) | deep | 3 | 1 |
| RFC 5311 | Simplified Extension of Link State PDU (LSP) Space for IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5316 | ISIS Extensions in Support of Inter-Autonomous System (AS) MPLS and GMPLS Traffic Engineer | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 5331 | MPLS Upstream Label Assignment and Context-Specific Label Space | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5332 | MPLS Multicast Encapsulations | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 5357](#ra_rfc5357) | A Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | part | 2 | 0 |
| RFC 5398 | Autonomous System (AS) Number Reservation for Documentation Use | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5420 | Encoding of Attributes for MPLS LSP Establishment Using Resource Reservation Protocol Traf | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5424 | The Syslog Protocol | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 5440](#ra_rfc5440) | Path Computation Element (PCE) Communication Protocol (PCEP) | [PCEP](#ra_pcep) | deep | 3 | 0 |
| RFC 5441 | A Backward-Recursive PCE-Based Computation (BRPC) Procedure to Compute Shortest Constraine | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 5443 | LDP IGP Synchronization | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5480 | Elliptic Curve Cryptography Subject Public Key Information | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 5492](#ra_rfc5492) | Capabilities Advertisement with BGP-4 | [BGP](#ra_bgp) | part | 1 | 0 |
| RFC 5495 | Description of the Resource Reservation Protocol - Traffic-Engineered (RSVP-TE) Graceful R | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5520 | Preserving Topology Confidentiality in Inter-Domain Path Computation Using a Path-Key-Base | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 5521 | Extensions to the Path Computation Element Communication Protocol (PCEP) for Route Exclusi | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 5541 | Encoding of Objective Functions in the Path Computation Element Communication Protocol (PC | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 5543 | BGP Traffic Engineering Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5561 | LDP Capabilities | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5586 | MPLS Generic Associated Channel | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5618 | Mixed Security Mode for the Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5668 | 4-Octet AS Specific BGP Extended Community | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5701 | IPv6 Address Specific BGP Extended Community Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 5712 | MPLS Traffic Engineering Soft Preemption | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 5758 | Internet X.509 Public Key Infrastructure: Additional Algorithms and Identifiers for DSA an | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 5771 | IANA Guidelines for IPv4 Multicast Address Assignments | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 5869 | HMAC-based Extract-and-Expand Key Derivation Function (HKDF) | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 5880](#ra_rfc5880) | Bidirectional Forwarding Detection (BFD) | [OAM](#ra_oam) | deep | 3 | 0 |
| RFC 5881 | Bidirectional Forwarding Detection (BFD) for IPv4 and IPv6 (Single Hop) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5882 | Generic Application of Bidirectional Forwarding Detection (BFD) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5883 | Bidirectional Forwarding Detection (BFD) for Multihop Paths | [OAM](#ra_oam) | scan | 0 | 0 |
| [RFC 5884](#ra_rfc5884) | Bidirectional Forwarding Detection (BFD) for MPLS Label Switched Paths (LSPs) | [OAM](#ra_oam) | deep | 2 | 0 |
| RFC 5885 | Bidirectional Forwarding Detection (BFD) for the Pseudowire Virtual Circuit Connectivity V | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5886 | A Set of Monitoring Tools for Path Computation Element (PCE)-Based Architecture | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 5905 | Network Time Protocol Version 4: Protocol and Algorithms Specification | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5918 | Label Distribution Protocol (LDP) 'Typed Wildcard' Forward Equivalence Class (FEC) | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 5919 | Signaling LDP Label Advertisement Completion | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 5925](#ra_rfc5925) | The TCP Authentication Option | [IP](#ra_ip) | deep | 4 | 0 |
| RFC 5926 | Cryptographic Algorithms for the TCP Authentication Option (TCP-AO) | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 5938 | Individual Session Control Feature for the Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 5952 | A Recommendation for IPv6 Address Text Representation | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6037 | Cisco Systems' Solution for Multicast in BGP/MPLS IP VPNs | [Multicast](#ra_mcast) | scan | 0 | 0 |
| [RFC 6038](#ra_rfc6038) | Two-Way Active Measurement Protocol (TWAMP) Reflect Octets and Symmetrical Size Features | [OAM](#ra_oam) | scan | 1 | 1 |
| RFC 6040 | Tunnelling of Explicit Congestion Notification | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6066 | Transport Layer Security (TLS) Extensions: Extension Definitions | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6073 | Segmented Pseudowire | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 6074 | Provisioning, Auto-Discovery, and Signaling in Layer 2 Virtual Private Networks (L2VPNs) | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 6107 | Procedures for Dynamically Signaled Hierarchical Label Switched Paths | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 6119 | IPv6 Traffic Engineering in IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 6125 | Representation and Verification of Domain-Based Application Service Identity within Intern | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6138 | LDP IGP Synchronization for Broadcast Networks | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 6213 | IS-IS BFD-Enabled TLV | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 6232 | Purge Originator Identification TLV for IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 6233 | IS-IS Registry Extension for Purges | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 6234 | US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF) | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6286 | Autonomous-System-Wide Unique BGP Identifier for BGP-4 | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 6368 | Internal BGP as the Provider/Customer Edge Protocol for BGP/MPLS IP Virtual Private Networ | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 6370 | MPLS Transport Profile (MPLS-TP) Identifiers | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 6378 | MPLS Transport Profile (MPLS-TP) Linear Protection | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 6388](#ra_rfc6388) | Label Distribution Protocol Extensions for Point-to-Multipoint and Multipoint-to-Multipoin | [MPLS/LDP](#ra_ldp) | part | 0 | 0 |
| RFC 6389 | MPLS Upstream Label Assignment for LDP | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 6391 | Flow-Aware Transport of Pseudowires over an MPLS Packet Switched Network | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 6398 | IP Router Alert Considerations and Usage | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6425 | Detecting Data-Plane Failures in Point-to-Multipoint MPLS - Extensions to LSP Ping | [OAM](#ra_oam) | scan | 0 | 0 |
| [RFC 6426](#ra_rfc6426) | MPLS On-Demand Connectivity Verification and Route Tracing | [OAM](#ra_oam) | scan | 1 | 1 |
| RFC 6454 | The Web Origin Concept | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6455 | The WebSocket Protocol | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6512 | Using Multipoint LDP When the Backbone Has No Route to the Root | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 6513 | Multicast in MPLS/BGP IP VPNs | [Multicast](#ra_mcast) | scan | 0 | 0 |
| [RFC 6514](#ra_rfc6514) | BGP Encodings and Procedures for Multicast in MPLS/BGP IP VPNs | [Multicast](#ra_mcast) | deep | 2 | 0 |
| RFC 6515 | IPv4 and IPv6 Infrastructure Addresses in BGP Updates for Multicast VPN | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 6583 | Operational Neighbor Discovery Problems | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6608 | Subcodes for BGP Finite State Machine Error | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 6625 | Wildcards in Multicast VPN Auto-Discovery Routes | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 6667 | LDP 'Typed Wildcard' Forwarding Equivalence Class (FEC) for PWid and Generalized PWid FEC  | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 6718 | Pseudowire Redundancy | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 6720 | The Generalized TTL Security Mechanism (GTSM) for the Label Distribution Protocol (LDP) | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 6790](#ra_rfc6790) | The Use of Entropy Labels in MPLS Forwarding | [MPLS/LDP](#ra_ldp) | part | 1 | 0 |
| [RFC 6793](#ra_rfc6793) | BGP Support for Four-Octet Autonomous System (AS) Number Space | [BGP](#ra_bgp) | deep | 1 | 0 |
| RFC 6805 | The Application of the Path Computation Element Architecture to the Determination of a Seq | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 6826 | Multipoint LDP In-Band Signaling for Point-to-Multipoint and Multipoint-to-Multipoint Labe | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 6870](#ra_rfc6870) | Pseudowire Preferential Forwarding Status Bit | [PW](#ra_pw) | deep | 2 | 0 |
| RFC 6890 | Special-Purpose IP Address Registries | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6901 | JavaScript Object Notation (JSON) Pointer | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6938 | Deprecation of BGP Path Attributes: DPA, ADVERTISER, and RCID_PATH / CLUSTER_ID | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 6979 | Deterministic Usage of the Digital Signature Algorithm (DSA) and Elliptic Curve Digital Si | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6980 | Security Implications of IPv6 Fragmentation with IPv6 Neighbor Discovery | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 6996 | Autonomous System (AS) Reservation for Private Use | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7032 | LDP Downstream-on-Demand in Seamless MPLS | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7110 | Return Path Specified Label Switched Path (LSP) Ping | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7112 | Implications of Oversized IPv6 Header Chains | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 7130](#ra_rfc7130) | Bidirectional Forwarding Detection (BFD) on Link Aggregation Group (LAG) Interfaces | [OAM](#ra_oam) | part | 0 | 0 |
| RFC 7140 | LDP Extensions for Hub and Spoke Multipoint Label Switched Path | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7153 | IANA Registries for BGP Extended Communities | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7246 | Multipoint Label Distribution Protocol In-Band Signaling in a Virtual Routing and Forwardi | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7267 | Dynamic Placement of Multi-Segment Pseudowires | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 7274 | Allocating and Retiring Special-Purpose MPLS Labels | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7275 | Inter-Chassis Communication Protocol for Layer 2 Virtual Private Network (L2VPN) Provider  | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 7300 | Reservation of Last Autonomous System (AS) Numbers | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7307 | LDP Extensions for Multi-Topology | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7308 | Extended Administrative Groups in MPLS Traffic Engineering (MPLS-TE) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7311 | The Accumulated IGP Metric Attribute for BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7313 | Enhanced Route Refresh Capability for BGP-4 | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7338 | Requirements and Framework for Point-to-Multipoint Pseudowires over MPLS Packet Switched N | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 7349 | LDP Hello Cryptographic Authentication | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7358 | Label Advertisement Discipline for LDP Forwarding Equivalence Classes (FECs) | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7361 | LDP Extensions for Optimized MAC Address Withdrawal in a Hierarchical Virtual Private LAN  | [PW](#ra_pw) | scan | 0 | 0 |
| RFC 7385 | IANA Registry for P-Multicast Service Interface (PMSI) Tunnel Type Code Points | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 7438 | Multipoint LDP (mLDP) In-Band Signaling with Wildcards | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7442 | Carrying Protocol Independent Multicast - Sparse Mode (PIM-SM) in Any-Source Multicast (AS | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 7447 | Deprecation of BGP Entropy Label Capability Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7473 | Controlling State Advertisements of Non-negotiated LDP Applications | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7490 | Remote Loop-Free Alternate (LFA) Fast Reroute (FRR) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7506 | IPv6 Router Alert Option for MPLS Operations, Administration, and Maintenance (OAM) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7524 | Inter-Area Point-to-Multipoint (P2MP) Segmented Label Switched Paths (LSPs) | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 7525 | Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport La | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 7552](#ra_rfc7552) | Updates to LDP for IPv6 | [MPLS/LDP](#ra_ldp) | part | 1 | 0 |
| RFC 7570 | Label Switched Path (LSP) Attribute in the Explicit Route Object (ERO) | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 7606](#ra_rfc7606) | Revised Error Handling for BGP UPDATE Messages | [BGP](#ra_bgp) | deep | 4 | 1 |
| RFC 7607 | Codification of AS 0 Processing | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7611 | BGP ACCEPT_OWN Community Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7679 | A One-Way Delay Metric for IP Performance Metrics (IPPM) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7680 | A One-Way Loss Metric for IP Performance Metrics (IPPM) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7715 | Multipoint LDP (mLDP) Node Protection | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 7717 | IKEv2-Derived Shared Secret Key for the One-Way Active Measurement Protocol (OWAMP) and Tw | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7726 | Clarifying Procedures for Establishing BFD Sessions for MPLS Label Switched Paths (LSPs) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7748 | Elliptic Curves for Security | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 7750 | Differentiated Service Code Point and Explicit Congestion Notification Monitoring in the T | [OAM](#ra_oam) | scan | 0 | 0 |
| [RFC 7761](#ra_rfc7761) | Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised) | [Multicast](#ra_mcast) | deep | 2 | 0 |
| RFC 7775 | IS-IS Route Preference for Extended IP and IPv6 Reachability | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7794 | IS-IS Prefix Attributes for Extended IPv4 and IPv6 Reachability | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7811 | An Algorithm for Computing IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7812 | An Architecture for IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7820 | UDP Checksum Complement in the One-Way Active Measurement Protocol (OWAMP) and Two-Way Act | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 7897 | Domain Subobjects for the Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | scan | 0 | 0 |
| [RFC 7911](#ra_rfc7911) | Advertisement of Multiple Paths in BGP | [BGP](#ra_bgp) | scan | 1 | 0 |
| RFC 7947 | Internet Exchange BGP Route Server | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7948 | Internet Exchange BGP Route Server Operations | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 7981 | IS-IS Extensions for Advertising Router Information | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 7999 | BLACKHOLE Community | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8017 | PKCS #1: RSA Cryptography Specifications Version 2.2 | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 8029](#ra_rfc8029) | Detecting Multiprotocol Label Switched (MPLS) Data-Plane Failures | [OAM](#ra_oam) | deep | 1 | 0 |
| RFC 8032 | Edwards-Curve Digital Signature Algorithm (EdDSA) | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 8077](#ra_rfc8077) | Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) | [PW](#ra_pw) | deep | 1 | 0 |
| RFC 8092 | BGP Large Communities Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8093 | Deprecation of BGP Path Attribute Values 30, 31, 129, 241, 242, and 243 | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8102 | Remote-LFA Node Protection and Manageability | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8169 | Residence Time Measurement in MPLS Networks | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| RFC 8186 | Support of the IEEE 1588 Timestamp Format in a Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 8200 | Internet Protocol, Version 6 (IPv6) Specification | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8201 | Path MTU Discovery for IP version 6 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8202 | IS-IS Multi-Instance | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8205 | BGPsec Protocol Specification | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8212 | Default External BGP (EBGP) Route Propagation Behavior without Policies | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8223 | Application-Aware Targeted LDP | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| [RFC 8231](#ra_rfc8231) | Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE | [PCEP](#ra_pcep) | deep | 5 | 1 |
| RFC 8232 | Optimizations of Label Switched Path State Synchronization Procedures for a Stateful PCE | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8233 | Extensions to the Path Computation Element Communication Protocol (PCEP) to Compute Servic | [PCEP](#ra_pcep) | scan | 0 | 0 |
| [RFC 8253](#ra_rfc8253) | PCEPS: Usage of TLS to Provide a Secure Transport for the Path Computation Element Communi | [PCEP](#ra_pcep) | deep | 1 | 0 |
| RFC 8259 | The JavaScript Object Notation (JSON) Data Interchange Format | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8271 | Updates to the Resource Reservation Protocol for Fast Reroute of Traffic Engineering GMPLS | [RSVP](#ra_rsvp) | scan | 0 | 0 |
| [RFC 8277](#ra_rfc8277) | Using BGP to Bind MPLS Labels to Address Prefixes | [BGP](#ra_bgp) | deep | 0 | 0 |
| [RFC 8281](#ra_rfc8281) | Path Computation Element Communication Protocol (PCEP) Extensions for PCE-Initiated LSP Se | [PCEP](#ra_pcep) | deep | 1 | 0 |
| RFC 8287 | Label Switched Path (LSP) Ping/Traceroute for Segment Routing (SR) IGP-Prefix and IGP-Adja | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 8306 | Extensions to the Path Computation Element Communication Protocol (PCEP) for Point-to-Mult | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8320 | LDP Extensions to Support Maximally Redundant Trees | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 8326 | Graceful BGP Session Shutdown | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8333 | Micro-loop Prevention by Introducing a Local Convergence Delay | [IS-IS](#ra_isis) | scan | 0 | 0 |
| [RFC 8338](#ra_rfc8338) | Signaling Root-Initiated Point-to-Multipoint Pseudowire Using LDP | [PW](#ra_pw) | deep | 1 | 1 |
| RFC 8356 | Experimental Codepoint Allocation for the Path Computation Element Communication Protocol  | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 8402 | Segment Routing Architecture | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8405 | Shortest Path First (SPF) Back-Off Delay Algorithm for Link-State IGPs | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8408 | Conveying Path Setup Type in PCE Communication Protocol (PCEP) Messages | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8439 | ChaCha20 and Poly1305 for IETF Protocols | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8446 | The Transport Layer Security (TLS) Protocol Version 1.3 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8448 | Example Handshake Traces for TLS 1.3 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 8491 | Signaling Maximum SID Depth (MSD) Using IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8538 | Notification Message Support for BGP Graceful Restart | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8545 | Well-Known Port Assignments for the One-Way Active Measurement Protocol (OWAMP) and the Tw | [OAM](#ra_oam) | scan | 0 | 0 |
| [RFC 8570](#ra_rfc8570) | IS-IS Traffic Engineering (TE) Metric Extensions | [IS-IS](#ra_isis) | part | 1 | 0 |
| RFC 8571 | BGP - Link State (BGP-LS) Advertisement of IGP Traffic Engineering Performance Metric Exte | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8623 | Stateful Path Computation Element (PCE) Protocol Extensions for Usage with Point-to-Multip | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8654 | Extended Message Support for BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8660 | Segment Routing with the MPLS Data Plane | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8661 | Segment Routing MPLS Interworking with LDP | [IS-IS](#ra_isis) | scan | 0 | 0 |
| [RFC 8664](#ra_rfc8664) | Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing | [PCEP](#ra_pcep) | deep | 1 | 1 |
| [RFC 8667](#ra_rfc8667) | IS-IS Extensions for Segment Routing | [IS-IS](#ra_isis) | deep | 1 | 0 |
| RFC 8668 | Advertising Layer 2 Bundle Member Link Attributes in IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 8669 | Segment Routing Prefix Segment Identifier Extensions for BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8685 | Path Computation Element Communication Protocol (PCEP) Extensions for the Hierarchical Pat | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8697 | Path Computation Element Communication Protocol (PCEP) Extensions for Establishing Relatio | [PCEP](#ra_pcep) | scan | 0 | 0 |
| [RFC 8706](#ra_rfc8706) | Restart Signaling for IS-IS | [IS-IS](#ra_isis) | deep | 0 | 0 |
| RFC 8741 | Ability for a Stateful Path Computation Element (PCE) to Request and Obtain Control of a L | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8745 | Path Computation Element Communication Protocol (PCEP) Extensions for Associating Working  | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8751 | Hierarchical Stateful Path Computation Element (PCE) | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8754 | IPv6 Segment Routing Header (SRH) | [IS-IS](#ra_isis) | scan | 0 | 0 |
| [RFC 8762](#ra_rfc8762) | Simple Two-Way Active Measurement Protocol | [OAM](#ra_oam) | part | 0 | 0 |
| RFC 8779 | Path Computation Element Communication Protocol (PCEP) Extensions for GMPLS | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8786 | Updated Rules for Processing Stateful PCE Request Parameters Flags | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8800 | Path Computation Element Communication Protocol (PCEP) Extension for Label Switched Path ( | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 8814 | Signaling Maximum SID Depth (MSD) Using the Border Gateway Protocol - Link State | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8950 | Advertising IPv4 Network Layer Reachability Information (NLRI) with an IPv6 Next Hop | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 8972 | Simple Two-Way Active Measurement Protocol Optional Extensions | [OAM](#ra_oam) | scan | 0 | 0 |
| RFC 8986 | Segment Routing over IPv6 (SRv6) Network Programming | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9000 | QUIC: A UDP-Based Multiplexed and Secure Transport | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9001 | Using TLS to Secure QUIC | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9002 | QUIC Loss Detection and Congestion Control | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9003 | Extended BGP Administrative Shutdown Communication | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9005 | Path Computation Element Communication Protocol (PCEP) Extension for Associating Policies  | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9012 | The BGP Tunnel Encapsulation Attribute | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9015 | BGP Control Plane for the Network Service Header in Service Function Chaining | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9026 | Multicast VPN Fast Upstream Failover | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 9050 | Path Computation Element Communication Protocol (PCEP) Procedures and Extensions for Using | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9059 | Path Computation Element Communication Protocol (PCEP) Extensions for Associated Bidirecti | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9072 | Extended Optional Parameters Length for BGP OPEN Message | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9085 | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9086 | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing BGP Egress Pe | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9088 | Signaling Entropy Label Capability and Entropy Readable Label Depth Using IS-IS | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9104 | Distribution of Traffic Engineering Extended Administrative Groups Using the Border Gatewa | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9110 | HTTP Semantics | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9112 | HTTP/1.1 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9114 | HTTP/3 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9204 | QPACK: Field Compression for HTTP/3 | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9234 | Route Leak Prevention and Detection Using Roles in UPDATE and OPEN Messages | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9256 | Segment Routing Policy Architecture | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9294 | Application-Specific Link Attributes Advertisement Using the Border Gateway Protocol - Lin | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9325 | Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport La | [IP](#ra_ip) | scan | 0 | 0 |
| RFC 9346 | IS-IS Extensions in Support of Inter-Autonomous System (AS) MPLS and GMPLS Traffic Enginee | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9350 | IGP Flexible Algorithm | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9352 | IS-IS Extensions to Support Segment Routing over the IPv6 Data Plane | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9357 | Label Switched Path (LSP) Object Flag Extension for Stateful PCE | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9377 | IS-IS Flood Reflection | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9384 | A BGP Cease NOTIFICATION Subcode for Bidirectional Forwarding Detection (BFD) | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9479 | IS-IS Application-Specific Link Attributes | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9488 | Local Protection Enforcement in the Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9494 | Long-Lived Graceful Restart for BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9502 | IGP Flexible Algorithm in IP Networks | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9514 | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing over IPv6 (SR | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9525 | Service Identity in TLS | [IP](#ra_ip) | scan | 0 | 0 |
| [RFC 9552](#ra_rfc9552) | Distribution of Link-State and Traffic Engineering Information Using BGP | [BGP](#ra_bgp) | deep | 2 | 0 |
| RFC 9603 | Path Computation Element Communication Protocol (PCEP) Extensions for IPv6 Segment Routing | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9604 | Carrying Binding Label/SID in PCE-Based Networks | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9658 | Multipoint LDP Extensions for Multi-Topology Routing | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 9687 | Border Gateway Protocol 4 (BGP-4) Send Hold Timer | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9757 | Path Computation Element Communication Protocol (PCEP) Extensions for Native IP Networks | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9774 | Deprecation of AS_SET and AS_CONFED_SET in BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9776 | Internet Group Management Protocol, Version 3 | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 9777 | Multicast Listener Discovery Version 2 (MLDv2) for IPv6 | [Multicast](#ra_mcast) | scan | 0 | 0 |
| RFC 9789 | MPLS Network Actions (MNAs) Framework | [MPLS/LDP](#ra_ldp) | scan | 0 | 0 |
| RFC 9793 | BGP Extensions for Bit Index Explicit Replication (BIER) | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9800 | Compressed SRv6 Segment List Encoding | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9830 | Advertising Segment Routing Policies in BGP | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9831 | Segment Type Extensions for BGP Segment Routing (SR) Policy | [BGP](#ra_bgp) | scan | 0 | 0 |
| RFC 9843 | IGP Flexible Algorithms: Bandwidth, Delay, Metrics, and Constraints | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9855 | Topology Independent Fast Reroute Using Segment Routing | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9862 | Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing (SR) | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 9885 | Multi-Part TLVs in IS-IS | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9917 | IGP Flexible Algorithms Reverse Affinity Constraint | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9929 | IGP Unreachable Prefix Announcement | [IS-IS](#ra_isis) | scan | 0 | 0 |
| RFC 9933 | Carrying SR-Algorithm in Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | scan | 0 | 0 |
| RFC 10039 | Interconnecting EVPN and IPVPN Domains | [BGP](#ra_bgp) | scan | 0 | 0 |

