# RFC analysis: contradictions, ambiguities and possible errata {#rfc_analysis}

A review of 407 RFCs covering BGP, IS-IS, MPLS, LDP, RSVP-TE, PCEP, PIM, BFD, pseudowires, measurement protocols and supporting IP and security specifications. Each finding names the RFC and section, quotes the text briefly, explains the contradiction, ambiguity or error, and gives the status of any existing erratum. Findings that look like errata not yet reported carry a proposed report in the RFC Editor's format (Original Text, Corrected Text, Notes). The review was done in two passes on 2026-11-09: a first pass over the most-used protocol specifications and an automated check of all texts, and a second pass that read the remaining texts.

## Summary {#ra_summary}

422 findings in 201 RFCs; 88 match an existing erratum report; **143 are proposed new errata**.

### Counts by severity {#ra_counts_sev}

| Severity | Findings | Existing erratum | Proposed erratum |
|---|---|---|---|
| error | 66 | 28 | 31 |
| contradiction | 87 | 9 | 59 |
| ambiguity | 187 | 23 | 25 |
| editorial | 82 | 28 | 28 |
| **total** | **422** | **88** | **143** |

"error" includes 10 security gaps (marked "Security gap"). "Existing erratum" counts findings that match an erratum report of any status, including rejected reports that leave a question open.

### Counts by area {#ra_counts_area}

| Area | RFCs | deep | part | read | light | scan | Findings | Proposed errata | error | contradiction | ambiguity | editorial |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [BGP, L3VPN, MVPN and BGP-LS](#ra_bgp) | 72 | 42 | 5 | 15 | 10 | 0 | 73 | 15 | 9 | 12 | 42 | 10 |
| [IS-IS, IGP TE, Segment Routing and IP FRR](#ra_isis) | 62 | 39 | 6 | 9 | 3 | 5 | 61 | 28 | 5 | 16 | 28 | 12 |
| [MPLS, LDP and mLDP](#ra_ldp) | 44 | 28 | 0 | 10 | 4 | 2 | 45 | 18 | 5 | 8 | 21 | 11 |
| [Pseudowires, VPLS and ICCP](#ra_pw) | 20 | 13 | 0 | 5 | 2 | 0 | 28 | 10 | 5 | 8 | 11 | 4 |
| [RSVP, RSVP-TE and GMPLS](#ra_rsvp) | 44 | 16 | 2 | 17 | 3 | 6 | 43 | 12 | 11 | 9 | 9 | 14 |
| [PCEP and PCE](#ra_pcep) | 36 | 26 | 2 | 1 | 6 | 1 | 85 | 35 | 10 | 20 | 41 | 14 |
| [Multicast: PIM, IGMP, MLD and MVPN](#ra_mcast) | 22 | 10 | 1 | 3 | 5 | 3 | 22 | 7 | 3 | 3 | 9 | 7 |
| [BFD, LSP ping, measurement and time](#ra_oam) | 30 | 20 | 3 | 1 | 5 | 1 | 42 | 14 | 10 | 7 | 19 | 6 |
| [IP, ICMP, neighbour discovery, transport and security](#ra_ip) | 77 | 11 | 2 | 16 | 33 | 15 | 23 | 4 | 8 | 4 | 7 | 4 |
| **all** | **407** | **205** | **21** | **77** | **71** | **33** | **422** | **143** | **66** | **87** | **187** | **82** |

### Coverage {#ra_coverage}

How deeply each RFC was read (the per-RFC table is the [Coverage by RFC](#ra_index) section at the end):

| Depth | Meaning | RFCs |
|---|---|---|
| deep | every normative section read (state machines, encodings, timers, error handling, IANA, security), or for the most-used specifications a targeted reading of all sections where implementers make choices | 205 |
| part | the sections named in the RFC entry read in full; the rest not read | 21 |
| read | normative statements and formats read through once | 77 |
| light | figures, IANA sections and the automated hits checked, or normative statements extracted | 71 |
| scan | automated checks only | 33 |

Errata status:

| Errata status | Meaning | RFCs |
|---|---|---|
| checked | the RFC Editor errata page was read; ids and status are given | 63 |
| errata exist; not read | an errata index shows errata for the RFC, but the page was not read | 19 |
| no verified errata in the index; page not read | an errata index shows no verified errata; the page was not read (reported or held errata may exist) | 64 |
| no errata page found by search (not confirmed) | a search found no errata page; not confirmed | 40 |
| not checked | not checked | 221 |

Errata status will be re-matched with a complete errata download; where a finding says "not checked" an erratum may already exist.

### Proposed errata {#ra_proposed}

| ID | RFC, section | Type | Summary |
|---|---|---|---|
| [RA-0111](#ra_rfc2385) | RFC 2385 4.3 | Technical | "32-byte words" should be "32-bit words". |
| [RA-0007](#ra_rfc4271) | RFC 4271 5 (vs RFC 7606 5.1) | Technical | Ascending attribute order conflicts with RFC 7606 5.1 (MP_REACH / MP_UNREACH first). |
| [RA-0016](#ra_rfc4724) | RFC 4724 4.2 | Technical | Clarify which stale routes are deleted on a consecutive restart, and when. |
| [RA-0117](#ra_rfc6286) | RFC 6286 2.2, 3 | Technical | Same-identifier check omits confederation peers although Section 3 treats the confederation as one AS. |
| [RA-0120](#ra_rfc7311) | RFC 7311 3.4.3, 3.2 | Technical | Capping at 0xffffffffffffffff creates a value that Section 3.2 tells receivers to discard. |
| [RA-0026](#ra_rfc7606) | RFC 7606 4 | Technical | The zero-length rule cannot be applied to unrecognized attributes. |
| [RA-0124](#ra_rfc7607) | RFC 7607 2, 4 | Technical | Security text says all routes with AS 0 are ignored; Section 2 only withdraws for AS_PATH. |
| [RA-0127](#ra_rfc7911) | RFC 7911 4 | Technical | Unclear whether an invalid Send/Receive value invalidates the tuple or the whole capability; duplicates unspecified. |
| [RA-0129](#ra_rfc7947) | RFC 7947 3, 2.2.2.2 | Technical | Security text attributes loop detection to the leftmost-AS check and cites the parent section. |
| [RA-0133](#ra_rfc8538) | RFC 8538 4.1, 9 | Technical | Start and restart conditions of the mandatory stale timer are unspecified, so the bound of Section 9 can be defeated by repeated resets. |
| [RA-0135](#ra_rfc8654) | RFC 8654 4 | Technical | Set of attributes "eligible under attribute discard" is undefined for well-formed attributes. |
| [RA-0141](#ra_rfc9234) | RFC 9234 5 | Technical | Egress value rules for confederations / private ASNs conflict with "preserved unchanged". |
| [RA-0145](#ra_rfc9494) | RFC 9494 4.2 | Technical | Consecutive-restart rule overrides RFC 4724 4.2 without saying so; scope (GR-stale vs LLGR-stale routes) unclear. |
| [RA-0149](#ra_rfc9774) | RFC 9774 3 | Technical | Treat-as-withdraw for AS_CONFED_SET in AS4_PATH conflicts with RFC 6793 handling of confederation segments in AS4_PATH. |
| [RA-0150](#ra_rfc9830) | RFC 9830 5 vs RFC 9012 13 | Technical | Error handling for malformed Tunnel Encapsulation sub-TLVs in SAFI 73 conflicts with RFC 9012 Section 13 without saying it overrides it. |
| [RA-0152](#ra_rfc3906) | RFC 3906 4.1, 4.2 | Technical | Absolute-metric example contradicts the definition in 4.1. |
| [RA-0036](#ra_rfc5120) | RFC 5120 7.1 | Technical | MT #0 is required of every MT router; "has to" is not a keyword; the 127-MT limit is per TLV. |
| [RA-0037](#ra_rfc5305) | RFC 5305 3, 4 | Technical | Path metric clamp at MAX_PATH_METRIC conflicts with ISO 10589 "unreachable" semantics. |
| [RA-0038](#ra_rfc5305) | RFC 5305 4 | Editorial | Typo "then"; nonexistent "paragraph 3.0". |
| [RA-0041](#ra_rfc5310) | RFC 5310 3.3 | Technical | Key preparation differs from RFC 2104 for L < key length <= B; Ko / Ipad length mismatch; SHA-224 block size missing. |
| [RA-0157](#ra_rfc6119) | RFC 6119 4.3 | Editorial | "interface address" in the Neighbor Address sub-TLV section. |
| [RA-0158](#ra_rfc6213) | RFC 6213 3.1, 3.2, 3.3 | Technical | Multi-topology effect of a single-topology BFD failure is implied by AND / OR rules but not stated. |
| [RA-0161](#ra_rfc7308) | RFC 7308 2.2 | Technical | EAG bit numbering example contradicts the AG-compatible word-wise numbering. |
| [RA-0162](#ra_rfc7490) | RFC 7490 5.2.1.2, 5.3 | Technical | Extended P-space: text uses N->S->E->P, pseudocode uses RFC 5286 Inequality 1 (N->S->P). |
| [RA-0164](#ra_rfc7775) | RFC 7775 3.3, 3.4 | Technical | Within-class selection and ties between internal and external routes not stated. |
| [RA-0166](#ra_rfc7794) | RFC 7794 2.2 | Technical | Source Router ID consistency rule ambiguous for leaked prefixes (originator's or carrier's TLV 134). |
| [RA-0169](#ra_rfc8202) | RFC 8202 3.6.1, 3.6.1.1, 3.6.2 | Technical | Discard rule of 3.6.1 conflicts with mandatory IID-TLV (IID 0) in point-to-point IIHs of 3.6.2 on point-to-point-over-LAN circuits; unclear "either address". |
| [RA-0170](#ra_rfc8333) | RFC 8333 5.4 | Technical | Mandatory delay in step 5 conflicts with the "SHOULD only ... when protected" restriction. |
| [RA-0172](#ra_rfc8405) | RFC 8405 5.2, 5.3, 5.4 | Technical | QUIET defined relative to last computation, FSM relative to last IGP event. |
| [RA-0174](#ra_rfc8570) | RFC 8570 4.6, Appendix A | Technical | Appendix A claims the 4.6 bundle definition was corrected per erratum 5486, but 4.6 is unchanged. |
| [RA-0178](#ra_rfc8661) | RFC 8661 2.1 | Technical | Coexistence example programs an SR entry for a prefix of a non-SR node. |
| [RA-0180](#ra_rfc8668) | RFC 8668 Appendix A, 3 | Technical | Appendix A TLV lengths omit the descriptor length octets. |
| [RA-0182](#ra_rfc9346) | RFC 9346 3.2 vs 3.4.4 | Editorial | Section 3.2 names a nonexistent "IPv6 Router ID sub-TLV". |
| [RA-0183](#ra_rfc9346) | RFC 9346 3.4.2, 3.4.3 | Editorial | Wrong parent TLV named for the Remote ASBR Identifier sub-TLVs. |
| [RA-0184](#ra_rfc9350) | RFC 9350 13.1 vs 8 | Technical | Saturation of overflowing flex-algorithm metrics at 0xFFFFFFFF makes the prefix unreachable downstream (Section 8), unlike the MAX_PATH_METRIC clamp of RFC 5305. |
| [RA-0186](#ra_rfc9352) | RFC 9352 11.3 | Editorial | Wrong RFC number in the IANA table of Section 11.3. |
| [RA-0190](#ra_rfc9377) | RFC 9377 4.5 vs 4.6 | Technical | Sections 4.5 and 4.6 disagree on standard L2 adjacencies between a flood reflector and its clients. |
| [RA-0194](#ra_rfc9502) | RFC 9502 6.1, 6.2 | Technical | Unclear whether an out-of-range algorithm invalidates the entry or the whole TLV. |
| [RA-0195](#ra_rfc9843) | RFC 9843 4.1.3.2 | Technical | IS-IS threshold rule sets a metric that does not fit the 24-bit Generic Metric. |
| [RA-0196](#ra_rfc9843) | RFC 9843 4.1.4.2 | Technical | Off-by-one: maximum 32-bit metric is 4,294,967,295. |
| [RA-0197](#ra_rfc9843) | RFC 9843 4.1.3.1, 4.1.3.2 | Editorial | Flags field drawn narrower than its 1-octet definition in two IS-IS figures. |
| [RA-0198](#ra_rfc9855) | RFC 9855 6.1 vs 7.1 | Technical | "Kept unchanged" conflicts with the MPLS pop / re-push rules of Section 7.1. |
| [RA-0199](#ra_rfc9885) | RFC 9885 3.2.1, 5 | Technical | MP-TLV key for TLV 22 does not say whether each part must repeat the link identifiers. |
| [RA-0048](#ra_rfc3212) | RFC 3212 3.4 | Technical | Reference to nonexistent Section 4.11 (status codes are in 5.3). |
| [RA-0201](#ra_rfc3478) | RFC 3478 3.3, 4 | Technical | Security section says "requires" for a rule stated as SHOULD NOT in 3.3. |
| [RA-0202](#ra_rfc3478) | RFC 3478 3.1.2 | Technical | Egress per-FEC-label case omits the FEC match that the 3.1.1 equivalent has. |
| [RA-0052](#ra_rfc5036) | RFC 5036 3.5.11 (and the other message figures) | Editorial | Message Type / Message Length boundary drawn one bit early in the message figures. |
| [RA-0206](#ra_rfc5331) | RFC 5331 8 | Technical | Off-by-one in the mask length condition for auto-generated context labels. |
| [RA-0208](#ra_rfc5443) | RFC 5443 2 | Technical | Misstates the effect of the RFC 5305 maximum link metric. |
| [RA-0210](#ra_rfc5918) | RFC 5918 6 | Technical | Field size stated as two octets; Section 3 and Figure 3 make it one octet. |
| [RA-0216](#ra_rfc6389) | RFC 6389 6, 9 | Technical | LAN upstream hash differs from RFC 6388 (sum vs CRC32) although Section 9 says it is taken from RFC 6388. |
| [RA-0219](#ra_rfc7307) | RFC 7307 3.3 | Technical | Figure 4 Len = 6 does not match the 4 octets drawn. |
| [RA-0221](#ra_rfc7307) | RFC 7307 3.5.2 | Editorial | "label release" where "label withdraw" is meant. |
| [RA-0222](#ra_rfc7349) | RFC 7349 6.1, 2.3 | Technical | TLV Length values in 6.1 omit the 8-octet Cryptographic Sequence Number counted by 2.3. |
| [RA-0223](#ra_rfc7349) | RFC 7349 5.2 | Technical | Unclear whether the HMAC covers the LDP PDU header (LDP Identifier). |
| [RA-0225](#ra_rfc7349) | RFC 7349 4, 6.2 | Editorial | Two wrong section references. |
| [RA-0226](#ra_rfc7473) | RFC 7473 4.1, 4.2 | Technical | Unknown App value: "error" (4.1) versus "ignore" (4.1, 4.2) with different keywords. |
| [RA-0227](#ra_rfc7473) | RFC 7473 4.1, 4.2 | Technical | U=1 silent-ignore rule contradicts the "Unsupported TLV" notification requirement. |
| [RA-0228](#ra_rfc7552) | RFC 7552 6.1.1 | Technical | Dual-Stack capability TLV figure has an undescribed MBZ field and no Length value. |
| [RA-0232](#ra_rfc8320) | RFC 8320 4.1 | Technical | S-bit values for advertise and withdraw are swapped. |
| [RA-0234](#ra_rfc8356) | RFC 8356 4 | Editorial | Wrong noun and wrong section reference for the experimental TLV range. |
| [RA-0237](#ra_rfc4385) | RFC 4385 4.2, Appendix | Technical | Normative text updates the expected sequence number on out-of-window packets; the Appendix does not. |
| [RA-0238](#ra_rfc4448) | RFC 4448 4.6 | Technical | "source MAC address" should be "destination MAC address". |
| [RA-0242](#ra_rfc5085) | RFC 5085 8.1.2, 4 | Editorial | Registry name says "Control Verification" for Connectivity Verification. |
| [RA-0244](#ra_rfc6073) | RFC 6073 14.5, 7.4.1 | Technical | Length of sub-TLV 0x06 is 14 octets per Section 7.4.1, not 12. |
| [RA-0245](#ra_rfc6073) | RFC 6073 7.4.1, 7.6 | Technical | "Mandatory" SP-PE sub-TLVs are never identified; loop detection depends on an optional one. |
| [RA-0248](#ra_rfc6074) | RFC 6074 3.2.3, 3.2.2.1 | Technical | Mapping of the VPLS-id Extended Community to the 8-octet AGI is unspecified. |
| [RA-0250](#ra_rfc6391) | RFC 6391 1.3, 3 | Technical | Section 1.3 discards the flow LSE unprocessed; Section 3 requires a reserved-label check. |
| [RA-0252](#ra_rfc7275) | RFC 7275 4.2.1, 4.4.2, 4.2 | Technical | ICCP and Application Connection state machines answer a NAK with a NAK. |
| [RA-0255](#ra_rfc7275) | RFC 7275 6.4.1 | Editorial | Code iii described with the condition of code ii. |
| [RA-0060](#ra_rfc8338) | RFC 8338 3.2.1 | Technical | Reference to nonexistent Section 2.3 (typed wildcard FEC is 3.3). |
| [RA-0259](#ra_rfc2210) | RFC 2210 3.3.6, 3.3.2 | Technical | ADSPEC example mislabels the extent of the general parameters fragment and shows 16-bit fields where 3.3.2 defines 32-bit ones. |
| [RA-0261](#ra_rfc2961) | RFC 2961 4.5 | Technical | Wrap test casts operands, not the difference; signed overflow and wrong result near 2^31. |
| [RA-0270](#ra_rfc4124) | RFC 4124 13.2, 6.5, 13.3.5 | Technical | IANA text says values 1 through 7; eight values are defined. |
| [RA-0275](#ra_rfc4873) | RFC 4873 4.3.1 | Editorial | Word order error in the replacement text for RFC 3473. |
| [RA-0276](#ra_rfc4874) | RFC 4874 3.2, 4.2, 6 | Editorial | Error code named "Routing Error" instead of "Routing Problem" (twice), and a wrong section reference in Section 6. |
| [RA-0277](#ra_rfc5063) | RFC 5063 5.3.1, 4.2 | Technical | Rule refers to an Epoch "received in the most recent Hello message"; Hello messages carry no Epoch. |
| [RA-0280](#ra_rfc5151) | RFC 5151 9.1 | Technical | Wrong reference in the IANA table for the Contiguous LSP flag. |
| [RA-0283](#ra_rfc5420) | RFC 5420 5, 9 | Technical | Rule for repeated objects conflicts with the "MUST NOT forward without acting" rule of Section 5. |
| [RA-0286](#ra_rfc7570) | RFC 7570 2.1 | Technical | Stated maximum Hop Attributes size (250) does not fit the 8-bit, 4-octet-aligned subobject length. |
| [RA-0287](#ra_rfc8169) | RFC 8169 3.1 | Technical | PTP sub-TLV Length (20), field sizes (4 + 10 + 2) and Figure 2 (Port ID of 6 octets) disagree. |
| [RA-0288](#ra_rfc8169) | RFC 8169 4.4.1 | Technical | RTM_SET TLV header does not follow the RFC 5420 TLV format; I-bit accumulation unspecified. |
| [RA-0289](#ra_rfc8271) | RFC 8271 7.2 | Technical | Wrong reference for ERROR_SPEC C-Type 6 and no IPv6 C-Type. |
| [RA-0073](#ra_rfc5088) | RFC 5088 7.2 | Editorial | Reference to nonexistent Section 4.1.5 (PCE-CAP-FLAGS is 4.5). |
| [RA-0290](#ra_rfc5441) | RFC 5441 12, 15.3 | Technical | IANA section gives bit 4 for the flag that Section 12 (and the registry) define as bit 28. |
| [RA-0291](#ra_rfc5441) | RFC 5441 12 | Technical | "PCReq" should be "PCRep". |
| [RA-0294](#ra_rfc5541) | RFC 5541 3.1.1 | Technical | Error-type 3 has no Error-value 4 in RFC 5440. |
| [RA-0078](#ra_rfc8231) | RFC 8231 7.3.2, 7.3.4 | Technical | Erratum 6289 also applies to 7.3.4: TLV Length is the value length. |
| [RA-0297](#ra_rfc8232) | RFC 8232 3.2, 4.2 | Technical | Stale marking and purge of 3.2 conflict with incremental synchronization; deletion encoding unspecified. |
| [RA-0298](#ra_rfc8232) | RFC 8232 5.2, 6.2 | Technical | SHOULD (5.2) versus MUST (6.2) for the empty ERO in the synchronization trigger. |
| [RA-0303](#ra_rfc8233) | RFC 8233 3.1.5.1 | Technical | Reply example sets B=1, which RFC 5440 7.8 forbids for a computed metric. |
| [RA-0304](#ra_rfc8233) | RFC 8233 3.2.2, 3.2.3, 7.3 | Editorial | LRBU expanded as "Residual" in 3.2.3 and 7.3, "Reserved" in 3.2.2. |
| [RA-0305](#ra_rfc8233) | RFC 8233 6.2, 3.2.3.1 | Technical | Reoptimisation trigger compares utilization in the wrong direction. |
| [RA-0308](#ra_rfc8306) | RFC 8306 3.7, 3.8 | Technical | Error behaviour attributed to a PCE that does not understand the P2MP flag. |
| [RA-0309](#ra_rfc8306) | RFC 8306 3.10 | Technical | Unclear trigger conditions for Error-Type 17 values; "PCC" for "PCE". |
| [RA-0315](#ra_rfc8623) | RFC 8623 12 | Technical | Wrong reference for instantiation security considerations. |
| [RA-0316](#ra_rfc8623) | RFC 8623 7.1.1, 6.1, 7.2 | Technical | Session-close rule differs between missing P2MP-LSP-IDENTIFIERS TLV and other missing P2MP objects. |
| [RA-0317](#ra_rfc8623) | RFC 8623 6.1, 6.6.2 | Technical | PCRpt examples in 6.6.2 do not match the RBNF of 6.1. |
| [RA-0318](#ra_rfc8623) | RFC 8623 5.1, 6.6.1 | Technical | Full-update rule of 5.1 versus the partial P2MP update of 6.6.1. |
| [RA-0319](#ra_rfc8623) | RFC 8623 9 | Technical | Capability flags attributed to the LSP object; error trigger only for the non-advertising receiver. |
| [RA-0084](#ra_rfc8664) | RFC 8664 4.3.1 vs 5.2.1 | Technical | NT "MUST be ignored" (even as corrected by 6753) conflicts with the validation rules of 5.2.1. |
| [RA-0322](#ra_rfc8685) | RFC 8685 4.2 | Technical | "PCReq" for "PCRep" in the negative reply; inconsistent name of the S bit. |
| [RA-0323](#ra_rfc8685) | RFC 8685 3.2.1, 4.1 | Technical | MUST in 3.2.1 versus SHOULD in 4.1 for the 28/1 PCErr. |
| [RA-0324](#ra_rfc8685) | RFC 8685 3.2.1.1 | Technical | Backward-compatibility claim ignores non-TLV extensions (OF codes, METRIC types, flags). |
| [RA-0327](#ra_rfc8697) | RFC 8697 5 | Technical | Boundary of the Operator-configured Association Range check is unclear. |
| [RA-0331](#ra_rfc8745) | RFC 8745 3.1 vs 4.5 | Technical | Number of working LSPs in a PPAG differs between Sections 3.1 and 4.5; N for 1:N is not signalled. |
| [RA-0334](#ra_rfc8779) | RFC 8779 2.5.2.5 | Technical | O-bit receive rule ("ignored") contradicts the 10/29 error for O and L both set. |
| [RA-0336](#ra_rfc8800) | RFC 8800 5.1 | Technical | DAT requires a range but defines no default for a peer that sends none. |
| [RA-0337](#ra_rfc8800) | RFC 8800 5.3 | Editorial | "OF object" should be "OF-List TLV". |
| [RA-0339](#ra_rfc9050) | RFC 9050 3 vs 5.5.8, 7.3 | Technical | PCC-based allocation (5.5.8) conflicts with the prohibition in Section 3; the range used is unspecified. |
| [RA-0341](#ra_rfc9050) | RFC 9050 5.5.8 | Technical | "PCRpt message without any label" cannot be encoded: Label is a fixed field of the CCI object. |
| [RA-0342](#ra_rfc9050) | RFC 9050 5.5.1, 5.5.2 | Editorial | "CC-ID object" should be "CCI object" (twice). |
| [RA-0347](#ra_rfc9059) | RFC 9059 5.7 | Editorial | "PCE speaker" should be "PCEP speaker"; sender and receiver confused in the tunnel-mismatch rule. |
| [RA-0350](#ra_rfc9603) | RFC 9603 5.2.1 vs 4.3.1, 4.3.1.1 | Technical | SRv6-ERO length validation omits the SID Structure (T bit). |
| [RA-0351](#ra_rfc9603) | RFC 9603 4.3.1 vs 5.2.1 | Technical | Receive rule for T and S both set differs between Sections 4.3.1 and 5.2.1. |
| [RA-0354](#ra_rfc9604) | RFC 9604 5 | Technical | PCC must close the session on a PCErr that carries the offending TLV, which the PCE is allowed to include. |
| [RA-0355](#ra_rfc9604) | RFC 9604 7 | Technical | Wrong reference for SRv6-ERO NT=0 handling. |
| [RA-0360](#ra_rfc9862) | RFC 9862 4.5.2 | Editorial | Garbled sentence on Protocol-Origin variants. |
| [RA-0085](#ra_rfc2236) | RFC 2236 2, 3 | Technical | References to sections 1.4, 7.3 and 7.8 should be 2.4, 8.3 and 8.8. |
| [RA-0363](#ra_rfc4607) | RFC 4607 9 | Editorial | Missing "::" in the IPv6 range of the IANA section. |
| [RA-0364](#ra_rfc5015) | RFC 5015 3.5.3.5, 3.6, 3.7.2 | Technical | State machine uses undefined BOperiod and OPlow_int. |
| [RA-0365](#ra_rfc5015) | RFC 5015 3.5.3.1, 3.7.1 | Editorial | "Path message" should be "Pass message". |
| [RA-0366](#ra_rfc5059) | RFC 5059 3.1.2 | Technical | Prose says NoInfo moves to AA; the state table moves to AP. |
| [RA-0376](#ra_rfc9776) | RFC 9776 8.12 vs 9777 9.12 | Technical | Unit error in the Older Version Querier Present Interval; differs from RFC 9777 9.12. |
| [RA-0378](#ra_rfc9777) | RFC 9777 9.5 | Editorial | Unbalanced parentheses in the Other Querier Present Interval formula. |
| [RA-0379](#ra_rfc5357) | RFC 5357 4.2 | Technical | Reflector decryption length for received Session-Sender packets in encrypted mode is wrong (96 instead of 32 octets). |
| [RA-0381](#ra_rfc5357) | RFC 5357 3.8 | Editorial | Wrong message named in the Stop-Sessions paragraph. |
| [RA-0386](#ra_rfc5882) | RFC 5882 4.3.2.2, 10.1.2 | Technical | Three cross-references point at Section 3.x where Section 4.2 / 4.3 is meant. |
| [RA-0391](#ra_rfc5938) | RFC 5938 3.2, 3.4 | Editorial | "session" for "section"; the "one or greater" rule attached to the wrong field in 3.4. |
| [RA-0098](#ra_rfc6038) | RFC 6038 4.3 | Editorial | Reference to nonexistent Section 4.1.2. |
| [RA-0099](#ra_rfc6426) | RFC 6426 7.2 | Technical | IANA table cites nonexistent Sections 2.4.1 / 2.4.2 (should be 2.3.1 / 2.3.2). |
| [RA-0394](#ra_rfc6426) | RFC 6426 2.1, 2.1.1 | Technical | Non IP address type K value is correct for the DSMAP but not for the DDMAP. |
| [RA-0397](#ra_rfc7110) | RFC 7110 4, 5.1 | Technical | Section 5.1 still requires at least one sub-TLV; companion to erratum 4197. |
| [RA-0401](#ra_rfc7726) | RFC 7726 2.3, 2.4 | Technical | "State Down(1)" conflicts with "without triggering any state change" under RFC 5880. |
| [RA-0403](#ra_rfc7726) | RFC 7726 2.1 | Technical | Mandatory drop of refused bootstrap echo requests conflicts with RFC 5884 erratum 5085 (reply mandatory). |
| [RA-0404](#ra_rfc7750) | RFC 7750 2.2.1 | Technical | "Least-significant" bits of the Differentiated Services field is ambiguous against the 8-bit TOS / Traffic Class octet. |
| [RA-0405](#ra_rfc8287) | RFC 8287 7.4 | Technical | Step 4a heading says "with the No-PHP flag" but requires the flag to be 0; IPv6 branch says "IPv4 Prefix". |
| [RA-0407](#ra_rfc8762) | RFC 8762 4.6, 4.3, 7 | Technical | Security considerations omit the amplification created by Section 4.6. |
| [RA-0410](#ra_rfc8972) | RFC 8972 4 | Editorial | Session-Reflector rules placed in the Session-Sender's validation list. |
| [RA-0411](#ra_rfc1071) | RFC 1071 4.1 | Technical | Sample C code dereferences a non-pointer and mishandles the odd byte on big-endian hosts. |
| [RA-0413](#ra_rfc1624) | RFC 1624 5 | Editorial | Wrong section reference. |
| [RA-0415](#ra_rfc4443) | RFC 4443 2.2, 4.2 | Technical | Echo Reply source rule of 4.2 differs from the general rule of 2.2 (b) without saying which applies. |
| [RA-0420](#ra_rfc5926) | RFC 5926 3.1.1 | Technical | Byte order of Output_Length in the KDF input is unspecified. |

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
- [RA-0133](#ra_rfc8538) RFC 8538 4.1, 9: The mandatory stale-route timer has no defined start or restart condition, so repeated resets can keep stale routes indefinitely (security).
- [RA-0145](#ra_rfc9494) RFC 9494 4.2: The LLGR consecutive-restart rule overrides RFC 4724 4.2 without saying so.
- [RA-0120](#ra_rfc7311) RFC 7311 3.4.3, 3.2: Capping the AIGP value at the maximum 64-bit value produces a value that receivers must discard.
- [RA-0184](#ra_rfc9350) RFC 9350 13.1 vs 8: Saturating overflowing flex-algorithm metrics makes prefixes unreachable downstream, unlike the clamp of RFC 5305.
- [RA-0232](#ra_rfc8320) RFC 8320 4.1: The S-bit values for advertise and withdraw are swapped.
- [RA-0290](#ra_rfc5441) RFC 5441 12, 15.3: The IANA section gives bit 4 for a flag that the body and the registry define as bit 28.
- [RA-0222](#ra_rfc7349) RFC 7349 6.1, 2.3: TLV Length values omit the 8-octet Cryptographic Sequence Number.
- [RA-0216](#ra_rfc6389) RFC 6389 6, 9: The LAN upstream hash differs from the RFC 6388 procedure it claims to reuse.
- [RA-0287](#ra_rfc8169) RFC 8169 3.1: PTP sub-TLV Length, field sizes and figure disagree.
- [RA-0238](#ra_rfc4448) RFC 4448 4.6: "source MAC address" where the destination MAC address is meant.
- [RA-0261](#ra_rfc2961) RFC 2961 4.5: The published wrap-safe identifier comparison is not wrap-safe in C.

## Method and limits {#ra_method}

**Scope.** 407 RFC texts, grouped into nine areas. The texts were taken as published (plain-text RFCs);
errata were not applied to them. A few related texts (IANA registries for PCEP, RSVP and RSVP-TE, one
Internet-Draft and NIST SP 800-38D) were used as references only and are not analysed.

**Automated checks, all 407 RFCs.** Every text was scanned by script for: references to sections that
do not exist in the same document; mixed-case or non-RFC 2119 keyword forms ("MAY NOT", "MUST not",
"SHOULD not"); leftover placeholders ("TBD", "TBA", "XXX"); and packet diagrams whose field boundaries
do not fall on bit boundaries. Every hit was read in context; most were false positives (references to
other documents split across lines, IANA wording, bit-ruler artefacts) and were dismissed. Confirmed ones
are findings. Mixed-case or non-keyword forms occur in 23 RFCs (RFC 1191, 1812, 2212, 3212, 3473, 3479,
3719, 3787, 4090, 4105, 4271, 4446, 4447, 4448, 4656, 4875, 5130, 5305, 5308, 5357, 8338, 8439, 9350);
they are listed once (RFC 1191) unless the case changes the meaning, as with "MAY NOT" in RFC 4271.

**First pass.** The protocol cores and their most-used extensions (56 RFCs) were read in the sections
where implementers have to make choices: state machines, error handling, timers and constants,
encodings and their figures, IANA tables, and the interaction with the RFCs they update or are updated
by. Findings RA-0001 to RA-0110 come from this pass.

**Second pass.** The RFCs the first pass had only scanned were read by four reviewers working in
parallel on separate lists, with the same rules: every normative section of a long RFC (all sections
with MUST or SHOULD, state machines, encodings, timers, error handling, IANA and security
considerations), and the whole text of a short one. Findings RA-0111 on come from this pass. Where
both passes produced findings for the same RFC (9 RFCs), the records were compared by section and
issue; none duplicated another, so all were kept. Background documents of little relevance to the
protocols reviewed (cryptographic algorithm specifications, test vectors, HTTP, QUIC, TLS and X.509
profiles, MIBs, frameworks) were read lightly or only scanned; the depth of every RFC is given in
[Coverage by RFC](#ra_index).

**Errata.** RFC Editor errata pages could be read only one at a time, when a web search returned the
page; no bulk export was reachable. Pages were read for 63 RFCs. For the others the status says what
is known: an errata index showing that errata exist, or showing no verified errata (reported or held
errata may still exist), a search that found no errata page (not a confirmation), or "not checked".
Existing errata are cited by id; a finding that matches a rejected report is still listed when the
question it raised remains open. Errata status will be re-matched against a complete errata download,
so a finding marked "not checked" or "none found" may turn out to be a known erratum. Proposed errata
are new reports in the RFC Editor's format; none has been filed, and several are clarifications that
would normally be "Held for Document Update".

**Limits.** Quotes are kept to one or two lines and may be abridged with "..."; line breaks are
removed. Findings come from reading, not from testing implementations. "Ambiguity" means the text
supports more than one reasonable reading, not that implementations are known to differ, unless the
issue says so. No finding for an RFC means that nothing was found at the depth stated, not that the
RFC is free of problems.

## BGP, L3VPN, MVPN and BGP-LS {#ra_bgp}

72 RFCs in this area (42 deep, 5 part, 15 read, 10 light); 73 findings, 15 of them proposed errata.

### RFC 1997: BGP Communities Attribute {#ra_rfc1997}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 2042: Registering New BGP Attribute Types {#ra_rfc2042}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 2385: Protection of BGP Sessions via the TCP MD5 Signature Option {#ra_rfc2385}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0111 | 4.3 | "The TCP header specifies where segment data starts with a 4-bit field which gives the total size of the header (including options) in 32-byte words." | The TCP Data Offset counts 32-bit words, not 32-byte words; the conclusion drawn in the next sentence (header at most 60 bytes, 40 bytes for options) is consistent only with 32-bit words. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0111 (RFC 2385, Section 4.3; type: Technical):

```
Original Text
-------------
   with a 4-bit field which gives the total size of the header
   (including options) in 32-byte words.

Corrected Text
--------------
   with a 4-bit field which gives the total size of the header
   (including options) in 32-bit words.

Notes
-----
   15 x 4 octets = 60 octets, as the following sentence states.
```

### RFC 2545: Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing {#ra_rfc2545}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 2918: Route Refresh Capability for BGP-4 {#ra_rfc2918}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 3765: NOPEER Community for Border Gateway Protocol (BGP) Route Scope Control {#ra_rfc3765}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4271: A Border Gateway Protocol 4 (BGP-4) {#ra_rfc4271}

Depth: deep. Errata: checked (checked: 21 (9 verified, 7 held, 5 rejected, 0 open)). Obsoletes: RFC 1771.

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

### RFC 4360: BGP Extended Communities Attribute {#ra_rfc4360}

Depth: read (normative statements and formats). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0112 | 2, 6 | "Each Extended Community is encoded as an 8-octet quantity" | The document gives no error handling for an EXTENDED_COMMUNITIES attribute whose length is not a multiple of 8 (or zero), nor for an attribute received with the wrong flags; behaviour was left to the generic RFC 4271 rules until RFC 7606 (Section 7.14, treat-as-withdraw) updated RFC 4360. Section 6 also says non-transitive communities "SHOULD be removed" across an AS boundary but "SHOULD NOT be removed" across a confederation boundary without saying which applies to a route leaving a confederation member towards an external AS through a member-AS boundary first. | ambiguity | not checked |

### RFC 4364: BGP/MPLS IP Virtual Private Networks (VPNs) {#ra_rfc4364}

Depth: deep. Errata: checked (checked: 9 records (1 verified editorial, 7 held, 2 rejected; none technical in substance)). Obsoletes: RFC 2547.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0012 | 4.3.4 | "... unlabeled VPN-IPv4 addresses ..." | VPN-IPv4 routes are always labelled (SAFI 128); "unlabeled IPv4 addresses" is meant. | editorial | 7180 (Held) |
| RA-0013 | 4.3.2 | "... is encoded as a VPN-IPv4 address with an RD of 0" | Receipt of a next hop with a non-zero RD is not covered. | ambiguity | none |

### RFC 4456: BGP Route Reflection: An Alternative to Full Mesh Internal BGP (IBGP) {#ra_rfc4456}

Depth: deep. Errata: checked (checked: 2 (1 held editorial, 1 rejected technical question)). Obsoletes: RFC 2796, RFC 1966.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0014 | 8 | "When an RR reflects a route, it MUST prepend the local CLUSTER_ID to the CLUSTER_LIST." | The RFC does not say what a receiver does with an IBGP route that carries ORIGINATOR_ID without CLUSTER_LIST, or CLUSTER_LIST without ORIGINATOR_ID (only a reflector could have added either). The erratum asking this was rejected as a question for the working group, so it stays open. RFC 7606 7.9 / 7.10 only cover malformed lengths. | ambiguity | 3898 (Rejected, question) |
| RA-0015 | 5 | "The Non-Client peer must be fully meshed" | Plural intended ("Non-Client peers"). | editorial | 3778 (Held) |

### RFC 4486: Subcodes for BGP Cease Notification Message {#ra_rfc4486}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4659: BGP-MPLS IP Virtual Private Network (VPN) Extension for IPv6 VPN {#ra_rfc4659}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4724: Graceful Restart Mechanism for BGP {#ra_rfc4724}

Depth: deep. Errata: checked (checked: 3 (1 reported technical, 1 held technical, 1 held editorial)). 

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

Depth: deep. Errata: checked (checked: 5 (1 verified technical, 4 held editorial)). Obsoletes: RFC 2858.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0020 | 4 | "(MP_UNREACH_NLRI, AFI:) identifies the set of Network Layer protocols to which the address carried in the Next Hop field must belong" | MP_UNREACH_NLRI has no Next Hop field; the AFI/SAFI only qualify the withdrawn routes. Copy-and-paste from section 3. | error | 1573 (Verified) |
| RA-0021 | 3 | "... the MP_NLRI attribute ..." | There is no "MP_NLRI" attribute; MP_REACH_NLRI (or its NLRI field) is meant. | editorial | 3848, 3849 (Held) |
| RA-0022 | 5 | "The Network Layer Reachability information is encoded as one or more 2-tuples of the form <length, prefix>" | The <length, prefix> encoding is written as if it applies to every SAFI; it applies only to SAFI 1 and 2. Labelled, VPN, MVPN, BGP-LS and SR Policy NLRI use their own encodings. | ambiguity | 5120 (Held) |
| RA-0023 | 7, 8 | "... the speaker MUST delete all the BGP routes received from that neighbor whose AFI/SAFI is the same as the one carried in the incorrect ... attribute." | Silent on an MP attribute for a family that was never negotiated, and offers two incompatible reactions (reset or "AFI/SAFI disable") for a malformed one. | ambiguity | none |

### RFC 4798: Connecting IPv6 Islands over IPv4 MPLS Using IPv6 Provider Edge Routers (6PE) {#ra_rfc4798}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5004: Avoid BGP Best Path Transitions from One External to Another {#ra_rfc5004}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5065: Autonomous System Confederations for BGP {#ra_rfc5065}

Depth: deep. Errata: not checked. Obsoletes: RFC 3065.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0113 | 5.3 | "When comparing routes using the internal (IBGP learned) versus external (EBGP learned) rules, treat a route that is learned from a peer that is in the same confederation (not necessarily the same Member-AS) as "internal"." | The rule makes routes from other Member-ASes equal to IBGP routes at the RFC 4271 9.1.2.2 (d) step; the text does not say whether an implementation may still prefer them over IBGP routes in a later tie-break (a common vendor variation), and rule 2 does not cover a path whose first non-confederation segment is an AS_SET (no neighbour AS defined for MED comparison in 5.2). | ambiguity | not checked |
| RA-0114 | 4.1 | "If the act of prepending will cause an overflow in the AS_PATH segment (i.e., more than 255 ASs), it SHOULD prepend a new segment of type AS_CONFED_SEQUENCE and prepend its own AS number to this new segment." | In rule b) 1) the value to prepend is the Member-AS Number and in rule c) 2) the AS Confederation Identifier, but both overflow sentences say "its own AS number", which in a confederation is ambiguous (Section 4 distinguishes the two). The behaviour on overflow is also only SHOULD, leaving the alternative unspecified. | ambiguity | not checked |
| RA-0115 | 5 | "If a BGP speaker receives such an UPDATE message, it SHALL treat the message as having a malformed AS_PATH according to the procedures of [BGP-4], Section 6.3" | Both error rules require session reset (RFC 4271 6.3). RFC 7606 (which does not list RFC 5065 as updated) makes a malformed AS_PATH "treat-as-withdraw" (7606 7.2), so the action a confederation speaker takes depends on which document is followed. "It is a error" (typo) and "AS_CONFED_SET or AS_CONFED_SEQUENCE attributes" (they are segment types, not attributes) are editorial. | ambiguity | not checked |

### RFC 5291: Outbound Route Filtering Capability for BGP-4 {#ra_rfc5291}

Depth: read (normative statements, formats). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0116 | 6 | "A BGP speaker that advertises the Outbound Route Filtering Capability to a peer using BGP Capabilities advertisement [BGP-CAP] does not have to advertise the BGP Route Refresh Capability to that peer." | RFC 2918 Section 4 allows a speaker to send ROUTE-REFRESH "only if it has received the Route Refresh Capability from its peer". Under this section an ORF-capable peer may send ROUTE-REFRESH messages carrying ORF entries to a speaker that advertised only the ORF capability, which RFC 2918 forbids; RFC 5291 does not list RFC 2918 as updated, so the precedence is implicit (and RFC 7313 later repeats the RFC 2918 rule for Enhanced Route Refresh). | contradiction | not checked |

### RFC 5398: Autonomous System (AS) Number Reservation for Documentation Use {#ra_rfc5398}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5492: Capabilities Advertisement with BGP-4 {#ra_rfc5492}

Depth: part. Errata: checked (checked: 1 (3882 rejected, technical)). Obsoletes: RFC 3392.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0024 | 3 | "In this case, the speaker SHOULD attempt to re-establish a BGP connection with the peer without sending to the peer the Capabilities Optional Parameter." | A speaker that needs capabilities (for example to exchange only IPv6 routes, or four-octet AS numbers) gains nothing from a session without them, and the fallback is the downgrade path an attacker can trigger with a forged NOTIFICATION (see RFC 4724). The erratum asking to make the retry a local choice was rejected because the SHOULD already allows it; the text gives no guidance on when not to retry. | ambiguity | 3882 (Rejected) |

### RFC 5543: BGP Traffic Engineering Attribute {#ra_rfc5543}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 5668: 4-Octet AS Specific BGP Extended Community {#ra_rfc5668}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 5701: IPv6 Address Specific BGP Extended Community Attribute {#ra_rfc5701}

Depth: read (encoding sections). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6286: Autonomous-System-Wide Unique BGP Identifier for BGP-4 {#ra_rfc6286}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0117 | 2.2, 3 | "If the BGP Identifier field of the OPEN message is zero, or if it is the same as the BGP Identifier of the local BGP speaker and the message is from an internal peer, then the Error Subcode is set to "Bad BGP Identifier"." | Section 3 says "the whole confederation is considered as one AS for the purpose of supporting the AS-wide Unique BGP Identifier", so a confederation-external peer (another member AS) sharing the local BGP Identifier is as much an error as an internal one; 2.2 limits the check to "an internal peer", and 2.3's collision rule for identical identifiers (larger AS wins) would then apply between member ASes. Section 3 also has the typo "AGGREAGTOR". | ambiguity | not checked; **proposed erratum below** |

Proposed erratum RA-0117 (RFC 6286, Section 2.2, 3; type: Technical):

```
Original Text
-------------
   and the message is from an internal peer, then the Error Subcode
   is set to "Bad BGP Identifier".

Corrected Text
--------------
   and the message is from an internal peer or from a peer in
   another member AS of the same confederation, then the Error
   Subcode is set to "Bad BGP Identifier".

Notes
-----
   Also: "AGGREAGTOR" in Section 3 should read "AGGREGATOR".
```

### RFC 6368: Internal BGP as the Provider/Customer Edge Protocol for BGP/MPLS IP Virtual Private Networks (VPNs) {#ra_rfc6368}

Depth: deep (5, 6). Errata: errata exist; not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0118 | 5 | "If its Partial flag is set and its Neighbor-Complete flag is clear, the UPDATE is treated as a route withdraw as discussed in [OPT-TRANS-BGP]." | The "Neighbor-Complete flag" is defined only in an expired Internet-Draft cited informatively ([OPT-TRANS-BGP]), so the rule cannot be applied from the published RFCs. RFC 7606 Section 7.16 replaces the paragraph with plain treat-as-withdraw and removes the reference; RFC 6368 readers need that update to implement the section. The malformation list (length below 4, MP_REACH / MP_UNREACH inside, malformed inner attributes) is unchanged. | error | not checked; fixed normatively by RFC 7606 7.16 |

### RFC 6608: Subcodes for BGP Finite State Machine Error {#ra_rfc6608}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0119 | 4 | "If a BGP speaker receives an unexpected message (e.g., OPEN/UPDATE/ROUTE-REFRESH message) on a session in OpenConfirm state, it MUST send a NOTIFICATION message" | In RFC 4271 (8.2.2, OpenConfirm) a received OPEN (Event 19) runs connection collision detection (6.8) rather than being an FSM error; listing OPEN as the example of an unexpected message in OpenConfirm invites implementations to reset the connection where RFC 4271 resolves a collision. The document also does not say which subcode applies in Connect / Active (no subcode is defined; 0 "Unspecified Error" is the only fit). | ambiguity | not checked |

### RFC 6793: BGP Support for Four-Octet Autonomous System (AS) Number Space {#ra_rfc6793}

Depth: deep. Errata: checked (checked: 1 (held, technical, section 8 MIB reference)). Obsoletes: RFC 4893. Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0025 | 8 | "If the BGP4-MIB [RFC4273] is supported, there are no additional manageability concerns that arise from the use of four-octet AS numbers" | RFC 4273 types AS numbers as Integer32 (0..65535), so it cannot carry four-octet AS numbers. | error | 4538 (Held) |

### RFC 6938: Deprecation of BGP Path Attributes: DPA, ADVERTISER, and RCID_PATH / CLUSTER_ID {#ra_rfc6938}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6996: Autonomous System (AS) Reservation for Private Use {#ra_rfc6996}

Depth: light (AS ranges). Errata: no verified errata in the index; page not read. Updates: RFC 1930.

Nothing notable found at this depth.

### RFC 7153: IANA Registries for BGP Extended Communities {#ra_rfc7153}

Depth: read (registry document). Errata: no verified errata in the index; page not read. Updates: RFC 4360, RFC 5701.

Nothing notable found at this depth.

### RFC 7300: Reservation of Last Autonomous System (AS) Numbers {#ra_rfc7300}

Depth: light (AS ranges). Errata: no verified errata in the index; page not read. Updates: RFC 1930.

Nothing notable found at this depth.

### RFC 7311: The Accumulated IGP Metric Attribute for BGP {#ra_rfc7311}

Depth: deep (3, 4 in full). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0120 | 3.4.3, 3.2 | "In all the computations discussed in this section, the AIGP value MUST be capped at its maximum unsigned value 0xffffffffffffffff." | Section 3.2 says that an AIGP attribute whose first AIGP TLV "contains the maximum value 0xffffffffffffffff ... SHOULD be considered to be malformed and SHOULD be discarded". A speaker that caps an overflowing sum as 3.4.3 requires therefore sends a value that every compliant receiver discards, so the route silently loses its AIGP attribute one hop later and, under Section 4.1, is then removed from consideration whenever another route still carries one. Capping at 0xfffffffffffffffe, or withdrawing the attribute, would avoid this; the text does not say which. | contradiction | not checked; **proposed erratum below** |
| RA-0121 | 3.4.3 | "If D is above a configurable threshold, set the AIGP TLV value to Xattr+D.  If D is below a configurable threshold, set the AIGP TLV value to Xattr." | D equal to the threshold is not covered. In the non-recursive case the same section requires that "A MUST be increased by a non-zero amount", while here a D below the threshold leaves the value unchanged after a next-hop change; the two rules disagree on whether a next-hop change may leave the AIGP value as received. | ambiguity | not checked |

Proposed erratum RA-0120 (RFC 7311, Section 3.4.3, 3.2; type: Technical):

```
Original Text
-------------
   In all the computations discussed in this section, the AIGP value
   MUST be capped at its maximum unsigned value 0xffffffffffffffff.

Corrected Text
--------------
   In all the computations discussed in this section, the AIGP value
   MUST be capped at 0xfffffffffffffffe, one less than the maximum
   unsigned value, which Section 3.2 treats as malformed.

Notes
-----
   Section 3.2: "If an AIGP attribute is received and its first AIGP
   TLV contains the maximum value 0xffffffffffffffff, the attribute
   SHOULD be considered to be malformed and SHOULD be discarded".
```

### RFC 7313: Enhanced Route Refresh Capability for BGP-4 {#ra_rfc7313}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 2918.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0122 | 4 | "When a BGP speaker receives a BoRR message from a peer, it MUST mark all the routes with the given Address Family Identifier and Subsequent Address Family Identifier ... from that peer as stale." | The text does not cover a second BoRR for the same <AFI, SAFI> before the EoRR of the first (whether stale marking restarts, or routes refreshed since the first BoRR become stale again), nor a session reset or graceful restart while routes are marked stale by a refresh, nor whether stale routes stay eligible for best-path selection until EoRR (implied, not stated). | ambiguity | not checked |
| RA-0123 | 6, 3.2 | "This document also defines two new subcodes for the Route Refresh message.  They have been registered with the IANA in a new registry as follows: ... Registry: "BGP Route Refresh Subcodes"" | Section 3.2 calls the field "Message Subtype" and lists values 0, 1, 2 and 255; Section 6 calls them "subcodes" and says two are defined. The registry name and the field name differ, which also clashes with the NOTIFICATION "subcode" defined in Section 5. | editorial | not checked |

### RFC 7447: Deprecation of BGP Entropy Label Capability Attribute {#ra_rfc7447}

Depth: deep. Errata: not checked. Updates: RFC 6790.

Nothing notable found at this depth.

### RFC 7606: Revised Error Handling for BGP UPDATE Messages {#ra_rfc7606}

Depth: deep. Errata: checked (checked: 1 (held, editorial: 7.16 "treat as withdraw" spelling)). Updates: RFC 1997, RFC 4271, RFC 4360, RFC 4456, RFC 4760, RFC 5543, RFC 5701, RFC 6368.

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

### RFC 7607: Codification of AS 0 Processing {#ra_rfc7607}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0124 | 2, 4 | "By ensuring that all implementations that see AS 0 in a route ignore that route, we prevent a malicious party from announcing routes containing AS 0" | Section 2 sends AS 0 in AGGREGATOR to RFC 7606 and AS 0 in AS4_PATH / AS4_AGGREGATOR to RFC 6793. Both specify "attribute discard" for those attributes (RFC 7606 7.7; RFC 6793 6), so the route itself is kept and only the attribute is dropped. Only AS 0 in AS_PATH leads to treat-as-withdraw. The Security Considerations claim that every route containing AS 0 is ignored therefore holds only for AS_PATH; a route with AS 0 only in AS4_PATH is accepted with the AS_PATH it carries. | contradiction | not checked; **proposed erratum below** |
| RA-0125 | 2 | "If a BGP speaker receives zero as the peer AS in an OPEN message, it MUST abort the connection and send a NOTIFICATION with Error Code "OPEN Message Error" and subcode "Bad Peer AS"" | With four-octet AS support the peer AS is carried in the Four-octet AS Number Capability (RFC 6793), with AS_TRANS in My Autonomous System; the text does not say that a capability value of 0 is covered, nor whether a My Autonomous System of 0 is still an error when the capability carries a valid AS. | ambiguity | not checked |

Proposed erratum RA-0124 (RFC 7607, Section 2, 4; type: Technical):

```
Original Text
-------------
   By ensuring that all implementations that see AS 0 in a route
   ignore that route, we prevent a malicious party from announcing
   routes containing AS 0 in an attempt to hijack those resources.

Corrected Text
--------------
   By ensuring that all implementations that see AS 0 in the AS_PATH
   of a route ignore that route (and discard AGGREGATOR, AS4_PATH or
   AS4_AGGREGATOR attributes containing AS 0), we prevent a
   malicious party from announcing routes containing AS 0 in an
   attempt to hijack those resources.

Notes
-----
   RFC 7606 Section 7.7 and RFC 6793 Section 6 handle malformed
   AGGREGATOR, AS4_PATH and AS4_AGGREGATOR by attribute discard, not
   treat-as-withdraw.
```

### RFC 7611: BGP ACCEPT_OWN Community Attribute {#ra_rfc7611}

Depth: read. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0126 | 2, 2.3 | "The functionality SHOULD default to being disabled / ACCEPT_OWN handling SHOULD be controlled by configuration, and if controlled by configuration, it MUST default to being disabled." | Section 2 makes "disabled by default" a SHOULD, Section 2.3 a MUST (when configurable). Section 2.1 identifies the source VRF only by RD equality, which is ambiguous where the same RD is configured on more than one VRF of the router. | contradiction | not checked |

### RFC 7911: Advertisement of Multiple Paths in BGP {#ra_rfc7911}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0030 | 3 | "If a BGP speaker receives a message to withdraw a prefix with a Path Identifier not seen before, it SHOULD silently ignore it." | Nothing is said about an UPDATE whose NLRI cannot be parsed because the two sides disagree on whether ADD-PATH applies to a family; with ADD-PATH the 4-octet Path Identifier makes misparsing likely to look valid. RFC 7606 5.3 does not cover it. | ambiguity | errata not checked |
| RA-0127 | 4 | "If any other value is received, then the capability SHOULD be treated as not understood and ignored [RFC5492]. / MUST do so by including the information in a single instance of the ADD-PATH Capability." | "The capability" can be read as the whole ADD-PATH Capability (all tuples, so one bad tuple disables ADD-PATH for every family) or as the one <AFI, SAFI, Send/Receive> tuple. The section also does not say what a receiver does with more than one instance of the capability, with the same <AFI, SAFI> listed twice, or with a Capability Length that is not a multiple of 4. | ambiguity | none found; **proposed erratum below** |
| RA-0128 | 3, 5 | "In order to carry the Path Identifier in an UPDATE message, the NLRI encoding MUST be extended by prepending the Path Identifier field" | The text and figure cover only the NLRI encoding; that the IPv4 Withdrawn Routes field and MP_UNREACH_NLRI also carry the Path Identifier follows only from Section 5 ("withdraw a prefix with a Path Identifier"). The interaction with label-carrying NLRI (RFC 8277) and other AFI encodings is not stated. | ambiguity | none found |

Proposed erratum RA-0127 (RFC 7911, Section 4; type: Technical):

```
Original Text
-------------
   If any other value is received, then the capability SHOULD be
   treated as not understood and ignored [RFC5492].

Corrected Text
--------------
   If any other value is received, then that <AFI, SAFI> tuple
   SHOULD be ignored; the remaining tuples are processed. If the
   same <AFI, SAFI> appears more than once, or the capability
   appears more than once, only the first occurrence is used.

Notes
-----
   As written, a single bad tuple could disable ADD-PATH for all
   families. Handling of repeated instances, repeated <AFI, SAFI>
   tuples and a length that is not a multiple of four is not
   specified.
```

### RFC 7947: Internet Exchange BGP Route Server {#ra_rfc7947}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0129 | 3, 2.2.2.2 | "The AS_PATH check described in Section 2.2.2 is normally enabled in order to check for malformed AS paths. ... this check is also used to detect BGP loops; removing the check could potentially cause routing loops to be formed." | The check meant is the leftmost-AS check of Section 2.2.2.2 (first AS equals the peer's AS, RFC 4271 6.3). That check does not detect loops; loop detection is the separate own-AS-in-path check of RFC 4271 9.1.2, which is unaffected when the leftmost-AS check is disabled for a route server peer. The security rationale therefore overstates the risk and may lead implementers to disable the wrong check. | ambiguity | not checked; **proposed erratum below** |

Proposed erratum RA-0129 (RFC 7947, Section 3, 2.2.2.2; type: Technical):

```
Original Text
-------------
   The AS_PATH check described in Section 2.2.2 is normally enabled
   in order to check for malformed AS paths.

Corrected Text
--------------
   The AS_PATH check described in Section 2.2.2.2 (leftmost AS equal
   to the peer's AS) is normally enabled in order to check for
   malformed AS paths. Disabling it does not disable the AS_PATH
   loop detection of Section 9.1.2 of [RFC4271].

Notes
-----
   Loop detection in BGP is performed by checking for the local AS
   in the AS_PATH, which is independent of the leftmost-AS check.
```

### RFC 7948: Internet Exchange BGP Route Server Operations {#ra_rfc7948}

Depth: light (lines with requirement words and section references scanned). Errata: not checked. 

Nothing notable found at this depth.

### RFC 7999: BLACKHOLE Community {#ra_rfc7999}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0130 | 3.3, 3.1 | "The error handling for this community follows the process in [RFC7606] that causes a malformed community to be treated as withdrawn." | A single 4-octet community value cannot be malformed; RFC 7606 7.8 applies treat-as-withdraw to a COMMUNITIES attribute whose length is not a non-zero multiple of 4. The sentence reads as if a BLACKHOLE value itself could trigger withdrawal. Section 3.1 also has "a network that it not using it" for "that is not using it". | editorial | not checked |

### RFC 8092: BGP Large Communities Attribute {#ra_rfc8092}

Depth: deep. Errata: checked (checked: 1 (4962 held, editorial, attribute name)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0131 | 3, 4 | "A receiving speaker MUST silently remove redundant BGP Large Community values from a BGP Large Community attribute. / contains all of the BGP Large Communities attributes from all of the aggregated routes." | The attribute is named "BGP Large Communities" (IANA LARGE_COMMUNITY), but the text alternates with "BGP Large Community attribute" (erratum 4962). Section 4 says the aggregate contains all the "attributes" where the attribute values are meant, and does not restate that duplicates are removed when merging. | editorial | 4962 (Held) |

### RFC 8093: Deprecation of BGP Path Attribute Values 30, 31, 129, 241, 242, and 243 {#ra_rfc8093}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8205: BGPsec Protocol Specification {#ra_rfc8205}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8212: Default External BGP (EBGP) Route Propagation Behavior without Policies {#ra_rfc8212}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0132 | 3 | "Routes contained in an Adj-RIB-In associated with an EBGP peer SHALL NOT be considered eligible in the Decision Process if no explicit Import Policy has been applied." | "Explicit Import Policy" is not defined: an empty policy, or a policy whose terms match nothing and fall through, may or may not count as explicit. The text also does not say whether sessions to confederation peers in another member AS (RFC 5065) are "EBGP" for this purpose, or whether the rule applies to every AFI/SAFI (for example BGP-LS or VPN families on an EBGP session). | ambiguity | not checked |

### RFC 8277: Using BGP to Bind MPLS Labels to Address Prefixes {#ra_rfc8277}

Depth: deep. Errata: not checked. Obsoletes: RFC 3107.

Nothing notable found at this depth.

### RFC 8326: Graceful BGP Session Shutdown {#ra_rfc8326}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8538: Notification Message Support for BGP Graceful Restart {#ra_rfc8538}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 4724.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0133 | 4.1, 9 | "an implementation MUST support a (configurable) timer, called the "stale timer", that imposes this upper bound. / To mitigate the consequent risk that an attacker could use repeated session resets to prevent stale routes from ever being deleted, we make the stale timer mandatory" | Security gap: With the N bit exchanged, stale routes are no longer deleted on consecutive restarts, and Section 9 relies on the stale timer to bound their lifetime. The text does not say when the stale timer starts or whether a further session termination restarts it. If each termination (or each new session) restarts it, repeated resets keep stale routes indefinitely, which is exactly the risk Section 9 claims to mitigate. The RFC 4724 Restart Time interacts in the same way. | error | none found; **proposed erratum below** |
| RA-0134 | 4 | "When a BGP speaker resets its session due to a HOLDTIME expiry, it should generate the relevant BGP NOTIFICATION message as mentioned in [RFC4271] but subsequently MUST follow the rules for the Receiving Speaker" | The sentence is not conditioned on the N bit having been exchanged, unlike the preceding paragraph. Read literally, it extends Graceful Restart helper behaviour to hold-timer expiry on every GR session, including peers without N, for which RFC 4724 treats any NOTIFICATION as ending GR. It is also not said whether N negotiated on the previous session applies to a NOTIFICATION sent during OpenSent / OpenConfirm of the next one. | ambiguity | none found |

Proposed erratum RA-0133 (RFC 8538, Section 4.1, 9; type: Technical):

```
Original Text
-------------
   To put an upper bound on the amount of time a router retains the
   stale routes, an implementation MUST support a (configurable)
   timer, called the "stale timer", that imposes this upper bound.

Corrected Text
--------------
   To put an upper bound on the amount of time a router retains the
   stale routes, an implementation MUST support a (configurable)
   timer, called the "stale timer", that imposes this upper bound.
   The stale timer is started when routes from the peer are first
   marked stale and is not restarted by subsequent session
   terminations while those routes remain stale.

Notes
-----
   Section 9 states the stale timer prevents an attacker from
   keeping stale routes alive with repeated resets, but nothing in
   Section 4.1 prevents the timer from being restarted on each
   reset.
```

### RFC 8571: BGP - Link State (BGP-LS) Advertisement of IGP Traffic Engineering Performance Metric Extensions {#ra_rfc8571}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8654: Extended Message Support for BGP {#ra_rfc8654}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0135 | 4 | "the speaker SHOULD try to reduce the outgoing message size by removing attributes eligible under the "attribute discard" approach of [RFC7606]." | RFC 7606 defines "attribute discard" as an error-handling action for specific malformed attributes, not a class of well-formed attributes that may be dropped for size; which attributes are "eligible" when they are well-formed is not defined (RFC 7606 names it only for a few, such as ATOMIC_AGGREGATE and AGGREGATOR). Dropping a well-formed transitive attribute also changes what downstream ASes receive, which Section 8 notes as an attack vector but does not bound. | ambiguity | none found; **proposed erratum below** |
| RA-0136 | 4, 5 | "A BGP speaker MAY send BGP Extended Messages to a peer only if the BGP Extended Message Capability was received from that peer." | Sending depends only on the peer's advertisement and receiving only on one's own, so the limit can differ per direction. Section 5 bounds NOTIFICATIONs to 4096 octets toward a peer without the capability but does not say whether the data field of a NOTIFICATION reporting an oversize message (Bad Message Length, RFC 4271 6.1) is truncated, nor whether ROUTE-REFRESH and other non-UPDATE messages follow the same rule. | ambiguity | none found |

Proposed erratum RA-0135 (RFC 8654, Section 4; type: Technical):

```
Original Text
-------------
   the speaker SHOULD try to reduce the outgoing message size by
   removing attributes eligible under the "attribute discard"
   approach of [RFC7606].

Corrected Text
--------------
   the speaker SHOULD try to reduce the outgoing message size by
   removing optional attributes for which [RFC7606] specifies the
   "attribute discard" approach (for example, ATOMIC_AGGREGATE and
   AGGREGATOR), as these do not affect route selection.

Notes
-----
   RFC 7606 attribute discard is a per-attribute error-handling
   rule; this section reuses it as a size-reduction rule without
   saying which well-formed attributes qualify.
```

### RFC 8669: Segment Routing Prefix Segment Identifier Extensions for BGP {#ra_rfc8669}

Depth: deep. Errata: checked (checked: 1 (6681 verified, editorial, Acknowledgements)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0137 | 4.1, 9 | "If multiple different prefixes are received with the same label index, all of the different prefixes MUST have their BGP Prefix-SID attribute considered to be "conflicting"." | Security gap: Any speaker that can inject a prefix into the SR domain with the label index of another prefix makes both conflicting, so the victim prefix loses its SR label everywhere (falls back to a dynamic label) without any authorisation of the injected prefix. The Security Considerations address only log flooding. The rule also does not say whether locally originated prefixes take part, whether prefixes of different AFIs (IPv4 / IPv6 LU) share the index space, or how "SRGB_Start" applies when the local SRGB has several ranges (Section 3.2 allows multi-range SRGBs; the derivation L = L_I + SRGB_Start assumes one). | error | not checked |
| RA-0138 | 4, 5.1 | "A BGP speaker receiving a BGP Prefix-SID attribute from an External BGP (EBGP) neighbor residing outside the boundaries of the SR domain MUST discard the attribute unless it is configured to accept the attribute from the EBGP neighbor." | The SR domain boundary is not a BGP concept, so whether a given EBGP neighbour is "outside" depends on configuration the RFC does not define; read with Section 8 ("one or more ASes"), an implementation without such configuration cannot tell, and either discards from all EBGP peers (breaking the RFC 8670 multi-AS model) or from none. | ambiguity | not checked |

### RFC 8814: Signaling Maximum SID Depth (MSD) Using the Border Gateway Protocol - Link State {#ra_rfc8814}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8950: Advertising IPv4 Network Layer Reachability Information (NLRI) with an IPv6 Next Hop {#ra_rfc8950}

Depth: deep. Errata: not checked. Obsoletes: RFC 5549.

Nothing notable found at this depth.

### RFC 9003: Extended BGP Administrative Shutdown Communication {#ra_rfc9003}

Depth: deep. Errata: not checked. Obsoletes: RFC 8203. Updates: RFC 4486.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0139 | 2, 4 | "Length: This 8-bit field represents the length of the Shutdown Communication field in octets. When the length value is zero, no Shutdown Communication field follows." | No receive rule is given for a Length larger than the data remaining in the NOTIFICATION, or for octets after the Shutdown Communication; Section 4 covers only invalid UTF-8. A receiver may log a truncated string, the whole data as hex, or nothing. | ambiguity | none found |

### RFC 9012: The BGP Tunnel Encapsulation Attribute {#ra_rfc9012}

Depth: part (2, 3.1, 4.3, 6, 13 read; tunnel-type specific sub-TLVs 3.2-3.7 and sections 8-11 scanned). Errata: no errata page found by search (not confirmed). Obsoletes: RFC 5512, RFC 5566. Updates: RFC 5640.

Nothing notable found at this depth.

### RFC 9015: BGP Control Plane for the Network Service Header in Service Function Chaining {#ra_rfc9015}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9072: Extended Optional Parameters Length for BGP OPEN Message {#ra_rfc9072}

Depth: deep. Errata: not checked. Updates: RFC 4271.

Nothing notable found at this depth.

### RFC 9085: Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing {#ra_rfc9085}

Depth: part. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9086: Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing BGP Egress Peer Engineering {#ra_rfc9086}

Depth: part (sections 3-5 and the SID sub-TLV encodings read; manageability scanned). Errata: not checked. 

Nothing notable found at this depth.

### RFC 9088: Signaling Entropy Label Capability and Entropy Readable Label Depth Using IS-IS {#ra_rfc9088}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9104: Distribution of Traffic Engineering Extended Administrative Groups Using the Border Gateway Protocol - Link State (BGP-LS) {#ra_rfc9104}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0140 | 2 vs RFC 9552 8.2.2 | "The length value MUST be a multiple of 4. If the length is not a multiple of 4, the TLV MUST be considered malformed." | "Malformed" is not tied to an action. Under RFC 9552 8.2.2 a propagating BGP-LS speaker checks only TLV framing and does not check "the length of a fixed-length TLV", while a consumer discards a malformed TLV; whether a length not a multiple of 4 is a framing error (affecting the whole BGP-LS Attribute and hence the UPDATE) or a TLV-level semantic error (TLV ignored) is left open. | ambiguity | none found |

### RFC 9234: Route Leak Prevention and Detection Using Roles in UPDATE and OPEN Messages {#ra_rfc9234}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0141 | 5 | "On egress from the Internet-facing AS, the OTC Attribute MUST NOT contain a value other than the Internet-facing ASN. ... Once the OTC Attribute has been set, it MUST be preserved unchanged (this also applies to an AS Confederation)." | If an OTC was set inside the private-ASN or confederation part of the network (to a private ASN or a Member-AS number), the egress rules require it not to leave with that value, while the preservation rule forbids changing it. The text does not say whether the egress router must rewrite the value, drop the attribute, or not advertise the route; each choice changes leak detection downstream. The confederation paragraph has the same conflict ("an UPDATE MUST NOT contain an OTC Attribute with a value corresponding to any Member-AS Number"). | contradiction | none found; **proposed erratum below** |
| RA-0142 | 4.2 | "For backward compatibility, if the BGP Role Capability is sent but one is not received, the BGP Speaker SHOULD ignore the absence of the BGP Role Capability and proceed with session establishment." | The case of a Role Capability received but none sent (no local role configured) is not covered: whether the speaker applies Section 5 with the role implied by the peer's, or ignores the capability. Section 4 makes configuring a role only a SHOULD, so the case is ordinary. | ambiguity | none found |
| RA-0143 | 5 | "If a route is to be advertised to a Customer, a Peer, or an RS-Client (when the sender is an RS), and the OTC Attribute is not present, then when advertising the route, an OTC Attribute MUST be added" | The parenthetical "(when the sender is an RS)" is redundant by Table 2 (a remote RS-Client implies a local RS) and can be misread as applying to the whole list. The rule is applied to routes from any source, including routes originated locally, which the text does not mention. | ambiguity | none found |

Proposed erratum RA-0141 (RFC 9234, Section 5; type: Technical):

```
Original Text
-------------
   Once the OTC Attribute has been set, it MUST be preserved
   unchanged (this also applies to an AS Confederation).

Corrected Text
--------------
   Once the OTC Attribute has been set, it MUST be preserved
   unchanged (this also applies to an AS Confederation), except that
   on egress from an AS Confederation or from an Internet-facing AS
   an OTC Attribute whose value is a Member-AS Number or a private
   ASN MUST be replaced by the AS Confederation Identifier or the
   Internet-facing ASN, respectively.

Notes
-----
   Either the egress rules are exceptions to preservation, or such
   routes must not be advertised; the text should say which.
```

### RFC 9384: A BGP Cease NOTIFICATION Subcode for Bidirectional Forwarding Detection (BFD) {#ra_rfc9384}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0144 | 4 | "When the procedures in [RFC8538] for sending a NOTIFICATION message with a "Cease" code and "Hard Reset" subcode are required, and the BGP connection is being terminated because BFD has gone into the Down state, the "BFD Down" subcode SHOULD be encapsulated in the Hard Reset's data portion" | RFC 8538 5 decides when a Hard Reset is "required" by the Cease subcode; BFD Down (10) postdates it and is not in its list, so whether a BFD Down termination with GR negotiated is a Hard Reset (flush) or a normal GR-preserving reset is not settled by either document; RFC 5882 4.3 adds the C-bit dimension. | ambiguity | none found |

### RFC 9494: Long-Lived Graceful Restart for BGP {#ra_rfc9494}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 6368.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0145 | 4.2 | "However, in the case of consecutive restarts, the previously marked stale routes MUST NOT be deleted before the timer for the Long-Lived Stale Time expires." | RFC 4724 4.2 requires stale routes to be deleted when the session resets again before End-of-RIB ("consecutive restarts"); this document keeps them until the LLST timer expires, and later in the same section removes "any remaining routes (for the AFI/SAFI whose LLST timer expired)" when the session resets before synchronisation. It does not say whether the RFC 4724 rule still applies to routes that are only GR-stale (still in the Restart Time period, not yet LLGR-stale) when the second reset happens, nor that it updates RFC 4724 4.2 (the header lists only RFC 6368). | contradiction | none found; **proposed erratum below** |
| RA-0146 | 4.3, 4.6, 4.7.1 | "The route SHOULD NOT be advertised to any neighbor from which the Long-Lived Graceful Restart Capability has not been received. The exception is described in Section 4.6." | Section 4.3 restricts LLGR-stale routes only towards neighbours that did not send the LLGR Capability; an eBGP neighbour that did send it may receive them. Section 4.6 (partial deployment) only concerns internal neighbours without the capability, and Section 4.7.1 the PE-CE eBGP case. Readers sometimes take 4.6's "MUST be internal" as a general ban on eBGP. | ambiguity | none found |
| RA-0147 | 4.2 | "The interval for which they are retained is limited by the sum of the Restart Time in the received Graceful Restart Capability and the Long-Lived Stale Time ... the timer continues to run once the session has re-established." | The first sentence bounds retention while the session is down; the later text keeps the LLST timer running after re-establishment until End-of-RIB, so retention can exceed the stated sum only by the synchronisation time, and the Selection_Deferral_Timer of RFC 4724 also ends synchronisation. Whether a local cap on LLST (allowed: "MAY be reduced by local configuration") applies to a timer already running is not said. | ambiguity | none found |

Proposed erratum RA-0145 (RFC 9494, Section 4.2; type: Technical):

```
Original Text
-------------
   However, in the case of consecutive restarts, the previously
   marked stale routes MUST NOT be deleted before the timer for the
   Long-Lived Stale Time expires.

Corrected Text
--------------
   However, in the case of consecutive restarts, and notwithstanding
   Section 4.2 of [RFC4724], the previously marked stale routes MUST
   NOT be deleted before the timer for the Long-Lived Stale Time
   expires. This applies to routes retained during the Restart Time
   period as well as during the Long-Lived Stale Time period.

Notes
-----
   RFC 4724 4.2 says such routes MUST be deleted; implementations of
   both documents need to know which rule wins for which routes.
```

### RFC 9514: Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing over IPv6 (SRv6) {#ra_rfc9514}

Depth: part. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9552: Distribution of Link-State and Traffic Engineering Information Using BGP {#ra_rfc9552}

Depth: deep. Errata: checked (checked: 2 (both verified, editorial)). Obsoletes: RFC 7752, RFC 9029.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0032 | 5.3.1.1 | "\|O\|T\|E\|B\|R\|V\|   \|   (Figure 15) against Table 7: 'A' \| Attached Bit \| [ISO10589]" | The figure names the second bit "T"; Table 7 calls it "A" (IS-IS Attached bit). The erratum corrects the figure. An implementer working from the figure gets the bit name wrong but the position right. | editorial | 7789 (Verified) |
| RA-0033 | 5.2.2 | "... and in the case of links having only IPv6 link-local addressing ..." | Stray "and" makes the sentence read as a third case. | editorial | 8766 (Verified) |

### RFC 9687: Border Gateway Protocol 4 (BGP-4) Send Hold Timer {#ra_rfc9687}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 4271.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0148 | 4.3, 4.4 | "Each time the local system sends a BGP message, it restarts the SendHoldTimer unless the SendHoldTime value is zero or the negotiated HoldTime value is zero" | "Sends" is not defined: queued by BGP, accepted by the TCP socket, or acknowledged. With a socket send buffer, writes succeed for a while after the peer's window closes, so a timer restarted on socket writes fires later than one restarted only when data leaves the local buffers; the RFC's scenario (zero receive window) depends on that choice. Section 4.4 also requires SendHoldTime > HoldTime without saying whether the configured or the negotiated HoldTime is meant (the default in Section 6 uses the negotiated one). | ambiguity | none found |

### RFC 9774: Deprecation of AS_SET and AS_CONFED_SET in BGP {#ra_rfc9774}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 6472. Updates: RFC 4271, RFC 5065.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0149 | 3 | "MUST use the "treat-as-withdraw" error handling behavior per [RFC7606] upon reception of BGP UPDATE messages containing AS_SETs or AS_CONFED_SETs in the AS_PATH or AS4_PATH [RFC6793]." | RFC 6793 forbids confederation segments in AS4_PATH and has the receiver discard them, so an AS_CONFED_SET in AS4_PATH is removed under RFC 6793 but makes the route withdrawn under this document. This document says it updates RFC 4271 and RFC 5065 but not RFC 6793, and does not say which handling applies to an AS_CONFED_SET in AS4_PATH. | contradiction | none found; **proposed erratum below** |

Proposed erratum RA-0149 (RFC 9774, Section 3; type: Technical):

```
Original Text
-------------
   upon reception of BGP UPDATE messages containing AS_SETs or
   AS_CONFED_SETs in the AS_PATH or AS4_PATH [RFC6793].

Corrected Text
--------------
   upon reception of BGP UPDATE messages containing AS_SETs or
   AS_CONFED_SETs in the AS_PATH, or AS_SETs in the AS4_PATH
   [RFC6793] (confederation segments in AS4_PATH continue to be
   handled as specified in [RFC6793]).

Notes
-----
   RFC 6793 is not listed as updated.
```

### RFC 9793: BGP Extensions for Bit Index Explicit Replication (BIER) {#ra_rfc9793}

Depth: light. Errata: checked (checked: 1 (8463 Verified technical, section 6 example next hop BFR1 -> BFER1)). 

Nothing notable found at this depth.

### RFC 9830: Advertising Segment Routing Policies in BGP {#ra_rfc9830}

Depth: deep (2.1, 2.4, 2.4.4, 3, 4, 5 in full; sub-TLV encodings 2.4.1-2.4.8 scanned). Errata: no errata page found by search (not confirmed). Updates: RFC 9012.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0150 | 5 vs RFC 9012 13 | "In case of any error detected, either at the attribute or its TLV/sub-TLV level, the "treat-as-withdraw" strategy MUST be applied." | RFC 9012 Section 13, which the same paragraph says MUST be applied, treats a malformed sub-TLV "as if it were an unrecognized sub-TLV" (ignored and propagated) and an unrecognized sub-TLV as absent. For SAFI 73 this document instead withdraws the route on any sub-TLV error, and 4.2.2 makes an unrecognized sub-TLV a reason for "not usable" (SHOULD NOT) rather than ignoring it. A speaker cannot follow both texts for a malformed RFC 9012 sub-TLV (for example a Color sub-TLV) inside an SR Policy tunnel TLV; the scope of the override (all sub-TLVs, or only those of Section 2.4) is not stated. | contradiction | none found; **proposed erratum below** |
| RA-0151 | 4.2.1 | "The SR Policy update MUST have either the NO_ADVERTISE community, at least one Route Target extended community in IPv4-address format, or both. If a router supporting this specification receives an SR Policy update with no Route Target extended communities and no NO_ADVERTISE community, the update MUST be considered to be malformed." | An update carrying Route Targets only in other formats (2-octet or 4-octet AS) and no NO_ADVERTISE fails the first sentence but not the second; whether it is malformed (treat-as-withdraw) or valid but unusable (4.2.2) is not settled. 4.2.2 also does not say whether the Local Administrator field of an IPv4-address RT must be zero for it to "match the BGP Identifier". | ambiguity | none found |

Proposed erratum RA-0150 (RFC 9830, Section 5 vs RFC 9012 13; type: Technical):

```
Original Text
-------------
   In case of any error detected, either at the attribute or its
   TLV/sub-TLV level, the "treat-as-withdraw" strategy MUST be
   applied.

Corrected Text
--------------
   In case of any error detected, either at the attribute or its
   TLV/sub-TLV level (including sub-TLVs defined in [RFC9012],
   notwithstanding Section 13 of [RFC9012]), the "treat-as-withdraw"
   strategy MUST be applied to SR Policy SAFI updates.

Notes
-----
   RFC 9012 ignores malformed sub-TLVs (except the Tunnel Egress
   Endpoint); this document withdraws the update.
```

### RFC 9831: Segment Type Extensions for BGP Segment Routing (SR) Policy {#ra_rfc9831}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 10039: Interconnecting EVPN and IPVPN Domains {#ra_rfc10039}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

## IS-IS, IGP TE, Segment Routing and IP FRR {#ra_isis}

62 RFCs in this area (39 deep, 6 part, 9 read, 3 light, 5 scan); 61 findings, 28 of them proposed errata.

### RFC 1142: OSI IS-IS Intra-domain Routing Protocol {#ra_rfc1142}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 1195: Use of OSI IS-IS for Routing in TCP/IP and Dual Environments {#ra_rfc1195}

Depth: deep. Errata: checked (checked: 2 (both held: 683 technical, 3741 editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0034 | 3.3 | "DFI       1 octet       value "xx"  /  AA        3 octets      value "xx xx xx"" | The values are given as placeholders that are neither valid decimal nor hexadecimal, so the derived NSAP is not specified. | ambiguity | 683 (Held) |
| RA-0035 | 5.3.5 | "7 IP Internal Reachability Information -- IP addresses within the routing domain reachable directly via one or more interfaces" | The level 2 description omits that entries may be reached indirectly through level 1 routing (section 5.3.2 says so); RFCs 3719 and 3787 clarify. | editorial | 3741 (Held) |

### RFC 3358: Optional Checksums in Intermediate System to Intermediate System (ISIS) {#ra_rfc3358}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 3719: Recommendations for Interoperable Networks using Intermediate System to Intermediate System (IS-IS) {#ra_rfc3719}

Depth: read (normative statements of 2 to 12). Errata: not checked. 

Nothing notable found at this depth.

### RFC 3787: Recommendations for Interoperable IP Networks using Intermediate System to Intermediate System (IS-IS) {#ra_rfc3787}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 3906: Calculating Interior Gateway Protocol (IGP) Routes Over Traffic Engineering Tunnels {#ra_rfc3906}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0152 | 4.1, 4.2 | "When using an absolute metric on a TE-tunnel, the cost of the IP routes in the routing table does not depend on the topology of the network. / If an absolute metric of 5 is configured on tunnel T1, then rtrA will install routes X, Y, and Z all with metrics 5, 15, and 25 respectively." | Section 4.1 says an absolute metric makes route costs independent of the topology and that the fixed metric "is not only used to compute the cost of IP routes advertised by the router that is the tail-end ... but also for all the routes that are downstream" (the POP example: all traffic to the POP uses the tunnel with metric 1). The 4.2 example instead adds the downstream distances (5, 15, 25), i.e. the absolute value replaces only the cost to the tail; the word "all" suggests an edit from "all with metric 5". Implementations differ (some install the absolute value for every prefix behind the tail). | contradiction | not checked; **proposed erratum below** |
| RA-0153 | 4.1 | "The relative metric is bounded by minimum and maximum allowed metric values while the positive metric disables the TE-tunnel in the SPF calculation." | The clause "while the positive metric disables the TE-tunnel" has no evident meaning: any positive relative metric would disable the tunnel, which contradicts the purpose of relative metrics (4.2 uses -5, and positive values are allowed "to make the route over the TE-tunnel ... more preferred" or less). Probably "a metric at the maximum value" or "a metric making the path worse than the native path" was meant; the text also does not say what happens when a negative relative metric would make a cost below the minimum (clamp or reject). | ambiguity | not checked |

Proposed erratum RA-0152 (RFC 3906, Section 4.1, 4.2; type: Technical):

```
Original Text
-------------
   If an absolute metric of 5 is configured on tunnel T1, then rtrA
   will install routes X, Y, and Z all with metrics 5, 15, and 25
   respectively.

Corrected Text
--------------
   (The working group should state which is intended.) Either "...
   install routes X, Y, and Z all with metric 5." or, in 4.1, "When
   using an absolute metric on a TE-tunnel, the cost to the tail-end
   router does not depend on the topology of the network;
   destinations downstream of the tail-end add their IGP distance
   from the tail-end."

Notes
-----
   Section 4.1 makes route costs over an absolute-metric tunnel
   independent of topology; the 4.2 example adds downstream IGP
   distances.
```

### RFC 5120: M-ISIS: Multi Topology (MT) Routing in Intermediate System to Intermediate Systems (IS-ISs) {#ra_rfc5120}

Depth: deep. Errata: not checked. 

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

### RFC 5130: A Policy Control Mechanism in IS-IS Using Administrative Tags {#ra_rfc5130}

Depth: read. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0154 | 4, 5, 6 | "there is no implied meaning to the ordering of the tags / An implementation supporting multiple tags SHOULD therefore assign any tag that is required to be interpreted by all systems as the first tag in any set of multiple tags." | Section 4 states that tag order carries no meaning ("Whether or not tag A precedes or succeeds tag B SHOULD not change the meaning"), but Sections 3.1, 5 and 6 give the first tag a special role (single-tag implementations interpret only the first one, so the tag that matters must be placed first). A receiver that supports multiple tags may legitimately treat the set as unordered while a single-tag one acts on the first only, so the same advertisement can be acted on differently. | contradiction | not checked |

### RFC 5286: Basic Specification for IP Fast Reroute: Loop-Free Alternates {#ra_rfc5286}

Depth: read (normative statements of 1 to 6). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5301: Dynamic Hostname Exchange Mechanism for IS-IS {#ra_rfc5301}

Depth: read. Errata: not checked. Obsoletes: RFC 2763.

Nothing notable found at this depth.

### RFC 5302: Domain-Wide Prefix Distribution with Two-Level IS-IS {#ra_rfc5302}

Depth: read (normative statements). Errata: not checked. Obsoletes: RFC 2966. Updates: RFC 1195.

Nothing notable found at this depth.

### RFC 5303: Three-Way Handshake for IS-IS Point-to-Point Adjacencies {#ra_rfc5303}

Depth: deep. Errata: not checked. Obsoletes: RFC 3373.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0155 | 3.2 | "If the new action is "Up", an adjacencyStateChange(Up) event is generated. / Up \| Initialize Accept Accept" | The action "Up" does not say that the three-way state is set to Up (only "Initialize" sets a state explicitly), and the "Initialize" action taken from three-way state Up when the neighbour reports Down generates no event: the ISO 10589 adjacency stays Up (and keeps being advertised) while the neighbour has just reported Down, i.e. after a neighbour restart the link remains in the LSPs until the neighbour reaches Initializing/Up again. Section 3.1 gives the Length range "1 to 17 octets" without saying which lengths are valid (1, 5, or 5 + ID Length + 4) or how an option with the Neighbor System ID but no Neighbor Extended Local Circuit ID is treated in the "if present" checks. | ambiguity | not checked |
| RA-0156 | 1, 2.2, 6 | "a method is defined to remove the limitation of 255 point-to-point interfaces imposed by IS-IS" | Section 1 says 255, Section 2.2 "an implicit limit of 256 interfaces" (eight-bit Circuit ID); Section 6 "the ISP 10589 reference" for ISO 10589. | editorial | not checked |

### RFC 5304: IS-IS Cryptographic Authentication {#ra_rfc5304}

Depth: deep. Errata: not checked. Obsoletes: RFC 3567. Updates: RFC 1195.

Nothing notable found at this depth.

### RFC 5305: IS-IS Extensions for Traffic Engineering {#ra_rfc5305}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 3784.

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

### RFC 5307: IS-IS Extensions in Support of Generalized Multi-Protocol Label Switching (GMPLS) {#ra_rfc5307}

Depth: read (normative statements). Errata: not checked. Obsoletes: RFC 4205. Updates: RFC 5305.

Nothing notable found at this depth.

### RFC 5308: Routing IPv6 with IS-IS {#ra_rfc5308}

Depth: part. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0040 | 2 | "than MAX_V6_PATH_METRIC (0xFE000000), this prefix MUST not be considered during the normal Shortest Path First (SPF) computation." | "MUST not" written in mixed case; the intent is MUST NOT. | editorial | not checked |

### RFC 5310: IS-IS Generic Cryptographic Authentication {#ra_rfc5310}

Depth: deep. Errata: no errata page found by search (not confirmed). 

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

### RFC 5311: Simplified Extension of Link State PDU (LSP) Space for IS-IS {#ra_rfc5311}

Depth: read (normative statements). Errata: not checked. Obsoletes: RFC 3786.

Nothing notable found at this depth.

### RFC 6119: IPv6 Traffic Engineering in IS-IS {#ra_rfc6119}

Depth: deep (4 in full). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0157 | 4.3 | "Implementations MUST NOT inject a /128 prefix for the interface address into their routing or forwarding table" | Section 4.3 defines the IPv6 Neighbor Address sub-TLV, but the sentence (copied from 4.2) speaks of "the interface address"; the neighbour address is meant. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0157 (RFC 6119, Section 4.3; type: Editorial):

```
Original Text
-------------
   Implementations MUST NOT inject a /128 prefix for the interface
   address into their routing or forwarding table

Corrected Text
--------------
   Implementations MUST NOT inject a /128 prefix for the neighbor
   address into their routing or forwarding table

Notes
-----
   Copy of the Section 4.2 sentence; Section 4.3 concerns the IPv6
   Neighbor Address sub-TLV (type 13).
```

### RFC 6213: IS-IS BFD-Enabled TLV {#ra_rfc6213}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0158 | 3.1, 3.2, 3.3 | "An "ISIS_BFD_REQUIRED" variable is set to the logical "AND" of all "ISIS_TOPO_BFD_REQUIRED" variables. ... An "ISIS_NEIGHBOR_USEABLE" variable is set to the logical "OR" of all "ISIS_TOPO_USEABLE" variables." | With more than one topology (for example MT 0 for IPv4 and MT 2 for IPv6), the adjacency rules of 3.2 apply only when every topology requires BFD (AND), and then the adjacency goes Down only when no topology is usable (OR); a BFD failure in one topology only withdraws that topology's IS neighbour (3.3), which 3.3 states without the ISIS_BFD_REQUIRED condition. The text does not say explicitly that an IPv4 BFD failure keeps a multi-topology adjacency Up, nor whether 3.3 applies when ISIS_BFD_REQUIRED is FALSE, and implementations that take the whole adjacency down on any failure are common. | ambiguity | not checked; **proposed erratum below** |

Proposed erratum RA-0158 (RFC 6213, Section 3.1, 3.2, 3.3; type: Technical):

```
Original Text
-------------
   An "ISIS_BFD_REQUIRED" variable is set to the logical "AND" of
   all "ISIS_TOPO_BFD_REQUIRED" variables.

Corrected Text
--------------
   (Clarification; no single correction.) Add after Section 3.3:
   "When ISIS_BFD_REQUIRED is FALSE because some topology does not
   require BFD, a BFD failure in a topology that does require it
   affects only the advertisement and use of that topology-specific
   neighbor as described in Section 3.3; the adjacency itself is
   maintained."

Notes
-----
   The AND
   OR combination keeps the adjacency Up while any topology is
   usable; many implementations instead take the adjacency down. A
   sentence stating the intended result, and that Section 3.3
   applies regardless of ISIS_BFD_REQUIRED, would remove the
   ambiguity.
```

### RFC 6232: Purge Originator Identification TLV for IS-IS {#ra_rfc6232}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 5301, RFC 5304, RFC 5310.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0159 | 5, 3 | "all implementations in a domain implementing authentication MUST be upgraded to receive the POI TLV before any IS is allowed to generate a purge with the POI TLV." | RFC 6233 Section 3 (published together, not marked as updating this document) says that an implementation that implements authentication generates a purge by removing non-purge TLVs and "The POI TLV MUST be added", while Section 3 here makes it a SHOULD. An upgraded authenticating IS is thus required to add the POI TLV (RFC 6233) and forbidden to send it until every IS in the domain is upgraded (this section); neither document says which rule wins during migration, and there is no configuration knob in either. | contradiction | not checked |

### RFC 6233: IS-IS Registry Extension for Purges {#ra_rfc6233}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 3563, RFC 5304, RFC 5310.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0160 | 3 | "If an implementation that implements authentication accepts a purge that does not include the POI TLV and it chooses to insert the POI TLV, it MUST also recompute authentication." | Recomputing requires a send key for that level; if the IS has none, or the larger purge no longer fits the LSP buffer size, the text gives no fallback (flood unchanged, or not insert). "Purges that are accepted MUST be propagated without removal of TLVs" also does not say whether the received Authentication TLV is removed or replaced when it is recomputed. | ambiguity | not checked |

### RFC 7308: Extended Administrative Groups in MPLS Traffic Engineering (MPLS-TE) {#ra_rfc7308}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0161 | 2.2 | "If an EAG's length is more than 4 bytes, numbering for these additional bytes picks up where the previous byte left off. For example, the least significant bit in the fifth byte of an 8-byte EAG is referred to as bit 32." | Bits 0-31 of the EAG "have the same meaning ... as an AG", whose bit 0 is the least significant bit of a 32-bit value sent in network order, i.e. the last of the first four bytes. Numbering the EAG word by word in the same way puts bit 32 at the least significant bit of the eighth byte; the example puts it in the fifth byte, which is a byte-wise continuation that is big-endian in the first word and little-endian afterwards. The two readings give different link colours for every group above 31, and implementations (and later users of the encoding such as the flexible-algorithm Admin Group sub-TLVs of RFC 9350) are known to use the word-wise reading. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0161 (RFC 7308, Section 2.2; type: Technical):

```
Original Text
-------------
   For example, the least significant bit in the fifth byte of an
   8-byte EAG is referred to as bit 32.

Corrected Text
--------------
   The EAG is a sequence of 32-bit words in network byte order; bit
   N is bit (N mod 32) of word (N div 32), bit 0 of a word being its
   least significant bit. For example, the least significant bit in
   the eighth byte of an 8-byte EAG is referred to as bit 32.

Notes
-----
   Bits 0-31 must equal the AG, whose bit 0 is the least significant
   bit of the fourth byte. Continuing word by word gives bit 32 in
   the eighth byte; the example's fifth byte implies a different
   byte order for the second and later words. The working group
   should confirm the intended numbering.
```

### RFC 7490: Remote Loop-Free Alternate (LFA) Fast Reroute (FRR) {#ra_rfc7490}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0162 | 5.2.1.2, 5.3 | "In cost terms, a router (P) is in extended P-space if the shortest path cost N->P is strictly less than the shortest path cost N->S->E->P. / if ( D_opt(n, y) < D_opt(n,self) + D_opt(self, y))" | The prose condition is link-specific (N's path to P must avoid S->E), while the pseudocode applies RFC 5286 Inequality 1 (N's path to P must avoid S altogether), which never refers to the failed link. The pseudocode result is a strict subset of the prose set: a node P reached from N through S but not over S-E is in extended P-space by the text and excluded by the code. Implementations following one or the other compute different PQ sets. | contradiction | none found; **proposed erratum below** |
| RA-0163 | 5.2.2, 5.3 | "it is RECOMMENDED that the member of the set of routers {PQ} with the lowest cost S->P be the default choice for P." | For a PQ node found only through extended P-space, S's shortest path to P crosses S-E by definition, so "cost S->P" is either that pre-failure cost (which the repair does not follow) or the cost of the repair path S->N->P; the text does not say which, and the tie-breaker "lowest node identifier" does not say which identifier (system ID, router ID, TE router ID). Apply_Downstream_Constraint() uses "dest", which is not defined in the per-link main function. | ambiguity | none found |

Proposed erratum RA-0162 (RFC 7490, Section 5.2.1.2, 5.3; type: Technical):

```
Original Text
-------------
   if ( D_opt(n, y) < D_opt(n,self) + D_opt(self, y))

Corrected Text
--------------
   (Clarification requested; to match the text:) if ( D_opt(n, y) <
   D_opt(n,self) + D_opt(self, fail_intf.remote_node) +
   D_opt(fail_intf.remote_node, y) ), noting that the RFC 5286
   Inequality 1 form gives a smaller, node-protecting set.

Notes
-----
   The two conditions coincide only when every shortest path from S
   to P crosses S-E.
```

### RFC 7775: IS-IS Route Preference for Extended IP and IPv6 Reachability {#ra_rfc7775}

Depth: deep. Errata: not checked. Updates: RFC 5308.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0164 | 3.3, 3.4 | "Note that all types of routes listed for a given preference are treated equally.  1.  L1 intra-area routes; L1 external routes" | The RFC defines three preference classes and puts internal and external routes of the same level in one class ("treated equally"), i.e. within a class the metric decides. It does not say how ties in metric between an internal and an external route of the same class are broken, nor whether "treated equally" permits ECMP across them. | ambiguity | not checked; **proposed erratum below** |
| RA-0165 | 3.1, 3.2, 3.3, 3.4 | "L2-L2 inter-area routes / L1-L2 external routes" | The preference lists write "L2-L2" and "L1-L2" where the route-type definitions use "L2->L2" and "L1->L2". The IPv4 list (3.1) has no "L1->L2 external" or "L2->L1 external" types, which the IPv6 list (3.2) has, and the IPv4 L1->L2 and L2->L1 inter-area entries do not say how the X-Flag is set when the leaked prefix was external, although the Prefix Attribute Flags sub-TLV [RFC7794] can carry it. | editorial | not checked |

Proposed erratum RA-0164 (RFC 7775, Section 3.3, 3.4; type: Technical):

```
Original Text
-------------
   Note that all types of routes listed for a given preference are
   treated equally.

Corrected Text
--------------
   Note that all types of routes listed for a given preference are
   treated equally; among them the route with the lowest metric is
   preferred, and routes of equal metric are equal-cost
   alternatives.

Notes
-----
   Implementations differ on whether internal routes are preferred
   over external routes of the same level when extended reachability
   TLVs are used.
```

### RFC 7794: IS-IS Prefix Attributes for Extended IPv4 and IPv6 Reachability {#ra_rfc7794}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0166 | 2.2 | "When included, the value MUST be identical to the value advertised in the Traffic Engineering router ID (TLV 134) defined in [RFC5305].  If present the sub-TLV MUST be included when the prefix advertisement is leaked to another level." | After leaking, the sub-TLV sits in the leaking router's LSP, which carries the leaking router's own TLV 134; the rule must mean the TLV 134 of the originating router (as the preceding note says), but read literally it requires the value to equal the TLV 134 of the LSP that carries it, which a leaked copy cannot satisfy. A receiver that validates the sub-TLV against the carrying LSP's TLV 134 would reject every leaked Source Router ID. | ambiguity | not checked; **proposed erratum below** |

Proposed erratum RA-0166 (RFC 7794, Section 2.2; type: Technical):

```
Original Text
-------------
   When included, the value MUST be identical to the value
   advertised in the Traffic Engineering router ID (TLV 134) defined
   in [RFC5305].

Corrected Text
--------------
   When included, the value MUST be identical to the value
   advertised by the originating router in its Traffic Engineering
   router ID (TLV 134) defined in [RFC5305].

Notes
-----
   The same wording is used for the IPv6 Source Router ID and TLV
   140.
```

### RFC 7811: An Algorithm for Computing IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) {#ra_rfc7811}

Depth: part. Errata: not checked. 

Nothing notable found at this depth.

### RFC 7812: An Architecture for IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) {#ra_rfc7812}

Depth: part. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0167 | 8.3, 8.2 | "Among the routers in the MRT Island with the lowest numerical value advertised for GADAG Root Selection Priority, an implementation MUST pick the router with the highest Router ID to be the GADAG root." | "Router ID" is not defined for IS-IS, where several candidates exist (system ID, TE Router ID TLV 134/140, the RFC 7811 mrt_node_id which is the 7-octet system ID plus pseudonode). All routers must pick the same root (RFC 7811 5.3 MUST), so the identifier must be fixed per IGP, as RFC 7811 Figure 15 does for interface ordering. RFC 7811 5.9.1 also breaks proxy-node ties "based upon the lowest Router ID" with the same undefined term. Section 8.2 has "either IPv4 and IPv6". | ambiguity | not checked |

### RFC 7981: IS-IS Extensions for Advertising Router Information {#ra_rfc7981}

Depth: deep. Errata: not checked. Obsoletes: RFC 4971.

Nothing notable found at this depth.

### RFC 8102: Remote-LFA Node Protection and Manageability {#ra_rfc8102}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0168 | 2.2.1, 2.2.6.1 | "the set of routers that are reachable from one or more direct neighbors of S, except primary node E, without traversing the S-E link on any of the shortest paths / D_opt(Ni,Y) < D_opt(Ni,S) + D_opt(S,Y)" | As in RFC 7490 (5.2.1.2 versus 5.3), the formal definition excludes only paths over the link S-E, while the "cost-based definition" excludes every path through S, a strictly smaller set; the section says the cost form defines the same set ("refer to Section 2.2.6.1"). Section 2.3.1 also says the needed metrics come from "the forward SPFs rooted at each of direct neighbor S", and Figure 6 mixes "D_opt" and "Distance_opt". | contradiction | not checked |

### RFC 8202: IS-IS Multi-Instance {#ra_rfc8202}

Depth: deep. Errata: not checked. Obsoletes: RFC 6822.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0169 | 3.6.1, 3.6.1.1, 3.6.2 | "MI-RTRs MUST discard IS-IS PDUs received if ... The destination multicast address is AllL1IS, AllL2IS, or AllIS and the PDU contains an IID-TLV. / all IIHs sent on a point-to-point circuit by an MI-RTR MUST include an IID-TLV.  This includes IIHs associated with IID #0." | In point-to-point operation over a LAN (RFC 5309), Section 3.6.1.1 sends standard-instance (IID #0) point-to-point IIHs to AllL1IS / AllL2IS / AllIS. If Section 3.6.2 ("all IIHs sent on a point-to-point circuit") applies to such circuits, those IIHs carry an IID-TLV with IID 0, and the receiving MI-RTR must discard them under the first rule of Section 3.6.1, so the IID #0 adjacency never forms. The text does not say whether a point-to-point-over-LAN circuit is a "point-to-point circuit" for Section 3.6.2, or whether the Section 3.6.1 discard rule exempts an IID-TLV with IID 0. Section 3.6.1.1 also says MI addresses "MUST" be used for non-zero-IID point-to-point IIHs and then "either address is permitted", without saying which two addresses are meant, and misspells "AllL2MI-ISs". | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0169 (RFC 8202, Section 3.6.1, 3.6.1.1, 3.6.2; type: Technical):

```
Original Text
-------------
   When sending point-to-point IIHs for a non-zero IID, either
   address is permitted.

Corrected Text
--------------
   When sending point-to-point IIHs for a non-zero IID, either
   AllL1MI-ISs or AllL2MI-ISs is permitted. (And in Section 3.6.1:)
   ... and the PDU contains an IID-TLV with a non-zero IID.

Notes
-----
   Sections 3.6.1, 3.6.1.1 and 3.6.2 together make IID #0
   point-to-point IIHs sent to the standard multicast addresses both
   mandatory to carry an IID-TLV and mandatory to discard when they
   do.
```

### RFC 8333: Micro-loop Prevention by Introducing a Local Convergence Delay {#ra_rfc8333}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0170 | 5.4 | "If the condition of a single local link-down event has been met, then an update of the RIB and the FIB MUST be delayed for ULOOP_DELAY_DOWN_TIMER ms. / Hence, it SHOULD only be done for a non-urgent convergence, such as administrative deactivation (maintenance) or when the traffic is protected by FRR." | Step 5 makes the delay mandatory for every single local link-down, while the next paragraph says it should only be applied when the failure is non-urgent or FRR-protected. For an unprotected destination behind the failed link, the MUST keeps the old (failed) forwarding entry for ULOOP_DELAY_DOWN_TIMER (typically seconds), which black-holes traffic. The condition (protection available per destination) belongs in the MUST. In Section 6.2 "its forwarding entry to F is updated" should read "to K" (the example's destination). | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0170 (RFC 8333, Section 5.4; type: Technical):

```
Original Text
-------------
   If the condition of a single local link-down event has been met,
   then an update of the RIB and the FIB MUST be delayed for
   ULOOP_DELAY_DOWN_TIMER ms.

Corrected Text
--------------
   If the condition of a single local link-down event has been met
   and the affected destinations are protected (for example by FRR)
   or the event is non-urgent, then an update of the RIB and the FIB
   MUST be delayed for ULOOP_DELAY_DOWN_TIMER ms.

Notes
-----
   Without the restriction, unprotected traffic is dropped for the
   whole delay.
```

### RFC 8402: Segment Routing Architecture {#ra_rfc8402}

Depth: part. Errata: checked (checked: 7546 (rejected, technical, Section 1 SL pointer); 7671 (verified, editorial; listed in the WG mail archive, not shown on the errata page fetched)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0171 | 3.1, 3.1.2 | "Multiple SIDs MAY be allocated to the same prefix so long as the tuple <prefix, topology, algorithm> is unique." | The sentence allows "multiple SIDs" for a prefix only when each <prefix, topology, algorithm> tuple is unique, i.e. at most one SID per tuple, but it reads as permitting several SIDs for one tuple. It does not say what a receiver does when two different SIDs arrive for the same tuple (from the same or different originators), which the protocol documents (RFC 8667, RFC 8660 conflict resolution) then have to settle. Section 3.1.2's "MUST NOT allocate the same Prefix-SID to different prefixes" also conflicts on its face with Section 3.3, where an anycast prefix is advertised by several routers with one SID (same prefix, so consistent, but "different prefixes" with the same SID across algorithms is not addressed). | ambiguity | none found |

### RFC 8405: Shortest Path First (SPF) Back-Off Delay Algorithm for Link-State IGPs {#ra_rfc8405}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0172 | 5.2, 5.3, 5.4 | "QUIET: This is the initial state, when no IGP events have occurred for at least HOLDDOWN_INTERVAL since the last routing table computation. / HOLDDOWN_TIMER: This is the FSM timer that is (re)started when an IGP event is received" | The state definition measures HOLDDOWN_INTERVAL from the last routing table computation, while the timer and transitions 2, 4, 5 and 6 measure it from the last IGP event. With LONG_SPF_DELAY close to HOLDDOWN_INTERVAL the two readings return to QUIET at different times, which matters for the stated goal of identical SPF delays on all routers. The FSM also allows QUIET with SPF_TIMER still running (when SPF delay exceeds HOLDDOWN_INTERVAL, both configurable up to 6000 ms); transition 1 then keeps the long delay ("if SPF_TIMER is not already running"), which is not discussed. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0172 (RFC 8405, Section 5.2, 5.3, 5.4; type: Technical):

```
Original Text
-------------
   QUIET: This is the initial state, when no IGP events have
   occurred for at least HOLDDOWN_INTERVAL since the last routing
   table computation.

Corrected Text
--------------
   QUIET: This is the initial state, when no IGP events have
   occurred for at least HOLDDOWN_INTERVAL since the last IGP event
   was received.

Notes
-----
   The state machine of Section 5.4 restarts HOLDDOWN_TIMER on every
   IGP event; the prose definition of QUIET in Section 5.2 uses the
   last routing table computation as reference.
```

### RFC 8491: Signaling Maximum SID Depth (MSD) Using IS-IS {#ra_rfc8491}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0173 | 2, 3 | "If there exist multiple Node MSD advertisements for the same MSD-Type originated by the same router, the procedures defined in [RFC7981] apply." | RFC 7981 defines no selection procedure; it says the choice between conflicting copies of a capability "is undefined", so the reference resolves to "undefined", as Section 3 says explicitly for Link MSD. Neither section says how an odd or zero Length, or a pair with MSD-Type 0 / 255 (reserved), is handled. | ambiguity | not checked |

### RFC 8570: IS-IS Traffic Engineering (TE) Metric Extensions {#ra_rfc8570}

Depth: deep. Errata: checked (checked via the obsoleted RFC 7810: 5293 (held, editorial), fixed in RFC 8570 section 11). Obsoletes: RFC 7810.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0044 | 4.5 to 4.7, 11 | "The length specified was 4, which did not include the RESERVED field shown in the figures." | RFC 7810 drew a RESERVED octet that its Length (4) did not count; implementations split on length 4 against 5. RFC 8570 removes the field. A receiver may still meet length-5 sub-TLVs 37 to 39 from old RFC 7810 speakers. | error | RFC 7810: 5293 (Held) |
| RA-0174 | 4.6, Appendix A | "For a bundled link, available bandwidth is defined to be the sum of the component link available bandwidths. / it used "sum of the component link available bandwidths" when it should have used "sum of the component link residual bandwidths".  This has been corrected and clarified." | Appendix A states that the definition criticised in erratum 5486 against RFC 7810 has been corrected, but Section 4.6 still carries the RFC 7810 wording verbatim. Either the correction was lost during editing or the appendix is wrong; an implementer cannot tell which definition is intended for bundles (and "sum of the component link residual bandwidths" would equal the residual bandwidth of Section 4.5, which suggests the appendix wording is not right either). | contradiction | none found; **proposed erratum below** |
| RA-0175 | 4.4 | "The basic unit is 0.000003%, where (2^24 - 2) is 50.331642%.  This value is the highest packet-loss percentage that can be expressed" | The 24-bit field can hold 2^24 - 1, but the text names 2^24 - 2 as the highest expressible value without saying whether 2^24 - 1 is reserved, invalid or simply also "at least" 50.331642%. Implementations clamping to 2^24 - 1 and to 2^24 - 2 coexist; a receiver does not know how to treat 2^24 - 1. | ambiguity | none found |
| RA-0176 | 3 | "However, as for the TE case, Interface Address and Neighbor Address sub-TLVs (IPv4 or IPv6) MUST be present." | Unnumbered links have no interface or neighbor address and are identified by Link Local/Remote Identifiers (RFC 5307 sub-TLV 4), and links to a pseudonode have no single neighbor address. Read literally, the MUST forbids TE Metric Extensions on such links. Section 4.3 also defines delay variation as "the delay from the local neighbor to the remote neighbor (i.e., the forward-path latency)", a copy of the delay sentence. | ambiguity | none found |

Proposed erratum RA-0174 (RFC 8570, Section 4.6, Appendix A; type: Technical):

```
Original Text
-------------
   For a bundled link, available bandwidth is defined to be the sum
   of the component link available bandwidths.

Corrected Text
--------------
   (Clarification requested; one possibility:) For a bundled link,
   available bandwidth is defined to be the residual bandwidth of
   the bundle (Section 4.5) minus the measured bandwidth used for
   the actual forwarding of non-RSVP-TE label switched path packets
   over all component links.

Notes
-----
   The text of Section 4.6 matches RFC 7810 Section 4.6, which
   erratum 5486 reported as circular. The appendix's replacement
   wording would make available bandwidth equal to residual
   bandwidth for bundles.
```

### RFC 8660: Segment Routing with the MPLS Data Plane {#ra_rfc8660}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0177 | 2.5.1, 2.6 | "the ingress node MUST resolve this collision by using this same "Incoming Label Collision resolution procedure" and by using the data of the receiving node. / All FEC types, except for the SR Policy, are ordered using the default administrative distance defined by the implementation." | Section 2.6 requires an ingress to reproduce the receiving node's collision resolution, but step 1 of the tiebreak (Section 2.5.1) depends on administrative distances that, for dynamically assigned SIDs, are "defined by the implementation" and are not advertised, and the routing-instance identifier used in the FEC encoding may be derived from local configuration. An ingress therefore cannot in general compute the receiving node's winner from IGP data, so the MUST of 2.6 is not implementable when the two routers run different implementations (Section 2.5.1 only requires the same tiebreaking rules, not the same administrative distances). | ambiguity | not checked |

### RFC 8661: Segment Routing MPLS Interworking with LDP {#ra_rfc8661}

Depth: part. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0178 | 2.1 | "Incoming label: 203 / -  Outgoing label: 203 / -  Outgoing next hop: B / Note: This entry is programmed by SR for 192.0.2.203/32." | In the Section 2 example only PE2, A, B, C and PE4 are SR capable, with Node SIDs 202, 101, 102, 103 and 204; PE3 (192.0.2.203) is "not SR capable" and no mapping server is configured, so there is no node segment 203 and SR cannot program an entry for 192.0.2.203/32. The EVEN service whose SR path is described in Section 2 uses 204 towards PE4 (192.0.2.204). The example contradicts the scenario it illustrates. | error | none found; **proposed erratum below** |
| RA-0179 | 3.2.3, 3.2.1 | "For any prefix for which it did not receive a Prefix-SID Advertisement, the MCC applies the SRMS mapping advertisements with the highest preference." | Tie-breaking between SRMS advertisements of equal preference with different SIDs for the same prefix is left to RFC 8660's collision rules only when they cause an incoming label collision; two equal-preference mappings giving different SIDs for one prefix (a prefix conflict, not a label collision) are not addressed here. The last paragraph also asks for an operator choice between SRMS and LDP for IP2MPLS without saying what the default is. | ambiguity | none found |

Proposed erratum RA-0178 (RFC 8661, Section 2.1; type: Technical):

```
Original Text
-------------
   Incoming label: 203
   Outgoing label: 203
   Outgoing next hop: B
   Note: This entry is programmed by SR for 192.0.2.203/32.

Corrected Text
--------------
   Incoming label: 204
   Outgoing label: 204
   Outgoing next hop: B
   Note: This entry is programmed by SR for 192.0.2.204/32.

Notes
-----
   Per the scenario of Section 2, PE3 is not SR capable and the
   SR-tunnelled service goes to PE4 with Node SID 204.
```

### RFC 8667: IS-IS Extensions for Segment Routing {#ra_rfc8667}

Depth: deep. Errata: checked (checked: 1 (7722 verified, editorial heading)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0045 | 2.1.1.1 | "2.1.1.1.  V-Flag and L-Flag" | The heading should also name the SID/Index/Label field, whose size depends on the flags (4-octet index or 3-octet label). Other flag combinations "are invalid" and the advertisement MUST be ignored. | editorial | 7722 (Verified) |

### RFC 8668: Advertising Layer 2 Bundle Member Link Attributes in IS-IS {#ra_rfc8668}

Depth: deep. Errata: checked (checked: 1 (6957 verified, editorial, Section 5 "sub-TLV 25" for "TLV 25")). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0180 | Appendix A, 3 | "\|  Type(25)     \| Length(64)    \|  ...  \|Len:9+6+10 = 25\| # Desc: 2     \| / \|  Type(25)     \| Length(46)    \|" | The descriptor lengths in the example (25, 25 and 32) exclude the descriptor's own length octet ("9 + 6 + 10": member count and identifiers, Maximum Link Bandwidth sub-TLV, Adj-SID sub-TLV), as Section 3 implies. With that reading the TLV for adjacency 1 is 8 (parent descriptor and flags) + 6 (IPv4 Interface Address sub-TLV) + 2 x (1 + 25) = 66 octets, and the TLV for adjacency 2 is 8 + 6 + (1 + 32) = 47 octets, not 64 and 46. The TLV lengths only add up if the descriptor length octet is not counted anywhere, so the example contradicts itself and can mislead an implementer about whether the descriptor Length includes itself. | error | none found; **proposed erratum below** |
| RA-0181 | 3.2, 5 | "y     sub-TLV may appear in TLV 25 but MUST NOT be shared by multiple L2 Bundle Members" | Sub-TLVs marked "y" (33 to 39, the RFC 8570 per-link measurements) may appear only once per descriptor (Section 3.2: duplicates are all ignored) yet must not be shared, so they can only be used in a descriptor listing exactly one member. This consequence is not stated, nor what a receiver does with a "y" sub-TLV in a descriptor that lists several members. The descriptor is also called both "L2 Bundle Attribute Descriptor" (Section 3) and "L2 Bundle Member Attribute Descriptor" (Sections 3.2, 4.1, 4.2). | ambiguity | none found |

Proposed erratum RA-0180 (RFC 8668, Section Appendix A, 3; type: Technical):

```
Original Text
-------------
   |  Type(25)     | Length(64)    |  (TLV for Adjacency #1)  and  |
    Type(25)     | Length(46)    |  (TLV for Adjacency #2)

Corrected Text
--------------
   |  Type(25)     | Length(66)    |  (TLV for Adjacency #1)  and  |
    Type(25)     | Length(47)    |  (TLV for Adjacency #2)

Notes
-----
   Parent L3 Neighbor Descriptor (7 + 1 octets) + IPv4 Interface
   Address sub-TLV (2 + 4) + for each L2 Bundle Attribute Descriptor
   its length octet (1) plus the value given in the example (25, 25;
   32). This gives 66 and 47. The descriptor length values
   themselves (25, 32) are consistent with Section 3.
```

### RFC 8706: Restart Signaling for IS-IS {#ra_rfc8706}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 5306.

Nothing notable found at this depth.

### RFC 8754: IPv6 Segment Routing Header (SRH) {#ra_rfc8754}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8986: Segment Routing over IPv6 (SRv6) Network Programming {#ra_rfc8986}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9256: Segment Routing Policy Architecture {#ra_rfc9256}

Depth: light. Errata: not checked. Updates: RFC 8402.

Nothing notable found at this depth.

### RFC 9294: Application-Specific Link Attributes Advertisement Using the Border Gateway Protocol - Link State (BGP-LS) {#ra_rfc9294}

Depth: deep (section 3 and 4 rules (1), (2)(A)-(G) in full). Errata: not checked. 

Nothing notable found at this depth.

### RFC 9346: IS-IS Extensions in Support of Inter-Autonomous System (AS) MPLS and GMPLS Traffic Engineering {#ra_rfc9346}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 5316.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0182 | 3.2 vs 3.4.4 | "If the originating node does not support IPv4, then the reserved value 0.0.0.0 MUST be used in the Router ID field, and the IPv6 Router ID sub-TLV MUST be present in the Inter-AS Reachability Information TLV." | No "IPv6 Router ID sub-TLV" is defined for TLV 141; Section 3.4.4 (and the IANA table) defines the IPv6 Local ASBR Identifier sub-TLV for exactly this case and says a TLV with Router ID 0.0.0.0 without it "MUST be ignored". | editorial | none found; **proposed erratum below** |
| RA-0183 | 3.4.2, 3.4.3 | "An IPv4 Remote ASBR Identifier sub-TLV and IPv6 Remote ASBR Identifier sub-TLV MAY both be present in an extended IS reachability TLV." | These sub-TLVs are defined for the Inter-AS Reachability Information TLV (141); the sentence names the Extended IS Reachability TLV (22), where they are not allowed by the IANA table of Section 6.2. | editorial | none found; **proposed erratum below** |

Proposed erratum RA-0182 (RFC 9346, Section 3.2 vs 3.4.4; type: Editorial):

```
Original Text
-------------
   and the IPv6 Router ID sub-TLV MUST be present in the Inter-AS
   Reachability Information TLV.

Corrected Text
--------------
   and the IPv6 Local ASBR Identifier sub-TLV (Section 3.4.4) MUST
   be present in the Inter-AS Reachability Information TLV.

Notes
-----
   Section 3.4.4 defines the sub-TLV meant here.
```

Proposed erratum RA-0183 (RFC 9346, Section 3.4.2, 3.4.3; type: Editorial):

```
Original Text
-------------
   MAY both be present in an extended IS reachability TLV.

Corrected Text
--------------
   MAY both be present in an Inter-AS Reachability Information TLV.

Notes
-----
   Appears in both 3.4.2 and 3.4.3.
```

### RFC 9350: IGP Flexible Algorithm {#ra_rfc9350}

Depth: deep (IS-IS sections in full; OSPF-only sections 5.2, 7, 9, 10 scanned). Errata: checked (checked: 2 (7406 Verified editorial 5.1 "Label Switched Path (LSP)" -> "Link State PDU (LSP)"; 7376 Held editorial 6 expand "IS"); neither touches the findings below). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0184 | 13.1 vs 8 | "During the route computation, it is possible for the Flex-Algorithm-specific metric to exceed the maximum value that can be stored in an unsigned 32-bit variable. In such scenarios, the value MUST be considered to be of value 0xFFFFFFFF during the computation and advertised as such." | A metric that saturates at 0xFFFFFFFF and is advertised as such in a FAPM is, by Section 8 ("Flex-Algorithm prefix metric larger than MAX_PATH_METRIC ... MUST NOT be considered"), unusable in the next area, while the same overflow in the default algorithm is clamped to MAX_PATH_METRIC (0xFE000000) and stays usable (RFC 5305 3). A prefix reachable at a large cost in algorithm 0 thus becomes unreachable for the flex-algorithm across an ABR. Whether saturating at 0xFFFFFFFF (rather than at MAX_PATH_METRIC) is intended is not stated. | contradiction | none found; **proposed erratum below** |
| RA-0185 | 5.3, 6 | "If it appears more than once, the IS-IS FAD sub-TLV MUST be ignored by the receiver." | Sections 6.1 to 6.5 give receive rules for duplicates but none for a sub-sub-TLV whose Length is not a multiple of 4 (a sender MUST only). Whether such a FAD is invalid (stop participating, 5.3) or only the sub-sub-TLV is ignored is left open; ignoring only an exclude rule changes the computed paths. | ambiguity | none found |

Proposed erratum RA-0184 (RFC 9350, Section 13.1 vs 8; type: Technical):

```
Original Text
-------------
   In such scenarios, the value MUST be considered to be of value
   0xFFFFFFFF during the computation and advertised as such.

Corrected Text
--------------
   (Clarification needed.) In such scenarios, the value MUST be
   considered to be of value 0xFFFFFFFF during the computation and
   advertised as such; note that, per Section 8, a prefix advertised
   with such a FAPM is not considered in the Flexible Algorithm
   computation of the receiving area.

Notes
-----
   The interaction of the saturation value and the MAX_PATH_METRIC
   receive rule should be stated.
```

### RFC 9352: IS-IS Extensions to Support Segment Routing over the IPv6 Data Plane {#ra_rfc9352}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 7370.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0186 | 11.3 | "\| 0     \| Reserved    \| RFC 9532  \|" | The registry "IS-IS Sub-Sub-TLVs for the SRv6 Capabilities Sub-TLV" cites RFC 9532 as the reference for value 0; this document (RFC 9352) is meant. RFC 9532 is unrelated. | editorial | none found; **proposed erratum below** |
| RA-0187 | 4.2-4.4 | "The Maximum H.Encaps MSD Type signals the maximum number of SIDs that can be added to the segment list of an SRH as part of the "H.Encaps" behavior" | The SRv6 MSD types count "SIDs", which predates compressed SIDs (RFC 9800): with NEXT-CSID or REPLACE-CSID one 128-bit segment-list entry carries several SIDs, and the limit that matters to hardware is the number of 128-bit entries. The text does not say whether a container counts as one SID or as the number of SIDs it carries; the LSR working group discussed (2025) but did not file an erratum. | ambiguity | none found (LSR discussion of an erratum for compressed SIDs, no report filed per the thread) |
| RA-0188 | 7.2 | "For a given MTID/Locator, the algorithm MUST be the same in all TLVs. If this restriction is not met, all TLVs for that MTID/Locator MUST be ignored." | The scope of "all TLVs" is not stated: all TLVs of the advertising node, or all TLVs for that locator from any node (an anycast locator advertised by several nodes, Section 6, could then be withdrawn network-wide by one misconfigured node). The rule also does not say whether the Prefix Reachability TLV for the same prefix (Section 5) is affected. | ambiguity | none found |
| RA-0189 | 6, 7.1 | "When included in the Locator TLV, the state of the X-flag in the Prefix Attributes Flags sub-TLV MUST match the setting of the embedded "X-bit" in any advertisement for the same prefix in TLVs 236 [RFC5308] and 237 [RFC5120]." | The SRv6 Locator TLV has no embedded X-bit, so a locator that is not also advertised in TLV 236/237 has only the sub-TLV X-flag; when the Prefix Attribute Flags sub-TLV (only a SHOULD in 7.1) is absent, whether the locator is external is unknown, while the D-flag is carried in the entry itself. The text does not say how a receiver treats a locator without the sub-TLV for external/internal preference. | ambiguity | none found |

Proposed erratum RA-0186 (RFC 9352, Section 11.3; type: Editorial):

```
Original Text
-------------
   | 0     | Reserved    | RFC 9532  |

Corrected Text
--------------
   | 0     | Reserved    | RFC 9352  |

Notes
-----
   Transposed digits.
```

### RFC 9377: IS-IS Flood Reflection {#ra_rfc9377}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0190 | 4.5 vs 4.6 | "A router acting as a flood reflector MUST NOT form any standard L2 adjacencies except with flood reflector clients. (4.5) / A flood reflector MUST NOT form any standard L2 adjacencies. (4.6)" | Section 4.5 allows a flood reflector to form standard L2 adjacencies with its clients (and says a reflector with "a direct L2 adjacency with the according remote side ... SHOULD use it instead of instantiating a tunnel"), while Section 4.6 forbids all standard L2 adjacencies, and Section 7 relies on that ("a flood reflector MUST NOT form an adjacency with a non-FR router"). An implementation following 4.6 refuses the direct adjacency that 4.5 prefers to a tunnel. | contradiction | none found; **proposed erratum below** |
| RA-0191 | 4.1 | "In case of Cluster ID value of 0, the TLV containing it MUST be ignored." | The Flood Reflection TLV "MUST appear in L2 IIHs on all Flood Reflection Adjacencies". Ignoring it makes the IIH look like a standard L2 IIH, so a reflector receiving it would form a standard L2 adjacency, which Section 4.6 forbids; the text does not say that the adjacency must be refused instead. | ambiguity | none found |

Proposed erratum RA-0190 (RFC 9377, Section 4.5 vs 4.6; type: Technical):

```
Original Text
-------------
   A flood reflector MUST NOT form any standard L2 adjacencies.

Corrected Text
--------------
   A flood reflector MUST NOT form any standard L2 adjacencies
   except with flood reflector clients of its cluster (Section 4.5).

Notes
-----
   Section 7 repeats the 4.6 wording.
```

### RFC 9479: IS-IS Application-Specific Link Attributes {#ra_rfc9479}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 8919.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0192 | 4.2 | "In cases where conflicting values for the same application/attribute/link are advertised, the first advertisement received in the lowest-numbered Link State Protocol Data Unit (LSP) MUST be used" | "First ... received" mixes arrival order with LSP order. Within one LSP fragment the order is the TLV order; across fragments the lowest LSP number decides; but "received" suggests that a later-arriving advertisement in a lower-numbered fragment would not replace one already in use. The rule also has an exception for maximum link bandwidth (4.2.1: all values ignored), which a reader of 4.2 alone would miss. | ambiguity | none found |
| RA-0193 | 4.2, 6.2 | "Such link attribute advertisements MUST be used by standard applications and/or UDAs when no link attribute advertisements with a non-zero-length Application Identifier Bit Mask and a matching Application Identifier Bit set are present for a given link." | The condition is stated per link, not per attribute: if an application has a non-zero-mask ASLA entry for the link that carries only some attributes (for example TE metric), the zero-length entry's other attributes (for example delay) are then not usable by that application. Whether resolution is per link or per attribute is left to the reader, although Section 9 says the change was made to remove interoperability problems. | ambiguity | none found |

### RFC 9502: IGP Flexible Algorithm in IP Networks {#ra_rfc9502}

Depth: deep (IS-IS sections in full, OSPF scanned). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0194 | 6.1, 6.2 | "If the Algorithms in the IS-IS IPv4 Algorithm Prefix Reachability TLV are outside the Flex-Algorithm range (128-255), the IS-IS IPv4 Algorithm Prefix Reachability TLV MUST be ignored by the receiver." | The Algorithm is a field of each prefix entry, and a TLV carries several entries. Read literally, one entry with an out-of-range algorithm makes the receiver drop the valid entries packed in the same TLV, so the set of reachable prefixes depends on how the originator packed them. Ignoring only the offending entry is the more likely intent (the entries remain parseable). | ambiguity | none found; **proposed erratum below** |

Proposed erratum RA-0194 (RFC 9502, Section 6.1, 6.2; type: Technical):

```
Original Text
-------------
   If the Algorithms in the IS-IS IPv4 Algorithm Prefix Reachability
   TLV are outside the Flex-Algorithm range (128-255), the IS-IS
   IPv4 Algorithm Prefix Reachability TLV MUST be ignored by the
   receiver.

Corrected Text
--------------
   If the Algorithm in a prefix entry of the IS-IS IPv4 Algorithm
   Prefix Reachability TLV is outside the Flex-Algorithm range
   (128-255), that prefix entry MUST be ignored by the receiver.

Notes
-----
   The same text appears for IPv6 in Section 6.2.
```

### RFC 9800: Compressed SRv6 Segment List Encoding {#ra_rfc9800}

Depth: part. Errata: not checked. Updates: RFC 8754.

Nothing notable found at this depth.

### RFC 9843: IGP Flexible Algorithms: Bandwidth, Delay, Metrics, and Constraints {#ra_rfc9843}

Depth: deep (IS-IS sections in full, OSPF sections scanned). Errata: not checked. Updates: RFC 9350.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0195 | 4.1.3.2 | "The Bandwidth Metric MUST be set to the maximum metric value of 4,261,412,864." | In IS-IS the Generic Metric sub-TLV carries a 3-octet metric (Section 2.1: "A metric value of 0xFFFFFF is considered a maximum link metric"), so 4,261,412,864 (0xFE000000, MAX_PATH_METRIC of RFC 5305) cannot be the metric of a link; the value is also not the 0xFFFFFF "last resort" value of Section 2.1. The rule for links below the first threshold therefore has no representable result. | contradiction | none found; **proposed erratum below** |
| RA-0196 | 4.1.4.2 | "The Bandwidth Metric MUST be set to the maximum metric value of 4,294,967,296." | 4,294,967,296 is 2^32 and does not fit the 4-octet metric; Section 2.2 gives 4,294,967,295 (0xFFFFFFFF) as the maximum link metric for OSPF. | error | none found; **proposed erratum below** |
| RA-0197 | 4.1.3.1, 4.1.3.2 | "\|    Flags   \|     Reserved                                     \|" | In the IS-IS FADRB and FADBT sub-TLV figures the Flags field is drawn about 6 bits wide, while the text defines "Flags (1 octet)"; the Reserved field and the following fields therefore do not start on the bit positions the ruler shows. Meaning is clear from the text (1-octet Flags, 3-octet Reserved). | editorial | none found; **proposed erratum below** |

Proposed erratum RA-0195 (RFC 9843, Section 4.1.3.2; type: Technical):

```
Original Text
-------------
   The Bandwidth Metric MUST be set to the maximum metric value of
   4,261,412,864.

Corrected Text
--------------
   The Bandwidth Metric MUST be set to the maximum link metric value
   of 16,777,215 (0xFFFFFF).

Notes
-----
   The value looks copied from MAX_PATH_METRIC; Section 2.1 defines
   0xFFFFFF as the maximum link metric. If the intent is "unusable",
   the text should say the link is pruned.
```

Proposed erratum RA-0196 (RFC 9843, Section 4.1.4.2; type: Technical):

```
Original Text
-------------
   The Bandwidth Metric MUST be set to the maximum metric value of
   4,294,967,296.

Corrected Text
--------------
   The Bandwidth Metric MUST be set to the maximum metric value of
   4,294,967,295.

Notes
-----
   OSPF Bandwidth Threshold rules.
```

Proposed erratum RA-0197 (RFC 9843, Section 4.1.3.1, 4.1.3.2; type: Editorial):

```
Original Text
-------------
   |    Flags   |     Reserved                                     |

Corrected Text
--------------
   |     Flags     |                   Reserved                    |

Notes
-----
   Editorial.
```

### RFC 9855: Topology Independent Fast Reroute Using Segment Routing {#ra_rfc9855}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0198 | 6.1 vs 7.1 | "The active segment MUST be kept on the SR header unchanged and the RL MUST be added. (6.1) / the active segment MUST be popped and then pushed again with a label value computed according to the Segment Routing Global Block (SRGB) of Q (7.1)" | For the MPLS data plane the active node segment is popped (rule 1) or replaced by the label from Q's SRGB (rule 2), so it is not "kept unchanged". 6.1 defers "the way the RL is added" to Section 7, but its MUST covers the active segment itself. | contradiction | none found; **proposed erratum below** |

Proposed erratum RA-0198 (RFC 9855, Section 6.1 vs 7.1; type: Technical):

```
Original Text
-------------
   The active segment MUST be kept on the SR header unchanged and
   the RL MUST be added.

Corrected Text
--------------
   The active segment MUST be kept on the SR header (subject to the
   data-plane-specific rules of Section 7) and the RL MUST be added.

Notes
-----
   Editorial clarification.
```

### RFC 9885: Multi-Part TLVs in IS-IS {#ra_rfc9885}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0199 | 3.2.1, 5 | "The key consists of the 7 octets of system ID and pseudonode number plus the set of link identifiers that are present." | For an Extended IS Reachability MP-TLV the key includes "the set of link identifiers that are present", so a continuation part that does not repeat the link identifier sub-TLVs has a different key (system ID only) and, read literally, describes another link; if it repeats them, a part carrying only some identifiers (for example IPv4 but not Link Local/Remote) again has a different key. Section 5 requires replicated key information but does not say that every part MUST carry all identifier sub-TLVs, nor how a part without identifiers is matched when parallel links to the same neighbour exist. | ambiguity | none found; **proposed erratum below** |
| RA-0200 | 5 | "The order of arrival and placement of the TLV parts in LSP fragments is irrelevant. / The first occurrence in the lowest numbered LSP is used." | Placement is said to be irrelevant, yet the default conflict rule (inconsistent fixed part such as the metric, or a duplicated single-instance sub-TLV) is decided by placement. A sender that moves a part between fragments thereby changes which metric receivers use; the statement of irrelevance holds only for consistent MP-TLVs. | ambiguity | none found |

Proposed erratum RA-0199 (RFC 9885, Section 3.2.1, 5; type: Technical):

```
Original Text
-------------
   The key consists of the 7 octets of system ID and pseudonode
   number plus the set of link identifiers that are present.

Corrected Text
--------------
   The key consists of the 7 octets of system ID and pseudonode
   number plus the set of link identifiers that are present. When
   link identifiers are used, every part of the MP-TLV MUST carry
   the same set of link identifier sub-TLVs.

Notes
-----
   Without that rule, receivers either merge parallel links or split
   one link.
```

### RFC 9917: IGP Flexible Algorithms Reverse Affinity Constraint {#ra_rfc9917}

Depth: deep. Errata: not checked. Updates: RFC 9350, RFC 9843.

Nothing notable found at this depth.

### RFC 9929: IGP Unreachable Prefix Announcement {#ra_rfc9929}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### Other RFCs in this area {#ra_isis_other}

Mechanical checks only, no finding: RFC 3630 (Traffic Engineering (TE) Extensions to OSPF Version 2), RFC 4444 (Management Information Base for Intermediate System to Intermediate Sy), RFC 5089 (IS-IS Protocol Extensions for Path Computation Element (PCE) Discovery), RFC 5306 (Restart Signaling for IS-IS), RFC 5316 (ISIS Extensions in Support of Inter-Autonomous System (AS) MPLS and GM).

## MPLS, LDP and mLDP {#ra_ldp}

44 RFCs in this area (28 deep, 10 read, 4 light, 2 scan); 45 findings, 18 of them proposed errata.

### RFC 3032: MPLS Label Stack Encoding {#ra_rfc3032}

Depth: deep. Errata: checked (checked: 4 (3 verified, 1 held; all editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0046 | 2.3.2 | "Since an ICMP message is  never sent as a result of" | Overstates RFC 1122: only ICMP error messages must not be sent in response to ICMP error messages. An LSR generating ICMP for a labelled Echo Request that expires must still be allowed to send Time Exceeded. | ambiguity | 982 (Verified) |
| RA-0047 | 4.2 | "hex 8281 (MPLS)." | The PPP protocol number 0x8281 is the MPLS Control Protocol (MPLSCP); 0x0281 is MPLS unicast. | editorial | 2166 (Verified) |

### RFC 3036: LDP Specification {#ra_rfc3036}

Depth: read (obsoleted by RFC 5036; checked only for the mechanical hits). Errata: not checked. 

Nothing notable found at this depth.

### RFC 3212: Constraint-Based LSP Setup using LDP {#ra_rfc3212}

Depth: scan (mechanical checks only). Errata: not checked. 

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

### RFC 3429: Assignment of the 'OAM Alert Label' for Multiprotocol Label Switching Architecture (MPLS) Operation and Maintenance (OAM) Functions {#ra_rfc3429}

Depth: light (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 3443: Time To Live (TTL) Processing in Multi-Protocol Label Switching (MPLS) Networks {#ra_rfc3443}

Depth: read (normative statements of 2 and 3). Errata: not checked. Updates: RFC 3032.

Nothing notable found at this depth.

### RFC 3478: Graceful Restart Mechanism for Label Distribution Protocol {#ra_rfc3478}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0201 | 3.3, 4 | "Once an LSR releases a label, the LSR SHOULD NOT re-use this label ... for at least the sum of the FT Reconnect Timeout plus Recovery Time / this document requires that labels not be re-used until at least the sum of Reconnect Timeout plus Recovery Time." | Section 3.3 states the label hold-down as SHOULD NOT; Section 4 says the document "requires" it. The text also does not say which Recovery Time is meant (the value advertised before or after the neighbour's restart; a helper learns the new one only after reconnecting) nor whether the rule applies to labels released while no restart is in progress (the wording applies to every release towards a GR-capable neighbour). | contradiction | not checked; **proposed erratum below** |
| RA-0202 | 3.1.2 | "the LSR would search its MPLS forwarding state for an entry that indicates Label pop (means no outgoing label), and the next hop equal to the next hop for that FEC associated with the entry" | For an egress that allocates a unique label per FEC the text says the FEC must be preserved, but the search criterion given is only "Label pop" plus next hop; unlike the corresponding paragraph of 3.1.1 (item (c) "has the same FEC") it does not say to match the FEC, so with several FECs sharing a next hop the entry found is not determined. The phrase "the next hop for that FEC associated with the entry" appears garbled. | ambiguity | not checked; **proposed erratum below** |
| RA-0203 | 2, 3.3 | "the LSR knows that the neighbor is capable of preserving its MPLS forwarding state across the restart (as was indicated by the FT Session TLV in the Initialization message received from the neighbor)" | Which field indicates the capability is not stated: Section 2 says an FT Reconnect Timeout of 0 means the sender will not preserve its state, and a Recovery Time of 0 (meaningful only after a restart) means it did not. A helper must infer that "capable" means a non-zero FT Reconnect Timeout in the previous session. The start instants of the "lesser of the Recovery Time ... and Maximum Recovery Time" period at the helper are also not stated. | ambiguity | not checked |
| RA-0204 | 4 | "LSRs that implement the mechanism described here are subject to to additional denial-of-service attacks" | Doubled "to"; heading "Security Consideration" singular. The countermeasure cited is the TCP MD5 option of [LDP], since superseded by TCP-AO (RFC 5925) for LDP (RFC 7349 context); an update would cite both. | editorial | not checked |

Proposed erratum RA-0201 (RFC 3478, Section 3.3, 4; type: Technical):

```
Original Text
-------------
   To reduce this issue, this document requires that labels not be
   re-used until at least the sum of Reconnect Timeout plus Recovery
   Time.

Corrected Text
--------------
   To reduce this issue, Section 3.3 specifies that labels SHOULD
   NOT be re-used until at least the sum of the FT Reconnect Timeout
   plus the Recovery Time advertised by the neighbor.

Notes
-----
   The normative statement in Section 3.3 is SHOULD NOT; Section 4
   overstates it. It is also unclear which advertised Recovery Time
   applies.
```

Proposed erratum RA-0202 (RFC 3478, Section 3.1.2; type: Technical):

```
Original Text
-------------
   In such case, the LSR would search its MPLS forwarding state for
   an entry that indicates Label pop (means no outgoing label), and
   the next hop equal to the next hop for that FEC associated with
   the entry

Corrected Text
--------------
   In such case, the LSR would search its MPLS forwarding state for
   an entry that (a) indicates Label pop (means no outgoing label),
   (b) indicates the next hop equal to the next hop for that FEC,
   and (c) has the same FEC as the one associated with the entry

Notes
-----
   Without matching the FEC, the search is ambiguous when several
   FECs with distinct labels share a next hop.
```

### RFC 3479: Fault Tolerance for the Label Distribution Protocol (LDP) {#ra_rfc3479}

Depth: read (Sections 4.1 to 4.3 and 8.2 FT Session TLV read; the FT protection / check-pointing procedures skimmed). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0205 | 8.2 | "If the S bit is also set to 1 then the C bit indicates that check-pointing is applied only to Sequence Numbered FT Labels. / 1   x   1   0    Same as (S=1,A=x,C=0,L=0)" | The flag description gives C a distinct meaning when S is set (check-pointing restricted to Sequence Numbered FT Labels), while the summary table says S=1, C=1 is the same as S=1, C=0. The FT Reconnect Timeout also has opposite meanings for the value zero depending on the flags: "the sending LSR will preserve state and resources indefinitely" with S or C set, but per RFC 3478 Section 2 (L set) zero means the sender "will not preserve its forwarding state"; 4.2.2's rule "a value of zero is treated as positive infinity" is stated without the L-bit qualification. | ambiguity | not checked |

### RFC 4950: ICMP Extensions for Multiprotocol Label Switching {#ra_rfc4950}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5036: LDP Specification {#ra_rfc5036}

Depth: deep. Errata: checked (checked: 11 (1 verified, 6 held, 4 rejected; all editorial or rejected questions)). Obsoletes: RFC 3036.

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

### RFC 5283: LDP Extension for Inter-Area Label Switched Paths (LSPs) {#ra_rfc5283}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5331: MPLS Upstream Label Assignment and Context-Specific Label Space {#ra_rfc5331}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0206 | 8 | "If the IPv4 network mask is greater than 12 bits, it is possible to map the remaining 20 bits into a unique context label value." | A mask of exactly 12 bits also leaves 20 host bits, which fit the 20-bit label; "greater than 12" excludes /12 needlessly (the subsequent offset rule, host part + 0x10 when not greater than 0xFFFEF, already handles the top of the range). "Greater than or equal to 12" is meant. With a mask longer than 12 bits the "remaining" bits are fewer than 20, so "the remaining 20 bits" is also imprecise. | error | not checked; **proposed erratum below** |
| RA-0207 | 6 | "an LSR distributes an upstream-assigned label binding for a FEC F if it is either (a) the ingress LSR for FEC F, or (b) if it has already received an upstream label binding for that FEC from its adjacent upstream LSR for FEC F, or (c) if it has received a request for a downstream label binding from its upstream adjacent LSR." | Condition (c) mixes the two schemes: an upstream-assigned binding is distributed to the downstream LSR, yet the trigger given is a request for a downstream-assigned binding from the upstream LSR. Section 4.1 also forbids using both kinds between the same adjacent pair. The intended trigger (a request from the downstream adjacent LSR for an upstream-assigned binding) has to be guessed. | ambiguity | not checked |

Proposed erratum RA-0206 (RFC 5331, Section 8; type: Technical):

```
Original Text
-------------
   If the IPv4 network mask is greater than 12 bits, it is possible
   to map the remaining 20 bits into a unique context label value.

Corrected Text
--------------
   If the IPv4 network mask is 12 bits or longer, it is possible to
   map the host part (at most 20 bits) into a unique context label
   value.

Notes
-----
   A /12 mask leaves exactly 20 host bits, which fit in a label.
```

### RFC 5332: MPLS Multicast Encapsulations {#ra_rfc5332}

Depth: read (all normative statements). Errata: not checked. Updates: RFC 3032, RFC 4023.

Nothing notable found at this depth.

### RFC 5443: LDP IGP Synchronization {#ra_rfc5443}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0208 | 2 | "Indeed, if a link is configured with 2^24-1 (the maximum link metric per [RFC5305]), then this link is not advertised in the topology." | RFC 5305 Section 3 does not withhold such a link from the topology: a link advertised with metric 2^24 - 1 is flooded (and may be used for TE) but "MUST NOT be considered during the normal SPF computation". The conclusion (use 2^24 - 2 so the link stays usable as a last resort) is right, the stated reason is not. The text also gives no value for IS-IS narrow metrics (TLV 2, maximum 63), where no "last resort" value below the maximum exists, nor for OSPFv3. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0208 (RFC 5443, Section 2; type: Technical):

```
Original Text
-------------
   Indeed, if a link is configured with 2^24-1 (the maximum link
   metric per [RFC5305]), then this link is not advertised in the
   topology.

Corrected Text
--------------
   Indeed, if a link is advertised with 2^24-1 (the maximum link
   metric per [RFC5305]), then this link is not considered during
   the normal SPF computation.

Notes
-----
   RFC 5305 Section 3 excludes such a link from normal SPF; it
   remains in the advertised topology.
```

### RFC 5561: LDP Capabilities {#ra_rfc5561}

Depth: deep (3 to 9). Errata: no verified errata in the index; page not read. Updates: RFC 5036.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0209 | 6, 7 | "If the U-bit is 1, then the speaker MUST silently ignore the Capability Parameter and allow the session to be established. However, if the U-bit is 0, then speaker SHOULD send a Notification message to the peer before terminating the session." | The U-bit handling of an unsupported Capability Parameter is specified only for Initialization messages (Section 6). For a Capability message (Section 7) the text does not say whether an unsupported capability with U = 0 terminates an established session, is answered with Unsupported Capability without closing it, or is ignored; nor what a speaker does when a peer withdraws (S = 0) a capability it never advertised, or changes one whose capability document allows only Initialization (for example RFC 6389 Section 3). | ambiguity | not checked |

### RFC 5586: MPLS Generic Associated Channel {#ra_rfc5586}

Depth: deep (4 in full). Errata: errata exist; not read. Updates: RFC 3032, RFC 4385, RFC 5085.

Nothing notable found at this depth.

### RFC 5918: Label Distribution Protocol (LDP) 'Typed Wildcard' Forward Equivalence Class (FEC) {#ra_rfc5918}

Depth: deep (read in full). Errata: errata exist; not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0210 | 6 | "Len FEC Type Info: Two octets.  It MUST be set to 0x0002." | Section 3 defines "Len FEC Type Info" as a one-octet field, and Figure 3 shows a one-octet "Len = 2". "Two octets" here describes the value (the length of the Address Family), not the field; read literally, the field size contradicts Figure 1 and Figure 3. The bit rulers of Figures 1 and 3 also run to 32 columns ("... 0 1 2"), one more than the 32-bit layout. | error | not checked (verified errata exist; content not read); **proposed erratum below** |
| RA-0211 | 4, 7 | "An LDP implementation that supports the Typed Wildcard FEC Element MUST support it for every FEC Element Type defined in [RFC5036]." | RFC 5036 defines the Wildcard (0x01) and Prefix (0x02) FEC Element types; Section 7 says the FEC Element Type "MUST NOT be either 0x01 or 0x03" and that no typed wildcard is needed for the Wildcard element. Section 4 therefore requires support for a type that Section 7 forbids; only the Prefix type is meant. | contradiction | not checked |

Proposed erratum RA-0210 (RFC 5918, Section 6; type: Technical):

```
Original Text
-------------
   Len FEC Type Info: Two octets.  It MUST be set to 0x0002.

Corrected Text
--------------
   Len FEC Type Info: One octet.  It MUST be set to 0x02 (the two
   octets of the Address Family).

Notes
-----
   Section 3: "Len FEC Type Info: One octet that specifies the
   length in octets of the FEC Type Specific information field."
   Figure 3 shows an 8-bit "Len = 2".
```

### RFC 5919: Signaling LDP Label Advertisement Completion {#ra_rfc5919}

Depth: deep (3 to 5). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0212 | 4, 4.1 | "An LDP speaker SHOULD start a per-peer internal timer, called 'EOL Notification' timer ... This timer is reset by the subsequent label advertisement, and stopped by the End-of-LIB Notification message." | End-of-LIB is sent "per Forwarding Equivalence Class (FEC) Type" (Section 4), but the timer is per peer. With several FEC types on one session (IPv4 and IPv6 prefixes, PW FECs, mLDP), the text does not say whether the first End-of-LIB stops the timer for all types, whether a timeout counts as End-of-LIB for every type still outstanding, or which FEC types a speaker is expected to signal (all it supports, or only those both peers enabled through capabilities). | ambiguity | not checked |

### RFC 6138: LDP IGP Synchronization for Broadcast Networks {#ra_rfc6138}

Depth: read (Informational). Errata: no verified errata in the index; page not read. Updates: RFC 5443.

Nothing notable found at this depth.

### RFC 6370: MPLS Transport Profile (MPLS-TP) Identifiers {#ra_rfc6370}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6378: MPLS Transport Profile (MPLS-TP) Linear Protection {#ra_rfc6378}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6388: Label Distribution Protocol Extensions for Point-to-Multipoint and Multipoint-to-Multipoint Label Switched Paths {#ra_rfc6388}

Depth: deep (2, 3.1 to 3.2, 5, 11 in full; 3.3, 7, 8 by MUST/SHOULD). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0213 | 2.4.1.1 | "1. The candidate upstream LSRs are numbered from lower to higher IP address. ... 3. The selected upstream LSR U is the LSR that has the number H." | The procedure exists so that all receivers on a LAN elect the same upstream LSR, but it does not say which address of a candidate is used (LSR Id, LDP transport address, or the candidate's address on the LAN), how IPv4 and IPv6 candidates are ordered against each other, or that numbering starts at 0 (H = CRC32 mod N ranges from 0 to N - 1, so numbering from 1 leaves the highest candidate unused and H = 0 unmatched). Two receivers that resolve these differently elect different forwarders, which is the duplication the procedure is meant to avoid. | ambiguity | not checked |
| RA-0214 | 2.4.2.2 | "then Z propagates the Label Withdraw for <X, Y> to its upstream T, by sending a Label Withdraw <X, Y, L1> where L1 is the label Z had previously advertised to T" | Section 2.4.1.4 uses T for the downstream LSR that sent the Label Mapping and U for the upstream LSR; here T names the upstream. The procedure is clear from "its upstream", but the letter swap makes the two sections read as if Withdraws go to the downstream peer. | editorial | not checked |
| RA-0215 | 2.1, 3.1 | "The P2MP Capability TLV MUST be advertised in the LDP Initialization message. ... If the peer has not advertised the corresponding capability, then label messages using the P2MP FEC Element SHOULD NOT be sent to the peer." | The capability is tied to Initialization only (no dynamic advertisement via RFC 5561 Capability messages, unlike RFC 6389 which says so explicitly), and sending P2MP / MP2MP FEC Elements to a peer without the capability is only a SHOULD NOT. Receive handling of such an element from a peer that did not advertise the capability is not stated (RFC 5561 leaves it to the capability document). | ambiguity | not checked |

### RFC 6389: MPLS Upstream Label Assignment for LDP {#ra_rfc6389}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0216 | 6, 9 | "2. The following hash is performed: H = (Sum Opaque value) modulo N, where N is the number of candidate upstream LSRs." | RFC 6388 Section 2.4.1.1 (published in the same month for the same purpose) uses H = CRC32(Opaque Value) modulo N, and Section 9 of this document says "The hashing algorithm used on LAN interfaces is taken from [RFC6388]". "Sum" is also undefined (sum of octets, of 16- or 32-bit words, and in what width). An LSR following this text and one following RFC 6388 elect different upstream LSRs on the same LAN. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0216 (RFC 6389, Section 6, 9; type: Technical):

```
Original Text
-------------
   2. The following hash is performed: H = (Sum Opaque value) modulo
   N,

Corrected Text
--------------
   2. The following hash is performed: H = (CRC32(Opaque Value))
   modulo N,

Notes
-----
   RFC 6388 Section 2.4.1.1 defines the hash as CRC32 of the Opaque
   Value; this document's Acknowledgements say the algorithm is
   taken from RFC 6388, but the text says "Sum", which is undefined
   and yields a different election.
```

### RFC 6512: Using Multipoint LDP When the Backbone Has No Route to the Root {#ra_rfc6512}

Depth: deep (2, 3). Errata: errata exist; not read. 

Nothing notable found at this depth.

### RFC 6667: LDP 'Typed Wildcard' Forwarding Equivalence Class (FEC) for PWid and Generalized PWid FEC Elements {#ra_rfc6667}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6720: The Generalized TTL Security Mechanism (GTSM) for the Label Distribution Protocol (LDP) {#ra_rfc6720}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 5036.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0217 | 2.2, 2.3, 3 | "If an LSR that has sent and received LDP Link Hello with G flag = 1 from the directly connected neighbor, then the LSR MUST enforce GTSM procedures ... in the forthcoming TCP Transport Connection with that neighbor." | The decision is described per Link Hello, but one LDP session can rest on several link adjacencies (parallel links) and on a targeted adjacency at the same time (case c of Section 3). The text does not say what to do when the Hellos on different links disagree on G, when the G flag changes on an established session, or when the only link adjacency goes away while the targeted one keeps the session up (the session is then multi-hop capable but GTSM is already enforced). Two peers resolving this differently can refuse each other's TCP segments. | ambiguity | not checked |

### RFC 6790: The Use of Entropy Labels in MPLS Forwarding {#ra_rfc6790}

Depth: deep. Errata: checked (checked: 1 (3431 held, technical)). Updates: RFC 3031, RFC 3107, RFC 3209, RFC 5036.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0053 | 5.2 | "attribute of value 28.  The inclusion of this attribute with an NLRI indicates that the advertising BGP router can process entropy labels" | The Entropy Label Capability attribute is described only as "of value 28"; the text does not say that its length is zero and it carries no data. Together with RFC 7606 section 4 (a zero-length attribute is a syntax error unless its specification allows length zero), a receiver can treat every ELC attribute as malformed. RFC 7447 has since deprecated the attribute, but old speakers may still send it. | ambiguity | 3431 (Held) |

### RFC 6826: Multipoint LDP In-Band Signaling for Point-to-Multipoint and Multipoint-to-Multipoint Label Switched Paths {#ra_rfc6826}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 7032: LDP Downstream-on-Demand in Seamless MPLS {#ra_rfc7032}

Depth: read. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 7140: LDP Extensions for Hub and Spoke Multipoint Label Switched Path {#ra_rfc7140}

Depth: deep (3, 6). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0218 | 6 | "In order to ensure that the leaf node sends the LSP Ping Echo Reply along the HSMP upstream path, the R flag (Validate Reverse Path) in the Global Flags field defined in [RFC6426] is reused here." | In RFC 6426 3.4 the R flag asks the responder to return reverse-path FEC information; it does not select the path the reply takes. Here the same flag also obliges the leaf to send the reply on the HSMP upstream path. A responder that implements only RFC 6426 sends the reply by its usual means with a Reverse-path Target FEC Stack, so the root cannot tell whether the upstream path was exercised. | ambiguity | not checked |

### RFC 7246: Multipoint Label Distribution Protocol In-Band Signaling in a Virtual Routing and Forwarding (VRF) Table Context {#ra_rfc7246}

Depth: read (normative lines and opaque encodings). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 7274: Allocating and Retiring Special-Purpose MPLS Labels {#ra_rfc7274}

Depth: read (2, 3 in full). Errata: no verified errata in the index; page not read. Updates: RFC 3032, RFC 3038, RFC 3209, RFC 3811, RFC 4182, RFC 4928, RFC 5331, RFC 5586, RFC 5921, RFC 5960, RFC 6391, RFC 6478, RFC 6790.

Nothing notable found at this depth.

### RFC 7307: LDP Extensions for Multi-Topology {#ra_rfc7307}

Depth: deep (3, 4.1, 5 in full; 4.3, 9 by MUST/SHOULD). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0219 | 3.3 | "\|Typed Wcard (5)\|    FEC Type   \|   Len = 6     \|  AF = MT IP ..\|" | Figure 4 draws the type-specific part as a 2-octet Address Family and a 2-octet MT-ID, 4 octets, but labels Len = 6. RFC 5918 defines Len as the length of the type-specific information, so either the figure omits a 2-octet field (for example a Reserved field as in the MT Prefix FEC element) or the label is wrong. | contradiction | not checked; **proposed erratum below** |
| RA-0220 | 3.5.1, 3.5.2 | "The MT-ID field of the MT Typed Wildcard FEC element MUST be set to "Wildcard Topology" when it is specified in the MT Capability TLV." | Section 3.5.2 announces capability "for multiple Multi-Topologies" with "one or more MT Typed FEC elements", each with its "corresponding 'MT-ID'", which a mandatory Wildcard Topology MT-ID makes impossible. | contradiction | not checked |
| RA-0221 | 3.5.2 | "Each side of the node sends a label release to its peer once it receives the label release messages even though each side has already cleaned up all the LSPs locally." | In RFC 5036 a Label Release answers a Label Withdraw; the sentence follows the withdrawal of all non-default-MT mappings, so "once it receives the label withdraw messages" is meant. As written, each side would answer Releases with Releases. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0219 (RFC 7307, Section 3.3; type: Technical):

```
Original Text
-------------
   |Typed Wcard (5)|    FEC Type   |   Len = 6     |  AF = MT IP ..|

Corrected Text
--------------
   |Typed Wcard (5)|    FEC Type   |   Len = 4     |  AF = MT IP ..|

Notes
-----
   Address Family (2) + MT-ID (2) = 4. If a Reserved field was
   intended, the figure needs it instead.
```

Proposed erratum RA-0221 (RFC 7307, Section 3.5.2; type: Editorial):

```
Original Text
-------------
   Each side of the node sends a label release to its peer once it
   receives the label release messages

Corrected Text
--------------
   Each side of the node sends a label release to its peer once it
   receives the label withdraw messages

Notes
-----
   Per RFC 5036 3.5.10 a Label Release is sent in response to a
   Label Withdraw.
```

### RFC 7349: LDP Hello Cryptographic Authentication {#ra_rfc7349}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0222 | 6.1, 2.3 | "It is set to 24 for HMAC-SHA-1, 36 for HMAC-SHA-256, 52 for HMAC-SHA-384, and 68 for HMAC-SHA-512." | Section 2.3 defines the Length as the value field "including the Security Association ID and Cryptographic Sequence Number fields", i.e. 4 + 8 + digest: 32, 44, 60 and 76. The values in 6.1 are 4 + digest and leave out the 8-octet sequence number. A sender using 6.1 produces a TLV whose Length stops 8 octets short of its Authentication Data. | contradiction | not checked; **proposed erratum below** |
| RA-0223 | 5.2 | "Hello Message refers to the LDP Hello message excluding the IP and the UDP headers." | In RFC 5036 terms the Hello message is one message inside an LDP PDU; the PDU header (Version, PDU Length, LDP Identifier) precedes it. "The LDP Hello message excluding the IP and the UDP headers" can mean the message alone or the whole UDP payload. If the PDU header is not covered, the LDP Identifier, which names the LSR and label space the Hello is for, is not authenticated and can be altered in transit. | ambiguity | not checked; **proposed erratum below** |
| RA-0224 | 5.1 | "In this application, Ko is always L octets long. Keys that are longer than the bit length of the hash function are hashed to force them to this length" | As in RFC 5310 3.3, the key is hashed when Ks is longer than the digest length L, whereas RFC 2104 HMAC hashes it only above the block size B, and an L-octet Ko is then combined with B-octet ipad / opad without saying it is zero-extended. An implementation that feeds Ks to a standard HMAC routine produces different digests for 33 to 64 octet keys (HMAC-SHA-256) or 49 to 128 octet keys (HMAC-SHA-384 / -512). | ambiguity | not checked |
| RA-0225 | 4, 6.2 | "the 2-octet LDP Cryptographic Protocol ID is appended to the authentication key prior to use (refer to Section 8)." | The Protocol ID assignment is in Section 9 (IANA Considerations), not Section 8 (Security Considerations). Section 6.2 likewise says the hash is computed "as explained in Section 3", while the computation is in Section 5. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0222 (RFC 7349, Section 6.1, 2.3; type: Technical):

```
Original Text
-------------
   It is set to 24 for HMAC-SHA-1, 36 for HMAC-SHA-256, 52 for
   HMAC-SHA-384, and 68 for HMAC-SHA-512.

Corrected Text
--------------
   It is set to 32 for HMAC-SHA-1, 44 for HMAC-SHA-256, 60 for
   HMAC-SHA-384, and 76 for HMAC-SHA-512.

Notes
-----
   Section 2.3: Length covers the Security Association ID (4), the
   Cryptographic Sequence Number (8) and the Authentication Data (20
   32
   48
   64 octets).
```

Proposed erratum RA-0223 (RFC 7349, Section 5.2; type: Technical):

```
Original Text
-------------
   Hello Message refers to the LDP Hello message excluding the IP
   and the UDP headers.

Corrected Text
--------------
   Hello Message refers to the LDP PDU carrying the Hello message
   (the LDP PDU header and the Hello message), excluding the IP and
   the UDP headers.

Notes
-----
   The LDP Identifier is in the PDU header, not in the Hello
   message; it should be covered by the digest.
```

Proposed erratum RA-0225 (RFC 7349, Section 4, 6.2; type: Editorial):

```
Original Text
-------------
   (refer to Section 8) ... and computes the Hash using the
   authentication key specified by the received Security Association
   ID field, as explained in Section 3.

Corrected Text
--------------
   (refer to Section 9) ... as explained in Section 5.

Notes
-----
   Section 8 is Security Considerations and Section 3 only lists
   algorithms; the Protocol ID is in Section 9 and the digest
   computation in Section 5.
```

### RFC 7358: Label Advertisement Discipline for LDP Forwarding Equivalence Classes (FECs) {#ra_rfc7358}

Depth: read (read in full; procedural update of FEC documents). Errata: no verified errata in the index; page not read. Updates: RFC 3212, RFC 4447, RFC 5036, RFC 5918, RFC 6388, RFC 7140.

Nothing notable found at this depth.

### RFC 7438: Multipoint LDP (mLDP) In-Band Signaling with Wildcards {#ra_rfc7438}

Depth: deep (3 to 6). Errata: no verified errata in the index; page not read. Updates: RFC 6826, RFC 7246.

Nothing notable found at this depth.

### RFC 7473: Controlling State Advertisements of Non-negotiated LDP Applications {#ra_rfc7473}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0226 | 4.1, 4.2 | "Any other value in this field MUST be treated as an error. / the receiver MUST ignore and discard the element and continue processing the rest of the TLV. / it SHOULD silently ignore/skip such an element" | Three statements give three requirement levels for an unknown App value: "MUST be treated as an error", "MUST ignore and discard the element", and (4.2) "SHOULD silently ignore/skip". Duplicate App types make the whole TLV "malformed" but it is then only "SHOULD" discarded. | contradiction | not checked; **proposed erratum below** |
| RA-0227 | 4.1, 4.2 | "The value of the U-bit for the TLV MUST be set to 1 so that a receiver MUST silently ignore this TLV if unknown to it / If a receiving LDP speaker does not understand the SAC capability TLV, then it MUST respond to the sender with an "Unsupported TLV" notification" | With U = 1, RFC 5036 3.3 requires an unknown TLV to be silently ignored, which Section 4.1 repeats; Section 4.2 then requires the same receiver to answer with an Unsupported TLV notification. A speaker that does not understand the TLV cannot be bound by this document in any case, so the 4.2 sentence can only describe RFC 5561 behaviour, and RFC 5561 does not require a notification for an unknown capability with U = 1 in an Initialization message. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0226 (RFC 7473, Section 4.1, 4.2; type: Technical):

```
Original Text
-------------
   Any other value in this field MUST be treated as an error.

Corrected Text
--------------
   Any other value in this field is unknown; an element with an
   unknown App value MUST be ignored as described below.

Notes
-----
   Sections 4.1 and 4.2 disagree on both the action and the
   requirement level.
```

Proposed erratum RA-0227 (RFC 7473, Section 4.1, 4.2; type: Technical):

```
Original Text
-------------
   If a receiving LDP speaker does not understand the SAC capability
   TLV, then it MUST respond to the sender with an "Unsupported TLV"
   notification as described in "LDP Capabilities" [RFC5561].

Corrected Text
--------------
   A receiving LDP speaker that does not understand the SAC
   capability TLV ignores it silently (U-bit set to 1), as described
   in "LDP Capabilities" [RFC5561]; the sender then continues to
   receive state for all applications.

Notes
-----
   Section 4.1 sets U=1 precisely so that unknown receivers ignore
   the TLV.
```

### RFC 7552: Updates to LDP for IPv6 {#ra_rfc7552}

Depth: deep. Errata: checked (checked: 1 (5690 verified, editorial)). Updates: RFC 5036, RFC 6720.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0054 | 6.1.1 | "Dual-Stack capability: TLV code point (Ox0701)" | The Dual-Stack capability TLV code point is printed with a letter O ("Ox0701"); it is 0x0701. | editorial | 5690 (Verified) |
| RA-0228 | 6.1.1 | "\|TR     \|        Reserved       \|     MBZ                       \|" | The figure has three fields after TR (Reserved, MBZ) but the text defines only TR and Reserved, and no TLV Length is given (4 by the figure). A receiver does not know whether a Length other than 4 is an error. The section also does not say what happens when both sides agree on TR = 0110 (LDPoIPv6) but only IPv4 Hellos are received from the peer (for example, IPv6 Hellos filtered): no IPv6 transport address is known, so rule 2b cannot be applied and no session forms, while a TR mismatch (rule 1) discards all Hellos and also prevents any session. | ambiguity | 5690 (Verified, different issue); **proposed erratum below** |
| RA-0229 | 7.2 | "MUST NOT advertise FEC-label bindings for link-local or IPv4-mapped IPv6 addresses (defined in Section 2.5.5.2 of [RFC4291])" | Section 2.5.5.2 of RFC 4291 defines IPv4-mapped addresses only; link-local unicast addresses are defined in Section 2.5.6. Section 7.1 cites 2.5.5.2 correctly for IPv4-mapped addresses alone. | editorial | not checked |

Proposed erratum RA-0228 (RFC 7552, Section 6.1.1; type: Technical):

```
Original Text
-------------
   |TR     |        Reserved       |     MBZ                       |

Corrected Text
--------------
   |TR     |                        Reserved                       |
     (and add: "Length: 4")

Notes
-----
   The text defines TR (4 bits) and Reserved; the figure
   additionally shows a 16-bit MBZ field. The TLV Length is not
   stated.
```

### RFC 7715: Multipoint LDP (mLDP) Node Protection {#ra_rfc7715}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0230 | 2.3, 5.4 | "Num PLR entry: Element as an unsigned integer followed by the number of "PLR entry" fields / S bit: Set to 1 to announce and 0 to withdraw the capability" | The size of "Num PLR entry" is given only by the figure (one octet) and its description is garbled. A PLR Status element carries one Address Family, so an MP2MP root with members of both families must send two elements, and "remove all PLR addresses" (Num = 0) applies to one family only; this is implied, not stated. In 5.4, one capability carries both P and M, but withdrawal (S = 0) is per TLV, so it is not stated how an LSR that is both PLR and MPT withdraws only one role (presumably by re-announcing with S = 1 and only the remaining bit). | ambiguity | not checked |

### RFC 8223: Application-Aware Targeted LDP {#ra_rfc8223}

Depth: deep. Errata: not checked. Updates: RFC 7473.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0231 | 2.2 | "On receipt of a valid TAC TLV, an LSR MUST generate its own TAC TLV with TAEs consisting of unique TA-Ids that it supports over the tLDP session." | The procedure assumes the responder sees the initiator's TAC before sending its own Initialization, which holds only when the responder is the passive side (RFC 5036 2.5.4); a responder that has the active role sends its Initialization first. The text also allows a TAC with "zero or more TAEs" while a null intersection forces 'Targeted Application Capability Mismatch', so an empty TAC always rejects the session; the unit of "a maximum value -- that is, 0xFFFF" for the retry interval is not given; and the registry text says the range is 0x0001-0xFFFE while listing 0x0000 as Reserved and leaving 0xFFFF unassigned and unlisted. | ambiguity | not checked |

### RFC 8320: LDP Extensions to Support Maximally Redundant Trees {#ra_rfc8320}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0232 | 4.1 | "S-bit:  The State bit MUST be 1 if used in the LDP Initialization message.  MAY be set to 0 or 1 in the dynamic Capability message to advertise or withdraw the capability, respectively, as described in [RFC5561]." | "0 or 1 ... to advertise or withdraw ... respectively" maps 0 to advertise and 1 to withdraw, the reverse of RFC 5561 Section 3 (S = 1 announces, S = 0 withdraws), which the same sentence cites and which the Initialization rule (S MUST be 1 to advertise) follows. | error | none found; **proposed erratum below** |
| RA-0233 | 4.1.1, 5.2.3, 6 | "An LSR advertising the LDP MRT Capability MUST also advertise the LDP Multi-Topology (MT) Capability." | No issue in the RFC text (cross-reference record only). The MT-capability requirement is in Section 4.1.1 and the egress / Rainbow rules in Sections 4.2, 5.1.1 and 5.2.3 / 5.2.4; Section 6 is Security Considerations and Section 5 has no capability rule. | editorial | none found |

Proposed erratum RA-0232 (RFC 8320, Section 4.1; type: Technical):

```
Original Text
-------------
   MAY be set to 0 or 1 in the dynamic Capability message to
   advertise or withdraw the capability, respectively, as described
   in [RFC5561].

Corrected Text
--------------
   MAY be set to 1 or 0 in the dynamic Capability message to
   advertise or withdraw the capability, respectively, as described
   in [RFC5561].

Notes
-----
   RFC 5561 Section 3 defines S = 1 as advertising and S = 0 as
   withdrawing a capability.
```

### RFC 8356: Experimental Codepoint Allocation for the Path Computation Element Communication Protocol (PCEP) {#ra_rfc8356}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 5440.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0234 | 4 | "This document sets aside object identifiers 65504-65535 for experimentation as described in Section 6.2." | The range 65504-65535 is a range of TLV type codes, not object identifiers, and the IANA action for it is in Section 6.3 (Section 6.2 is the PCEP Objects registry). A copy of the Section 3 sentence. | editorial | none found; **proposed erratum below** |
| RA-0235 | 5 | "A PCEP implementation that receives an experimental PCEP message that it does not recognize reacts by sending a PCErr message with Error-Type=2" | No error code is defined for an experimental object or TLV that is recognised but belongs to a different experiment (Section 7 warns of this case). Experimental Error-Types were added later (RFC 9756), so a receiver of RFC 8356 code points alone has only the generic unknown-object handling. | ambiguity | none found |

Proposed erratum RA-0234 (RFC 8356, Section 4; type: Editorial):

```
Original Text
-------------
   This document sets aside object identifiers 65504-65535 for
   experimentation as described in Section 6.2.

Corrected Text
--------------
   This document sets aside TLV type codes 65504-65535 for
   experimentation as described in Section 6.3.

Notes
-----
   Section 6.3 holds the IANA action for the PCEP TLV Type
   Indicators registry.
```

### RFC 9658: Multipoint LDP Extensions for Multi-Topology Routing {#ra_rfc9658}

Depth: deep. Errata: not checked. Updates: RFC 7307.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0236 | 3.1.1-3.1.3, 7 | "Reserved: This 8-bit field MUST be zero on transmission and MUST be ignored on receipt." | Sections 3.1.2 and 3.1.3 do not say whether the MT root address length in the MP FEC element counts the Reserved / IPA / MT-ID word that follows the address, while the LSP ping encoding in Section 7 uses lengths of 8 and 20 (address plus word). Implementations can disagree on the length field and so fail to parse each other's FECs. | ambiguity | none found |

### RFC 9789: MPLS Network Actions (MNAs) Framework {#ra_rfc9789}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### Other RFCs in this area {#ra_ldp_other}

Mechanical checks only, no finding: RFC 3468 (The Multiprotocol Label Switching (MPLS) Working Group decision on MPL).

## Pseudowires, VPLS and ICCP {#ra_pw}

20 RFCs in this area (13 deep, 5 read, 2 light); 28 findings, 10 of them proposed errata.

### RFC 4385: Pseudowire Emulation Edge-to-Edge (PWE3) Control Word for Use over an MPLS PSN {#ra_rfc4385}

Depth: deep. Errata: checked (checked: 1 (1743 verified, technical)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0055 | 4, 4.1, 4.2 | "The sequence number that follows 65535 (maximum unsigned 16-bit number) is one." | The rules that exclude zero (wrap from 65535 to 1, zero meaning "not used") are written for every PW type, but TDM pseudowires (SAToP, CESoPSN, TDMoIP) use zero as an ordinary sequence number. The erratum limits the zero-excluding rules to non-TDM PWs and says a zero sequence number on a non-TDM PW is treated as in order. | error | 1743 (Verified) |
| RA-0237 | 4.2, Appendix | "If the packet sequence number was not zero, then the expected sequence number is set to the packet sequence number plus one." | In Section 4.2 this sentence follows all the cases and so applies to every packet with a non-zero sequence number, including one found "out of order" (outside the window); the non-normative Appendix calls updateExpected() only for in-order and in-window packets and not in processOutOfWindow(). Under the normative text a single stale or forged packet resets the expected number backwards, making all subsequent genuine packets appear out of window. | contradiction | not covered by 1743; **proposed erratum below** |

Proposed erratum RA-0237 (RFC 4385, Section 4.2, Appendix; type: Technical):

```
Original Text
-------------
   If the packet sequence number was not zero, then the expected
   sequence number is set to the packet sequence number plus one.

Corrected Text
--------------
   If the packet was found to be in order or within the allowed
   receive sequence number window, and its sequence number was not
   zero, then the expected sequence number is set to the packet
   sequence number plus one.

Notes
-----
   The Appendix leaves the expected number unchanged for packets
   outside the window; the normative text should say the same.
```

### RFC 4446: IANA Allocations for Pseudowire Edge to Edge Emulation (PWE3) {#ra_rfc4446}

Depth: read (registries). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4447: Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) {#ra_rfc4447}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4448: Encapsulation Methods for Transport of Ethernet over MPLS Networks {#ra_rfc4448}

Depth: deep (Sections 2 to 6; informational Appendices A and B skimmed). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0238 | 4.6 | "Thus, if the source MAC address of an Ethernet frame carried over the PW without a control word present begins with 0x4 or 0x6, it could be mistaken for an IPv4 or IPv6 packet." | An Ethernet frame (preamble and FCS stripped, 4.4) begins with the destination MAC address, so the nibble after the bottom label is the first nibble of the destination address, not the source address. | error | not checked; **proposed erratum below** |
| RA-0239 | 4.4.1, 4.1, 4.2 | "If an Ethernet PW is operating in tagged mode, every frame sent on the PW MUST have a service-delimiting VLAN tag. ... This is the default operating mode.  This is the only REQUIRED mode." | Tagged mode (PW type 0x0004) is the only REQUIRED and the default mode, while raw mode (0x0005) is the one that carries a whole port (4.2) and is the more common deployment; an implementation supporting only raw mode does not conform. The "dummy VLAN tag" to be prepended is not specified (VLAN ID, PRI, TPID), although 4.7 says a default PRI of zero MUST be supported "if an 802.1Q VLAN field is added". | ambiguity | not checked |

Proposed erratum RA-0238 (RFC 4448, Section 4.6; type: Technical):

```
Original Text
-------------
   Thus, if the source MAC address of an Ethernet frame carried over
   the PW without a control word present begins with 0x4 or 0x6, it
   could be mistaken for an IPv4 or IPv6 packet.

Corrected Text
--------------
   Thus, if the destination MAC address of an Ethernet frame carried
   over the PW without a control word present begins with 0x4 or
   0x6, it could be mistaken for an IPv4 or IPv6 packet.

Notes
-----
   The destination MAC address is the first field of the transported
   frame and so immediately follows the label stack when no control
   word is used.
```

### RFC 4623: Pseudowire Emulation Edge-to-Edge (PWE3) Fragmentation and Reassembly {#ra_rfc4623}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4761: Virtual Private LAN Service (VPLS) Using BGP for Auto-Discovery and Signaling {#ra_rfc4761}

Depth: light (normative statements extracted). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4762: Virtual Private LAN Service (VPLS) Using Label Distribution Protocol (LDP) Signaling {#ra_rfc4762}

Depth: deep. Errata: checked (checked: 2 (4144 verified editorial, 4834 held editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0056 | Appendix A | "In a VPLS, we use a VCID (which, when using the PWid FEC, has been substituted with a more general identifier (AGI)" | The PWid FEC (FEC 128) has a PW ID, not a VCID field, and the AGI belongs to the Generalized PWid FEC (FEC 129), not the PWid FEC. Read literally, the sentence mixes the two encodings. | editorial | 4144 (Verified) |

### RFC 5003: Attachment Individual Identifier (AII) Types for Aggregation {#ra_rfc5003}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5085: Pseudowire Virtual Circuit Connectivity Verification (VCCV): A Control Channel for Pseudowires {#ra_rfc5085}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0240 | 5.2.1, 6.2.1 | "Implementations MUST use ICMPv4 [RFC0792] if the signaling for VCCV used IPv4 addresses, or ICMPv6 [RFC4443] if IPv6 addresses were used." | For MPLS PWs the ICMP Ping CV type gives no IP header rules: the L2TPv3 equivalent (6.2.1) fixes the destination and source to the LCCE tunnel endpoint addresses and TTL / Hop Limit to 1, but 5.2.1 says nothing about source, destination or TTL, and "the signaling ... used IPv4 addresses" does not say which addresses (LDP transport address, LSR Id, PW endpoint). Responders cannot know which destination addresses to accept. | ambiguity | not checked |
| RA-0241 | 4, 5.3, 7 | "The decision of the type of VCCV control channel is left completely to the receiving control entity ... The receiver SHOULD choose a single Control Channel Type" | Each PE both sends and receives a label mapping, so each is the "receiving control entity" for the other's advertisement; the text does not say whether the two directions may use different CC Types (Section 7's precedence makes them equal only if both apply it to the same intersection, which "SHOULD" does not guarantee), nor how a PE learns which type the peer "chose" other than by traffic received ("transmitted and replied to", 4). | ambiguity | not checked |
| RA-0242 | 8.1.2, 4 | "IANA has set up a registry of "MPLS VCCV Control Verification Types"." | The registry is for Connectivity Verification (CV) Types; "Control Verification" is a misnomer repeated in the next paragraph. Section 4: "If no capability is signaled, then the peer MUST assume that the peer has no VCCV capability" names the same party twice (the receiving PE assumes the advertising peer has none). | editorial | not checked; **proposed erratum below** |
| RA-0243 | 10 | "For this reason implementations MUST provide a method to secure the data plane." | Security gap: The MUST is met by "providing the ability to architect the MPLS network in such a way that no external MPLS packets can be injected", which is a deployment property, not an implementation method; the requirement is therefore not testable. No authentication of VCCV messages themselves is defined (LSP Ping replies can be forged by anyone able to inject on the PW label). | error | not checked |

Proposed erratum RA-0242 (RFC 5085, Section 8.1.2, 4; type: Editorial):

```
Original Text
-------------
   IANA has set up a registry of "MPLS VCCV Control Verification
   Types".

Corrected Text
--------------
   IANA has set up a registry of "MPLS VCCV Connectivity
   Verification Types".

Notes
-----
   Section 4 and the registry content use "Connectivity Verification
   (CV) Types".
```

### RFC 6073: Segmented Pseudowire {#ra_rfc6073}

Depth: deep (7, 10, 14 in full; 8, 9 by MUST/SHOULD). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0244 | 14.5, 7.4.1 | "0x06     12    L2 PW address of PW Switching Point" | Section 7.4.1 says sub-TLV 0x06 holds the L2 PW address in the RFC 5003 Section 3.2 format, which "includes the AII type field and length, as well as the L2 PW address with the AC ID field set to zero": 1 + 1 + 4 (Global ID) + 4 (Prefix) + 4 (AC ID) = 14 octets, not 12. RFC 7267 Section 6 already states that the length MUST be 14 and that the value 12 in this document is wrong; this document does not carry an Updated-by pointer to it. | contradiction | not checked; **proposed erratum below** |
| RA-0245 | 7.4.1, 7.6 | "The SP-PE TLV MUST contain the appropriate mandatory sub-TLVs specified below." | None of the sub-TLVs that follow is marked mandatory: 0x01 and 0x05 apply only to FEC 128 or FEC 129 segments, the description, local and remote IP address sub-TLVs are "OPTIONAL", and 0x06 is "recommended". Loop detection (7.6) compares the S-PE's "own IP address" with the received TLVs, which only works when each S-PE includes the optional Local IP address sub-TLV (0x03); VCCV to an S-PE (9.5) needs the same. The text therefore requires a set of mandatory sub-TLVs that it never defines. | contradiction | not checked; **proposed erratum below** |
| RA-0246 | 10 | "Only one SP-PE TLV can be present in this message. This message is then relayed by each S-PE unchanged." | The status notification carries the PWid FEC or Generalized ID FEC of the segment it is sent on, and each SS-PW has its own PWid or AII (7.2); item i in the same section says the PWid "is set to the value of the PW segment of the next hop". The message is therefore never relayed unchanged: at least its FEC (and, per 10.1.5 / 10.2, possibly its SP-PE TLV) is rewritten at each S-PE. | contradiction | not checked |
| RA-0247 | 7.2.1 | "The SAII and TAII are compared as unsigned integers; if the SAII is larger, then the T-PE assumes the active role." | For AII Type 2 the identifiers are 12-octet structures (Global ID, Prefix, AC ID) and AII Type 1 is 4 octets; "compared as unsigned integers" does not say whether the AII Type and Length octets take part, how identifiers of different types or lengths compare, or what happens when they are equal. | ambiguity | not checked |

Proposed erratum RA-0244 (RFC 6073, Section 14.5, 7.4.1; type: Technical):

```
Original Text
-------------
   0x06     12    L2 PW address of PW Switching Point

Corrected Text
--------------
   0x06     14    L2 PW address of PW Switching Point

Notes
-----
   Section 7.4.1 includes the AII Type and Length octets with the
   12-octet AII Type 2 value, giving 14; RFC 7267 Section 6 makes
   the same correction normatively.
```

Proposed erratum RA-0245 (RFC 6073, Section 7.4.1, 7.6; type: Technical):

```
Original Text
-------------
   The SP-PE TLV MUST contain the appropriate mandatory sub-TLVs
   specified below.

Corrected Text
--------------
   The SP-PE TLV MUST contain the "Local IP address of PW Switching
   Point" sub-TLV and, for the segment just traversed, either the
   "PWid of last PW segment traversed" (FEC 128) or the "FEC Element
   of last PW segment traversed" (FEC 129) sub-TLV.

Notes
-----
   Every sub-TLV in 7.4.1 is optional or conditional; Section 7.6
   loop detection and Section 9.5 VCCV to S-PEs rely on the Local IP
   address sub-TLV, which is therefore effectively required. The
   proposed text is one possible resolution for the working group.
```

### RFC 6074: Provisioning, Auto-Discovery, and Signaling in Layer 2 Virtual Private Networks (L2VPNs) {#ra_rfc6074}

Depth: deep (3.1.2, 3.2, 4.2, 6, 7 in full; 3.3 to 3.5 by MUST/SHOULD). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0248 | 3.2.3, 3.2.2.1 | "The AGI field in this case consists of a Type of 1, a length field of value 8, and the 8 bytes of the VPLS-id." | The VPLS-id is carried in BGP as an 8-octet Extended Community (type 0x00 or 0x01, sub-type 0x0A, then a 6-octet value), but the AGI is also 8 octets. Whether "the 8 bytes of the VPLS-id" are the Extended Community octets including type and sub-type, or an RD-style encoding of the 6-octet value (2-octet RD type, then AS / IPv4 address and number), is not stated; implementations are known to use the RD-style form, which is not what a literal reading gives. PEs that differ never match each other's Label Mappings. | ambiguity | not checked; **proposed erratum below** |
| RA-0249 | 3.2.2.1 | "If a PE receives a BGP update from which any of the elements specified above is absent, the update should be ignored." | "Ignored" (lower-case "should") is not defined against BGP route handling: if a previous advertisement of the same NLRI was valid, ignoring the update leaves the old route and its PWs in place although the advertiser replaced it; RFC 7606 would instead treat such a route as withdrawn, or keep it but not use it. The text also does not say whether a route reflector, which does not import the route, should still reflect it. | ambiguity | not checked |

Proposed erratum RA-0248 (RFC 6074, Section 3.2.3, 3.2.2.1; type: Technical):

```
Original Text
-------------
   The AGI field in this case consists of a Type of 1, a length
   field of value 8, and the 8 bytes of the VPLS-id.

Corrected Text
--------------
   The AGI field in this case consists of a Type of 1, a length
   field of value 8, and the VPLS-id encoded as a Route
   Distinguisher [RFC4364]: a Two-octet AS Specific Layer 2 VPN
   Identifier is encoded as RD Type 0 with the same Administrator
   and Assigned Number fields, an IPv4 Address Specific one as RD
   Type 1.

Notes
-----
   The Extended Community has 2 octets of type and 6 of value; the
   AGI has 8 octets. The corrected text records the common practice;
   the working group may prefer another mapping, but one needs to be
   stated.
```

### RFC 6391: Flow-Aware Transport of Pseudowires over an MPLS Packet Switched Network {#ra_rfc6391}

Depth: deep (1.3 to 5). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0250 | 1.3, 3 | "On receipt of the PW packet at the egress PE (which knows a flow LSE is present), the flow LSE is discarded without processing." | Section 3 requires the opposite: "If a flow LSE is present, it MUST be checked to determine whether it carries a reserved label. If it is a reserved label, the packet is processed according to the rules associated with that reserved label; otherwise, the LSE is discarded." Section 1.3 also says the ingress MUST NOT use a reserved label as flow label, so the check in Section 3 concerns labels such as the GAL or an entropy-label indicator placed at that position, which "discarded without processing" would drop silently. | contradiction | not checked; **proposed erratum below** |

Proposed erratum RA-0250 (RFC 6391, Section 1.3, 3; type: Technical):

```
Original Text
-------------
   On receipt of the PW packet at the egress PE (which knows a flow
   LSE is present), the flow LSE is discarded without processing.

Corrected Text
--------------
   On receipt of the PW packet at the egress PE (which knows a flow
   LSE is present), the flow LSE is checked as described in Section
   3 and, unless it carries a reserved label, discarded.

Notes
-----
   Section 3: "If a flow LSE is present, it MUST be checked to
   determine whether it carries a reserved label."
```

### RFC 6718: Pseudowire Redundancy {#ra_rfc6718}

Depth: deep (read in full; Informational requirements). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0251 | 4.1 | "Both methods MUST be supported, and signal failure triggers MUST be treated with a lower priority than any local or far-end forced switch or manual trigger." | Placing signal failure below a manual switch inverts the usual protection-switching order, in which a signal failure on the selected path pre-empts a manual switch and only lockout and forced switch outrank it (RFC 6378 Section 3.6 for MPLS-TP linear protection, ITU-T G.808.1). Read literally, a PW kept on a failed path by an operator's earlier manual switch stays there. The same bullet list calls N:1 protection "less efficient ... hence, this SHOULD be supported", a non sequitur. | contradiction | not checked |

### RFC 6870: Pseudowire Preferential Forwarding Status Bit {#ra_rfc6870}

Depth: deep. Errata: checked (checked: 3656 (held, editorial; all "Section 15" references). Updated by RFC 7771, which is not in rfcs/). Updates: RFC 4447.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0057 | 1, 5 | "Section 15 shows in detail how the mechanisms described in this document are used to achieve the desired protection schemes" | There is no section 15; the applications are in Appendix A ("Applications of PW Redundancy Procedures"), the numbering of the draft. Eight references are affected, including the recommendation "it is recommended to use the independent mode of operation as in the application described in Section 15.2" (Appendix A.2). | error | 3656 (Held) |
| RA-0058 | header | "(no RFC text: the RFC Editor page for RFC 6870 states "Updated by RFC 7771")" | RFC 7771 ("Switching Provider Edge (S-PE) Protection for MS-PWs") updates RFC 6870 but is not in rfcs/, so the copy the code is checked against misses its changes to the Preferential Forwarding procedures for MS-PWs. | ambiguity | none |

### RFC 7267: Dynamic Placement of Multi-Segment Pseudowires {#ra_rfc7267}

Depth: read. Errata: no verified errata in the index; page not read. Updates: RFC 6073.

Nothing notable found at this depth.

### RFC 7275: Inter-Chassis Communication Protocol for Layer 2 Virtual Private Network (L2VPN) Provider Edge (PE) Redundancy {#ra_rfc7275}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0252 | 4.2.1, 4.4.2, 4.2 | "CAPREC ... Receive any other ICCP message CAPREC Action: Transmit NAK TLV in RG Notification message" | In CAPREC and CONNECTING, every ICCP message other than an acceptable RG Connect is answered with a NAK, and an RG Notification carrying a NAK is itself "any other ICCP message". Two PEs that are both in CAPREC (for example after one rejected the other's Connect, which per 4.2 makes the sender "stop attempting") therefore answer each other's NAKs with NAKs indefinitely. The application state machine has the same pattern ("Receive any other Application TLV ... Transmit NAK TLV" in RESET, CONNSENT, CONNREC, CONNECTING). The text in 4.2 that a rejected PE stops is not reflected in the tables, which have no "Receive NAK" event at the ICCP level. | contradiction | not checked; **proposed erratum below** |
| RA-0253 | 4.4.2 | "CONNSENT ... Receive Application Connect TLV with A-bit=1 OPERATIONAL ... Receive any other Application TLV RESET Action: Transmit NAK TLV" | When both PEs send their Application Connect (A-bit = 0) at the same time, each is in CONNSENT and receives a Connect with A-bit = 0, which the table treats as "any other Application TLV": both reset and NAK, and after 4.4 ("MUST stop attempting ... until it receives a new Application Connection request") neither retries. The ICCP connection table likewise has no OPERATIONAL entry for a received RG Connect, so a repeated Connect after a restart of the peer's application is undefined. | contradiction | not checked |
| RA-0254 | 4.2.1, 8 | "S-bit ... 0 - The TLV is withdrawing the capability specified by the TLV Code Point." | Section 8 lets a peer withdraw the ICCP capability with a Capability message (S = 0, RFC 5561 dynamic capabilities), but the ICCP Connection state machine has no event for a withdrawn capability: CAPREC, CONNECTING and OPERATIONAL leave only on "LDP session torn down" or an RG Disconnect. Whether a withdrawal takes the RG connections (and their applications) down, and to which state they return, is not specified. | ambiguity | not checked |
| RA-0255 | 6.4.1 | "iii. ICCP Application Connection Count Exceeded (0x00010003) This is used to reject a new incoming Application Connection that would cause the local PE's ICCP connection count to exceed its capabilities." | The code is for the Application Connection count; the text says "ICCP connection count", which is the condition of code ii. | editorial | not checked; **proposed erratum below** |
| RA-0256 | 4.6 | "A PE that requires a separate LDP session will advertise a separate LDP adjacency with a non-zero label space identifier." | The ICCP connection state machine is per LDP session (NONEXISTENT means "no LDP session"); with a dedicated session the text does not say which of the two sessions carries the RG, whether the ICCP capability is advertised on both, or what happens to the RG when only one of them fails. A non-zero label space identifier also denotes a per-interface label space in RFC 5036. | ambiguity | not checked |

Proposed erratum RA-0252 (RFC 7275, Section 4.2.1, 4.4.2, 4.2; type: Technical):

```
Original Text
-------------
   Receive any other ICCP message CAPREC
   Action: Transmit NAK TLV in RG Notification message

Corrected Text
--------------
   Receive RG Notification message CAPREC
   (no action)
   Receive any other ICCP message CAPREC
   Action: Transmit NAK TLV in RG Notification message

Notes
-----
   An RG Notification is an ICCP message, so "any other ICCP
   message" includes the NAK sent in reply; two PEs in CAPREC or
   CONNECTING exchange NAKs without end. The same applies to the
   Application Connection state machine. Section 4.2 says a rejected
   PE stops attempting, but the tables have no event for receiving a
   NAK.
```

Proposed erratum RA-0255 (RFC 7275, Section 6.4.1; type: Editorial):

```
Original Text
-------------
   that would cause the local PE's ICCP connection count to exceed
   its capabilities.

Corrected Text
--------------
   that would cause the local PE's Application Connection count to
   exceed its capabilities.

Notes
-----
   Status code 0x00010003 concerns Application Connections (Section
   4.4 ii); the description repeats the wording of code 0x00010002.
```

### RFC 7338: Requirements and Framework for Point-to-Multipoint Pseudowires over MPLS Packet Switched Networks {#ra_rfc7338}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 7361: LDP Extensions for Optimized MAC Address Withdrawal in a Hierarchical Virtual Private LAN Service (H-VPLS) {#ra_rfc7361}

Depth: deep (5 in full; 3, 6, 7 by MUST/SHOULD). Errata: checked (checked: 1 (4380 verified, technical, 5.2: PBB sub-TLV types 0x0407 / 0x0408 should be 0x01 / 0x02)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0257 | 5.1.1, 5.1.2 | "The U-bit and F-bit [RFC5036] are set to forward if unknown so that potential intermediate VPLS PE-rs devices unaware of the new TLV can just propagate it transparently." | With U = 1 a PE-rs that does not know the TLV ignores it and processes the Address Withdraw with an empty MAC list per RFC 4762, i.e. flushes all MACs except those learned from the sender ("flush-all-but-mine"). For the optimized procedure (N = 1, "flush-all-from-me") that is the complement of the requested action, not a harmless fallback; the document relies on "the assumption ... that the MAC Flush TLV is understood by all devices before it is turned on", but the U-bit choice makes a partial deployment silently do the opposite rather than fail. The rationale given (transparent propagation) does not fit LDP, whose Address Withdraw messages are regenerated per session rather than forwarded. | ambiguity | none found |
| RA-0258 | 5.1.3 | "When optimized MAC flushing is not supported, a MAC Flush TLV is received with N = 0 in the MAC flush message" | A receiver that does not support optimized flushing cannot interpret the TLV at all; the sentence means a TLV received with N = 0 (flush-all-but-mine, the RFC 4762 semantics), whatever the receiver supports. As written it ties the value of N to the receiver's capability. | editorial | none found |

### RFC 8077: Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) {#ra_rfc8077}

Depth: deep. Errata: checked (checked: 1 shown (5243 rejected, technical, 6.1 Group ID example)). Obsoletes: RFC 4447, RFC 6723.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0059 | 6.1 | "... wildcard label withdrawals and status notifications ... to remote PEs upon physical port failure." | The Group ID example names only physical port failure; whether a PE may (or should) use Group-ID wildcards for other shared failures, such as a transport tunnel going down, is left implicit. The erratum asking for it was rejected because the sentence is an example. | ambiguity | 5243 (Rejected) |

### RFC 8338: Signaling Root-Initiated Point-to-Multipoint Pseudowire Using LDP {#ra_rfc8338}

Depth: deep. Errata: not checked. Updates: RFC 7385.

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

## RSVP, RSVP-TE and GMPLS {#ra_rsvp}

44 RFCs in this area (16 deep, 2 part, 17 read, 3 light, 6 scan); 43 findings, 12 of them proposed errata.

### RFC 2205: Resource ReSerVation Protocol (RSVP) -- Version 1 Functional Specification {#ra_rfc2205}

Depth: deep. Errata: checked (checked: 1 (4732 held, editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0061 | A.5 | "Its contents depend upon the Error Type." | "Error Type" is not defined anywhere in the RFC; the field that qualifies Error Value is the Error Code. | editorial | 4732 (Held) |

### RFC 2209: Resource ReSerVation Protocol (RSVP) -- Version 1 Message Processing Rules {#ra_rfc2209}

Depth: read (lightly (informational processing rules). Errata: not checked. 

Nothing notable found at this depth.

### RFC 2210: The Use of RSVP with IETF Integrated Services {#ra_rfc2210}

Depth: deep (Sections 2.3 and 3 read in full; 1, 2, 4 and the appendix skimmed). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0259 | 3.3.6, 3.3.2 | "Words 2-7: Default general characterization parameters / 4   \|  zero extension of ..           IS hop cnt (16-bit unsigned)  \|" | In the complete ADSPEC example the default general parameters fragment occupies words 2 to 10 (header plus the 8 words its own length field gives), not "Words 2-7"; the Guaranteed fragment then correctly starts at word 11. The example also shows IS hop count and composed MTU as zero-extended 16-bit values, while the fragment definition in 3.3.2 gives "IS hop cnt (32-bit unsigned integer)" and "Composed MTU (32-bit unsigned integer)"; RFC 2215 limits the values but the two figures differ on the encoding a receiver must accept. | contradiction | not checked; **proposed erratum below** |
| RA-0260 | 3.3.5 | "(c) - Length of per-service data, two words not including header / (c) - Parameter ID, parameter 6" | In the override example the legend uses "(c)" twice and the figure uses "(d)" for both the parameter ID and the flags, so the labels do not match the fields. Section 3.2.1: "than that value should be used" for "then". | editorial | not checked |

Proposed erratum RA-0259 (RFC 2210, Section 3.3.6, 3.3.2; type: Technical):

```
Original Text
-------------
   Words 2-7: Default general characterization parameters

Corrected Text
--------------
   Words 2-10: Default general characterization parameters

Notes
-----
   The fragment header (word 2) gives a length of 8 words, so it
   ends at word 10; Section 3.3.2 defines the hop count and MTU as
   32-bit unsigned integers.
```

### RFC 2747: RSVP Cryptographic Authentication {#ra_rfc2747}

Depth: deep. Errata: checked (checked: 1 (4313 verified, technical)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0062 | 3.2 | "The remaining 32 bits are filled with the 32 least significant bits of the timestamp." | The example puts the low-order timestamp bits in the high half of the sequence number; the erratum says the 32 most significant bits of the timestamp are meant (the counter supplies the low half). With a timestamp finer than one second the literal text would make sequence numbers repeat or go backwards. | error | 4313 (Verified) |

### RFC 2750: RSVP Extensions for Policy Control {#ra_rfc2750}

Depth: read (normative statements). Errata: not checked. Updates: RFC 2205.

Nothing notable found at this depth.

### RFC 2961: RSVP Refresh Overhead Reduction Extensions {#ra_rfc2961}

Depth: deep. Errata: errata exist; not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0261 | 4.5 | "if ((int) old_id - (int) new_id > 0) { new value is less than old value; }" | The wrap-safe comparison casts each 32-bit identifier to a signed int before subtracting. With 32-bit int the subtraction can overflow (undefined behaviour in C) and for operands on either side of 2^31 gives the wrong sign. The intended serial-number test (RFC 1982 style) is the cast of the difference, (int32_t)(old_id - new_id) > 0, computed on unsigned 32-bit values. | error | not checked; **proposed erratum below** |
| RA-0262 | 4.5 | "When a node is sending a trigger message, the Message_Identifier value MUST have a value that is greater than any other value previously used with the same Epoch / Note that the 32-bit Message_Identifier value MAY wrap." | Once the identifier wraps within one Epoch no new value can be "greater than any other value previously used"; the MUST can only be read as "greater in serial-number arithmetic than the most recent value". The text does not say how far apart in-flight values may be (RFC 1982 requires less than 2^31) nor that the Epoch must change before reuse. | contradiction | not checked |
| RA-0263 | 5.2, 5.3 | "When the use of this method is administratively configured, the destination address should be the well known group address 224.0.0.14. / When the destination address of the message is a multicast address, then identified information is added to the message in a MESSAGE_ID SRC_LIST object" | The secondary (next-hop) method of 5.3 uses MESSAGE_ID LIST / MCAST_LIST objects, and 5.2 says Srefresh sent to the next hop "MUST NOT include any MESSAGE_ID SRC_LIST objects". When configured to send to 224.0.0.14 the destination is a multicast address, which the later 5.3 rule maps to SRC_LIST objects, whose group is "the message's destination IP address" (wrong for 224.0.0.14). Which object types are allowed, whether a Router Alert is carried (5.2 MUST for session destinations, SHOULD NOT for neighbours) and the IPv6 equivalent of 224.0.0.14 are not specified. | contradiction | not checked |
| RA-0264 | 6.3, 4.7 | "/* acknowledged or no reply from receiver for too long: */ do any needed clean up; exit;" | The behaviour after Rl unacknowledged transmissions is not specified: whether the state continues to be refreshed by standard refreshes (implied by 4.7, "followed by standard RSVP refreshes"), whether the neighbour should be treated as no longer refresh-reduction capable, and whether later refreshes of that state may still use Srefresh (whose entries the neighbour may not hold). | ambiguity | not checked |
| RA-0265 | 8, 4.5 | "No new security issues are raised in this document." | Security gap: The out-of-order rule (4.5, "Out of order messages SHOULD be ignored, i.e., silently dropped") lets a forged message with the neighbour's addresses, the current Epoch and a high Message_Identifier cause subsequent genuine triggers to be dropped until the identifier catches up; Srefresh NACKs make the receiver resend full state (a small amplification). Both are mitigated only by the INTEGRITY object [RFC2747], which the security section does not mention. | error | not checked |
| RA-0266 | 4.5, 3.3 | "Rapid retransmission rate MUST be based on the exponential exponential back-off procedures defined in section 6." | Doubled word "exponential exponential". Section 3.3 "exactly one IP datagram, which is approximately 64K bytes" means the maximum IP datagram size. Section 4.1 uses "Only one MESSAGE_ID object MAY be included" as a limit (MUST NOT include more than one); receiver handling of two MESSAGE_ID objects is not stated. | editorial | not checked |

Proposed erratum RA-0261 (RFC 2961, Section 4.5; type: Technical):

```
Original Text
-------------
   if ((int) old_id - (int) new_id > 0) {

Corrected Text
--------------
   if ((int32_t) (old_id - new_id) > 0) {   /* old_id, new_id:
   uint32_t */

Notes
-----
   The expression as printed is not wrap-safe in C; the difference
   of the unsigned values must be computed first and then
   interpreted as signed 32-bit, as in RFC 1982 serial arithmetic.
```

### RFC 3097: RSVP Cryptographic Authentication -- Updated Message Type Value {#ra_rfc3097}

Depth: read. Errata: not checked. Updates: RFC 2747.

Nothing notable found at this depth.

### RFC 3209: RSVP-TE: Extensions to RSVP for LSP Tunnels {#ra_rfc3209}

Depth: deep. Errata: checked (checked: 2 (2669 verified, 4733 held; both editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0063 | 4.3.3.1 | "The path between a loose node and its preceding node MAY include other network nodes that are not part of the strict node or its preceding abstract node." | The paragraph describes a loose node; "strict" inverts the meaning of the ERO check for a loose hop. | editorial | 2669 (Verified) |
| RA-0064 | 4.3.2 | "set of abstract nodes to be traversed." | An explicit route is ordered; "set" suggests otherwise. | editorial | 4733 (Held) |

### RFC 3270: Multi-Protocol Label Switching (MPLS) Support of Differentiated Services {#ra_rfc3270}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 3471: Generalized Multi-Protocol Label Switching (GMPLS) Signaling Functional Description {#ra_rfc3471}

Depth: read (normative statements of 3 to 12). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0267 | 4.2 | "To resolve contention, the node with the higher node ID will win the contention and it MUST issue a PathErr/NOTIFICATION message with a "Routing problem/Label allocation failure" indication." | "Node ID" is not defined (TE Router ID, signalling address, LDP/CR-LDP LSR ID, or the address in the RSVP_HOP), nor how IDs of different address families or lengths compare, so two implementations can each consider themselves the winner. Editorial in the same document: "These bits SHOULD be pass through" (7.1, 8.1), "restarts and losses most of its state" (9.2). | ambiguity | not checked |

### RFC 3472: Generalized Multi-Protocol Label Switching (GMPLS) Signaling Constraint-based Routed Label Distribution Protocol (CR-LDP) Extensions {#ra_rfc3472}

Depth: read (CR-LDP binding, background only). Errata: not checked. 

Nothing notable found at this depth.

### RFC 3473: Generalized Multi-Protocol Label Switching (GMPLS) Signaling Resource ReserVation Protocol-Traffic Engineering (RSVP-TE) Extensions {#ra_rfc3473}

Depth: deep. Errata: checked (checked: 7 (all verified; 3 technical)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0065 | 4.2.1 | "The Notify_Request Class-Number is 195 (of form 11bbbbbb).  The format of a Notify Request is:" | The text gives Class-Num 195 but the object figures put the C-Type value in the Class-Num position; an implementer copying the figure would send the wrong class. | error | 1518 (Verified) |
| RA-0066 | 5.2.1 | "when labels are recorded for bidirectional LSPs, label ERO subobjects" | Labels are recorded in the RRO; "label ERO subobjects" should read "label RRO subobjects". | error | 4585 (Verified) |
| RA-0067 | 2.4 | "Waveband switching uses the same format as the generalized label, see section 2.2." | Wrong cross-reference: waveband switching is section 2.3. | editorial | 4467 (Verified) |

### RFC 3475: Documentation of IANA assignments for Constraint-Based LSP setup using LDP (CR-LDP) Extensions for Automatic Switched Optical Network (ASON) {#ra_rfc3475}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 3477: Signalling Unnumbered Links in Resource ReSerVation Protocol - Traffic Engineering (RSVP-TE) {#ra_rfc3477}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0268 | 4.1 | "The LSR uses this information to find a link with tuple <Router ID, local identifier> matching the tuple <IP Address, Interface ID> carried in the IF_INDEX TLV." | The IF_ID RSVP_HOP carries the upstream node's Router ID and the identifier the upstream node assigned (4.2). In the receiving LSR's terminology of Section 2 that identifier is the "remote identifier"; "local identifier" is correct only from the neighbour's point of view, and the sentence does not say whose Router ID is matched. Read literally against Section 2, the receiver would match its own identifiers. | ambiguity | not checked |
| RA-0269 | 4.1, 7 | "The Error code in the object is set to 24.  The Error value in the object is set to 16." | Error value 16 of Error Code 24 (Routing Problem) is used without a name and is not requested in the IANA Considerations, which cover only the ERO/RRO subobject and the object class (the registry lists it as "Unknown Interface Index" with this RFC as reference). Section 3.1 "a class number of of 193" (doubled word); Section 6 "interface identify" for "interface identifier". | editorial | not checked |

### RFC 3988: Maximum Transmission Unit Signalling Extensions for the Label Distribution Protocol {#ra_rfc3988}

Depth: read (normative statements, TLV format). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4090: Fast Reroute Extensions to RSVP-TE for LSP Tunnels {#ra_rfc4090}

Depth: deep. Errata: checked (checked: 3 (4203, 6203, 6939; all verified, technical)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0068 | 6 | "... the "local protection available", "local protection in use"," | When the PLR may set "local protection available" in the RRO was unclear; the erratum says only once a bypass (or detour) has been chosen and the forwarding state to use it is installed. | ambiguity | 4203 (Verified) |
| RA-0069 | 6 | ""bandwidth protection guaranteed" flag is set, the PLR SHOULD try to" | There is no "bandwidth protection guaranteed" flag; the SESSION_ATTRIBUTE flag is "bandwidth protection desired" (0x08). | error | 6203 (Verified) |
| RA-0070 | 4.4 | "requested, we define two new flags in the RRO IPv4 sub-object." | The two new RRO flags are defined only for the IPv4 subobject; the erratum extends them to the IPv6 subobject. | error | 6939 (Verified) |

### RFC 4105: Requirements for Inter-Area MPLS Traffic Engineering {#ra_rfc4105}

Depth: light (requirements document; normative statements extracted). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4124: Protocol Extensions for Support of Diffserv-aware MPLS Traffic Engineering {#ra_rfc4124}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0270 | 13.2, 6.5, 13.3.5 | "This document defines, in Section 6.5, values 1 through 7 in that name space (see Section 13.3.5)." | Sections 6.5 and 13.3.5 both define eight Error Values (1 to 8) for Error Code 28; value 8 "Inconsistency between signaled PHBs and signaled Class-Type" is omitted from the count in 13.2. | contradiction | not checked; **proposed erratum below** |
| RA-0271 | 6.1, 6.3 | "MUST send a PathErr towards the sender with the error code "Diffserv-aware TE Error" and an error value of "Unexpected CLASSTYPE object" (for a Path that) does not have a session type of LSP_Tunnel_IPv4" | Section 6.1 restricts CLASSTYPE to LSP_TUNNEL_IPv4 sessions and 6.3 mandates error 28/1 for any other session type. Read literally, an RSVP-TE LSP of an LSP_TUNNEL_IPv6 session (RFC 3209 4.6.1.2) or a P2MP session (RFC 4875) cannot carry a Class-Type other than 0. Whether the restriction is intentional or an artefact of the IPv4-only scope of the time is not stated, and no later document lifts it explicitly. | ambiguity | not checked |
| RA-0272 | 6.3 | "determines that the tuple formed by (i) this Class-Type and (ii) the setup priority signaled in the same Path message, is not one of the eight TE-Classes ... MUST send a PathErr ... "CT and setup priority do not form a configured TE-Class"" | The conditions for Error Values 4 and 5 are each stated without excluding the other, so when both setup and holding tuples are unconfigured three MUST clauses (values 4, 5 and 6) apply at once. The intended reading (value 6 only, 4 and 5 when only one tuple fails) has to be inferred. | ambiguity | not checked |
| RA-0273 | 6.2.1, 5.1 | "Class Number = 66 / Class-Type = 1" | The object header label "Class-Type = 1" means C-Type 1 (6.2 says "only one defined C-Type which is C-Type 1"); "Class-Type" is the DS-TE term for CT and is confusing here. Section 5.1 does not bound N in "Bandwidth Constraints (N x 4 octets)" (at most 8 BCs per 4.1.1) nor say how a receiver treats more than 8. | editorial | not checked |

Proposed erratum RA-0270 (RFC 4124, Section 13.2, 6.5, 13.3.5; type: Technical):

```
Original Text
-------------
   This document defines, in Section 6.5, values 1 through 7 in that
   name space (see Section 13.3.5).

Corrected Text
--------------
   This document defines, in Section 6.5, values 1 through 8 in that
   name space (see Section 13.3.5).

Notes
-----
   Sections 6.5 and 13.3.5 list values 1 to 8.
```

### RFC 4125: Maximum Allocation Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering {#ra_rfc4125}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4127: Russian Dolls Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering {#ra_rfc4127}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4206: Label Switched Paths (LSP) Hierarchy with Generalized Multi-Protocol Label Switching (GMPLS) Traffic Engineering (TE) {#ra_rfc4206}

Depth: read (normative statements of 3 to 7). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0274 | 7 | ""Each sender SHOULD have distinct security associations (and keys) per secured sending interface (or LIH). ..." it should read: "Each sender SHOULD have distinct security associations (and keys) per secured receiver's IP address." | Section 7 rewrites the security-association selection rule of RFC 2747 Section 2.1, but the document header does not list RFC 2747 as updated, so a reader of RFC 2747 is not pointed to the change (RFC 5150 Section 6 repeats the same replacement text, also without an Updates header). The rewritten rule is stated for FA-LSPs but its scope ("it should read") is unrestricted, leaving open whether all RSVP-TE implementations must select keys by receiver address. | ambiguity | not checked |

### RFC 4561: Definition of a Record Route Object (RRO) Node-Id Sub-Object {#ra_rfc4561}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4872: RSVP-TE Extensions in Support of End-to-End Generalized Multi-Protocol Label Switching (GMPLS) Recovery {#ra_rfc4872}

Depth: read. Errata: not checked. Updates: RFC 3471.

Nothing notable found at this depth.

### RFC 4873: GMPLS Segment Recovery {#ra_rfc4873}

Depth: read (normative statements of 2 to 9). Errata: not checked. Updates: RFC 3473, RFC 4872.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0275 | 4.3.1 | "o new text: If a message contains multiple NOTIFY_REQUEST objects, only the first object used is in notification." | The replacement text for RFC 3473 is garbled ("only the first object used is in notification"); "only the first object is used in notification" is meant. The replacement also turns RFC 3473's "SHOULD NOT be propagated" into "MUST be propagated in the order received", which changes the behaviour of every RFC 3473 node that sees several NOTIFY_REQUEST objects, not only branch and merge nodes. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0275 (RFC 4873, Section 4.3.1; type: Editorial):

```
Original Text
-------------
   only the first object used is in notification.

Corrected Text
--------------
   only the first object is used in notification.

Notes
-----
   The sentence replaces RFC 3473 text and should read "only the
   first object is used in notification".
```

### RFC 4874: Exclude Routes - Extension to Resource ReserVation Protocol-Traffic Engineering (RSVP-TE) {#ra_rfc4874}

Depth: read (all normative statements of 1.2 to 7). Errata: not checked. Updates: RFC 3209, RFC 3473.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0276 | 3.2, 4.2, 6 | "In this case, the node MUST send a PathErr message with the error code "Routing Error" and error value "XRO Too Complex"." | RSVP has no "Routing Error" error code; the other errors of this document use code 24 "Routing Problem", and the IANA section registers "XRO Too Complex" and "EXRS Too Complex" as values of "Routing Problem". Section 6 item 2 says an unsupported EXRS "MUST be rejected as an unknown ERO subobject as described in Section 4.2", but 4.2 has no such procedure (the unknown-subobject handling is RFC 3209 4.3.4 / 4.3.5). | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0276 (RFC 4874, Section 3.2, 4.2, 6; type: Editorial):

```
Original Text
-------------
   the node MUST send a PathErr message with the error code "Routing
   Error" and error value "XRO Too Complex".

Corrected Text
--------------
   the node MUST send a PathErr message with the error code "Routing
   Problem" and error value "XRO Too Complex".

Notes
-----
   The same correction applies to "EXRS Too Complex" in Section 4.2;
   Section 6 should refer to [RFC3209] for unknown ERO subobjects.
```

### RFC 4875: Extensions to Resource Reservation Protocol - Traffic Engineering (RSVP-TE) for Point-to-Multipoint TE Label Switched Paths (LSPs) {#ra_rfc4875}

Depth: deep. Errata: checked (checked: 15 records (2 verified, 10 held, 3 rejected; 1 held technical)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0071 | 8.2 | "If the Sub-Group Originator ID is its own address, then it MUST set the receiver address in the RESV_CONFIRM object to this address, else it MUST propagate the object unchanged." | The second paragraph of 8.2 is an earlier version of the third: it omits the merge case, where the third paragraph says the LSR MUST put its own Router ID in RESV_CONFIRM when it merges several Resvs carrying one. Read together they give two different MUSTs for a merging transit LSR. | contradiction | 2485 (Held) |
| RA-0072 | 17 | "section 24, PE1 can set up a P2P LSP to P1 and use that as a LSP" | "Figure 2 in section 24" should be "Figure 2 in Appendix A"; section 24 is not in the document. Erratum 2483 corrects a similar wrong reference in 6.1 (4.1 for 5.1). | editorial | 2490 (Verified) |

### RFC 5063: Extensions to GMPLS Resource Reservation Protocol (RSVP) Graceful Restart {#ra_rfc5063}

Depth: deep. Errata: not checked. Updates: RFC 2961, RFC 3473.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0277 | 5.3.1, 4.2 | "Received Path state containing a MESSAGE_ID object whose Epoch value matches the Epoch received in the most recent Hello message is considered as updated after the upstream neighbor has restarted." | Hello messages carry no Epoch: the Hello grammar of Section 4.2 is <Common Header> [<INTEGRITY>] <HELLO> [<RESTART_CAP>] [<CAPABILITY>], and the Epoch of RFC 2961 is carried only in MESSAGE_ID objects of other messages. The rule for excluding already-updated Path state from RecoveryPath Srefresh messages therefore refers to a value the downstream neighbour does not have; the intended reference is presumably the Epoch of the MESSAGE_ID objects received from the restarted neighbour after its restart. | contradiction | not checked; **proposed erratum below** |
| RA-0278 | 1, 4.5.1 | "the downstream RSVP neighbor MUST send a RecoveryPath message for each LSP associated with the restarting node for which it has sent a Resv message." | The Introduction says a RecoveryPath is sent "for every Path message it has previously received from the restarting node"; 4.5.1 restricts it to LSPs for which a Resv was sent. LSPs whose Path was received but whose Resv was not yet sent (setup in progress at the restart) are covered by one text and not the other. Section 4.5.2.3 also says unresynchronised Path messages with a Recovery_Label "MUST be treated as being received during the Recovery Period" at its end, which reads as the opposite of the intended "as received after it" (i.e. as new setups per RFC 3473). | ambiguity | not checked |
| RA-0279 | 5.1, 8 | "A new bit within the existing Flags field of each object is defined.  ... 0x02: RecoveryPath Flag" | The new flag in the MESSAGE_ID_ACK, MESSAGE_ID_NACK and MESSAGE_ID_LIST objects (fields RFC 2961 defines as "MUST be zero on transmission and ignored on receipt") is not mentioned in the IANA Considerations and no registry is created for these flag fields; 4.4.1 also calls the R bit both "RecoveryPath Desired" and "RecoveryPath Receive Desired". | editorial | not checked |

Proposed erratum RA-0277 (RFC 5063, Section 5.3.1, 4.2; type: Technical):

```
Original Text
-------------
   Received Path state containing a MESSAGE_ID object whose Epoch
   value matches the Epoch received in the most recent Hello message
   is considered as updated after the upstream neighbor has
   restarted.

Corrected Text
--------------
   Received Path state containing a MESSAGE_ID object whose Epoch
   value matches the Epoch received from the restarted neighbor in
   any MESSAGE_ID object since the restart was detected is
   considered as updated after the upstream neighbor has restarted.

Notes
-----
   Per RFC 2961 the Epoch is carried in MESSAGE_ID objects; the
   Hello format in Section 4.2 has none.
```

### RFC 5150: Label Switched Path Stitching with Generalized Multiprotocol Label Switching Traffic Engineering (GMPLS TE) {#ra_rfc5150}

Depth: read (normative statements of 3 to 6). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5151: Inter-Domain MPLS and GMPLS Traffic Engineering -- Resource Reservation Protocol-Traffic Engineering (RSVP-TE) Extensions {#ra_rfc5151}

Depth: deep. Errata: not checked. Updates: RFC 3209, RFC 3473.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0280 | 9.1 | "4     Contiguous LSP         Yes          No           Yes   [RFC5150]" | The "Contiguous LSP" attribute flag is defined in Section 4.1 of this document (RFC 5151); the IANA table gives RFC 5150 (LSP stitching), which defines the different "LSP stitching desired" flag. | error | not checked; **proposed erratum below** |
| RA-0281 | 2, 4.1 | "must in any case support contiguous inter-domain TE LSPs since this is the default mode of operation for RSVP-TE / recognizes the "Contiguous LSP" bit, but cannot support contiguous TE LSPs, MUST send a Path Error message with an error code "Routing Problem"/"Contiguous LSP type not supported"" | Section 2 says a domain border LSR must always support contiguous LSPs, and 4.1 says domain border LSRs "MUST support and act on" the flag, yet 4.1 defines an error for a node that recognises the bit but "cannot support contiguous TE LSPs". The only consistent reading is "is not permitted by policy to signal contiguous LSPs", which the text does not say; it is also not said whether policy refusal should use this error or 2/103 "Inter-domain policy failure". | contradiction | not checked |
| RA-0282 | 3, 8 | "3.  Carry out ERO procedures as described in Section 3 in addition to the procedures in [RFC3209] and [RFC3473]." | The ERO rules are in Section 3.1 (the step is itself inside Section 3). Section 8 A): "The domain border LSR can make implement this policy" (stray "make"). | editorial | not checked |

Proposed erratum RA-0280 (RFC 5151, Section 9.1; type: Technical):

```
Original Text
-------------
   4     Contiguous LSP         Yes          No           Yes
   [RFC5150]

Corrected Text
--------------
   4     Contiguous LSP         Yes          No           Yes
   [RFC5151]

Notes
-----
   The flag is defined in Section 4.1 of RFC 5151; RFC 5150 defines
   the LSP stitching flags.
```

### RFC 5152: A Per-Domain Path Computation Method for Establishing Inter-Domain Traffic Engineering (TE) Label Switched Paths (LSPs) {#ra_rfc5152}

Depth: read (normative statements of 4 to 7). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5284: User-Defined Errors for RSVP {#ra_rfc5284}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5420: Encoding of Attributes for MPLS LSP Establishment Using Resource Reservation Protocol Traffic Engineering (RSVP-TE) {#ra_rfc5420}

Depth: deep. Errata: not checked. Obsoletes: RFC 4420. Updates: RFC 3209, RFC 3473.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0283 | 5, 9 | "each transit LSR MUST examine the attributes in the LSP_REQUIRED_ATTRIBUTES object and MUST NOT forward the object without acting on its contents. / Subsequent instances of these objects within a Path message SHOULD be ignored and MUST be forwarded unchanged." | Section 9 applies to both objects: a second LSP_REQUIRED_ATTRIBUTES object is to be ignored and forwarded unchanged, which Section 5 forbids (no forwarding without acting on the contents). A second instance can therefore carry required attributes that some transit LSRs silently pass on without examination, defeating the purpose of the 0bbbbbbb C-Num. | contradiction | not checked; **proposed erratum below** |
| RA-0284 | 3, 14 | "Prior to the change, the Length field indicated the length of the Value field only.  After the change ... the Length field indicates the length of the whole TLV." | The Length semantics changed incompatibly from RFC 4420 without a new C-Type or any means of detection; a receiver cannot tell an RFC 4420 encoding (for the 4-octet Attribute Flags TLV, Length 4) from an RFC 5420 one (Length 8) except by heuristics. The document gives no guidance on handling a Length that does not fit the object (e.g., Length less than 4 or larger than the remaining object). | ambiguity | not checked |
| RA-0285 | 7.3.2, 7.2 | "To report non-compliance, an LSR MAY clear the corresponding bit in the Attributes subobject." | The Attributes subobject is pushed by the reporting LSR itself with all bits defaulting to zero (7.3.4), so "clear" has no effect; the intended statement is that the LSR leaves the bit clear. Section 7.2 states the length constraints in lower case ("must be a multiple of four and must be at least eight") without saying how a receiver treats a violating subobject. | editorial | not checked |

Proposed erratum RA-0283 (RFC 5420, Section 5, 9; type: Technical):

```
Original Text
-------------
   Subsequent instances of these objects within a Path message
   SHOULD be ignored and MUST be forwarded unchanged.

Corrected Text
--------------
   Subsequent instances of the LSP_ATTRIBUTES object within a Path
   message SHOULD be ignored and MUST be forwarded unchanged.  A
   Path message containing more than one LSP_REQUIRED_ATTRIBUTES
   object SHOULD be rejected.

Notes
-----
   Forwarding an unexamined LSP_REQUIRED_ATTRIBUTES instance
   contradicts Section 5.
```

### RFC 5495: Description of the Resource Reservation Protocol - Traffic-Engineered (RSVP-TE) Graceful Restart Procedures {#ra_rfc5495}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 5712: MPLS Traffic Engineering Soft Preemption {#ra_rfc5712}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6107: Procedures for Dynamically Signaled Hierarchical Label Switched Paths {#ra_rfc6107}

Depth: read (normative lines; 3.5, 3.6 in full). Errata: errata exist; not read. Updates: RFC 3477, RFC 4206.

Nothing notable found at this depth.

### RFC 7570: Label Switched Path (LSP) Attribute in the Explicit Route Object (ERO) {#ra_rfc7570}

Depth: deep (Sections 2 to 3.2.3 read; IANA and security not read). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0286 | 2.1 | "The size of the ERO subobject limits the size of the Hop Attributes TLV to 250 bytes." | An ERO subobject Length is 8 bits and (RFC 3209 4.3.3) a multiple of 4, so its maximum is 252 octets; after the 4-octet subobject header (L/Type, Length, Reserved and R bit) at most 248 octets remain for Hop Attributes TLVs (each with its own 4-octet RFC 5420 header). 250 is not reachable. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0286 (RFC 7570, Section 2.1; type: Technical):

```
Original Text
-------------
   The size of the ERO subobject limits the size of the Hop
   Attributes TLV to 250 bytes.

Corrected Text
--------------
   The size of the ERO subobject limits the total size of the Hop
   Attributes TLVs to 248 bytes.

Notes
-----
   Maximum subobject length 252 (multiple of 4, at most 255) minus
   the 4-octet subobject header.
```

### RFC 8169: Residence Time Measurement in MPLS Networks {#ra_rfc8169}

Depth: part. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0287 | 3.1 | "The Length field of the PTP sub-TLV contains the number of octets of the Value part of the TLV and MUST be 20. / The 10-octet-long Port ID field contains the identity of the source port." | The sizes do not add up. The Value as described is Flags + PTPType (4 octets) + Port ID (10 octets, the IEEE 1588 portIdentity) + Sequence ID (2 octets) = 16 octets, not 20; 20 is the value length plus the 4-octet Type / Length header, which the sentence explicitly excludes. Figure 2 in turn draws Port ID over one and a half rows (6 octets), giving a 12-octet value. Text, figure and Length value are mutually inconsistent, so two implementations can build different PTP sub-TLVs and reject each other's RTM messages. | error | none found; **proposed erratum below** |
| RA-0288 | 4.4.1 | "\|     Type      \|     Length    \|I\|         Reserved            \| / Type value (5) has been assigned by IANA in the RSVP-TE "Attributes TLV Space" sub-registry" | TLVs in the LSP_ATTRIBUTES "Attributes TLV Space" use the RFC 5420 format with a 16-bit Type and a 16-bit Length; Figure 7 draws an 8-bit Type and an 8-bit Length. A parser following RFC 5420 and one following Figure 7 disagree on where the I bit and the sub-TLVs start. In addition, the I bit is a field of the single RTM_SET TLV (only one is allowed per object), but the procedure sets it in "the node's RTM_SET TLV" at each hop, so each node overwrites the indication of the nodes downstream unless the rule is read as "set if any node set it", which is not stated. Figure 10 is captioned "IPv4 Sub-TLV Format" for the unnumbered sub-TLV. | contradiction | none found; **proposed erratum below** |

Proposed erratum RA-0287 (RFC 8169, Section 3.1; type: Technical):

```
Original Text
-------------
   The Length field of the PTP sub-TLV contains the number of octets
   of the Value part of the TLV and MUST be 20.

Corrected Text
--------------
   The Length field of the PTP sub-TLV contains the number of octets
   of the Value part of the TLV and MUST be 16.  (Figure 2 to be
   redrawn with a 10-octet Port ID.)

Notes
-----
   With a 10-octet Port ID as stated in the text and in IEEE 1588
   (portIdentity), the Value is 16 octets; 20 would include the Type
   and Length fields, which the definition of Length excludes.
```

Proposed erratum RA-0288 (RFC 8169, Section 4.4.1; type: Technical):

```
Original Text
-------------
   |     Type      |     Length    |I|         Reserved            |

Corrected Text
--------------
   |             Type              |             Length            |

    |I|                        Reserved                         |
   (16-bit Type and Length as in RFC 5420; and: "a node that sets
   the TTL to 255 MUST set the I flag; a node MUST NOT clear an I
   flag that is already set")

Notes
-----
   RFC 5420 defines Attributes TLVs with 16-bit Type and Length
   fields; the IANA registry for type 5 is that space.
```

### RFC 8271: Updates to the Resource Reservation Protocol for Fast Reroute of Traffic Engineering GMPLS Label Switched Paths (LSPs) {#ra_rfc8271}

Depth: part. Errata: not checked. Updates: RFC 4090.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0289 | 7.2 | "New Error Code "FRR Bypass Assignment Error" (value 44) and its sub-codes are defined for the ERROR_SPEC Object (C-Type 6) [RFC2205]" | ERROR_SPEC C-Type 6 is the IPv4 IF_ID ERROR_SPEC of RFC 3473 (RFC 2205 defines only C-Types 1 and 2). Naming a single IPv4 C-Type also leaves the IPv6 case (C-Type 7, needed when the BYPASS_ASSIGNMENT IPv6 subobject of Section 7.1 is used) without a defined object. Sub-code 0 ("Bypass Assignment Cannot Be Used") is also used as a real value, while many RSVP error codes treat 0 as "unspecified". | error | not checked; **proposed erratum below** |

Proposed erratum RA-0289 (RFC 8271, Section 7.2; type: Technical):

```
Original Text
-------------
   are defined for the ERROR_SPEC Object (C-Type 6) [RFC2205] in
   this document

Corrected Text
--------------
   are defined for the ERROR_SPEC Object (IPv4 IF_ID ERROR_SPEC,
   C-Type 6, or IPv6 IF_ID ERROR_SPEC, C-Type 7) [RFC3473] in this
   document

Notes
-----
   The IF_ID ERROR_SPEC C-Types 6 and 7 are defined in RFC 3473
   Section 8.2, not in RFC 2205.
```

### Other RFCs in this area {#ra_rsvp_other}

Mechanical checks only, no finding: RFC 2211 (Specification of the Controlled-Load Network Element Service), RFC 2212 (Specification of Guaranteed Quality of Service), RFC 3175 (Aggregation of RSVP for IPv4 and IPv6 Reservations), RFC 4126 (Max Allocation with Reservation Bandwidth Constraints Model for Diffse), RFC 4726 (A Framework for Inter-Domain Multiprotocol Label Switching Traffic Eng), RFC 4920 (Crankback Signaling Extensions for MPLS and GMPLS RSVP-TE).

## PCEP and PCE {#ra_pcep}

36 RFCs in this area (26 deep, 2 part, 1 read, 6 light, 1 scan); 85 findings, 35 of them proposed errata.

### RFC 5088: OSPF Protocol Extensions for Path Computation Element (PCE) Discovery {#ra_rfc5088}

Depth: scan (mechanical checks only). Errata: not checked. 

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

Depth: deep. Errata: checked (checked: 6 (2 verified technical, 2 verified editorial, 2 held editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0074 | 5 | "All PCEP messages MUST be sent using the registered TCP port for the source and destination TCP port." | Read literally a PCC could not use an ephemeral source port, and two sessions between the same pair could not coexist. The erratum: the PCE MUST listen on 4189; the PCC SHOULD use it as source but MAY use an ephemeral port. A PCE must therefore not reject connections from ports other than 4189. | error | 2940 (Verified) |
| RA-0075 | 10.7.1 | "The PCE SHOULD NOT allow parallel TCP connections from the same PCC on the PCEP-registered port." | Section 10.7.1 weakens to SHOULD / SHOULD NOT what sections 5 and 4.2.1 make MUST; the erratum makes both MUST. | contradiction | 2941 (Verified) |
| RA-0076 | 6.9 | "send a PCErr message with Error-value=2 (capability not supported)." | "Error-value=2" is written where Error-Type 2 ("Capability not supported") is meant; there is no Error-value 2 without a type. | editorial | 4427 (Held) |

### RFC 5441: A Backward-Recursive PCE-Based Computation (BRPC) Procedure to Compute Shortest Constrained Inter-Domain Traffic Engineering Label Switched {#ra_rfc5441}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0290 | 12, 15.3 | "Bit number     Name Flag / 28           BRPC path computation chain unavailable / Bit number  Meaning ... 4        BRPC path computation chain unavailable" | Section 12 assigns bit 28 of the NO-PATH-VECTOR TLV flags; the IANA section lists bit 4 for the same flag. RFC 5440 numbers NO-PATH-VECTOR bits from the most significant bit (0) and the IANA registry records 28, so "4" in 15.3 is wrong (it is 32 - 28 counted from the least significant end). | contradiction | not checked; **proposed erratum below** |
| RA-0291 | 12 | "the PCE MUST send a negative path computation reply to the requester using a PCReq message as specified in [RFC5440] that contains a NO-PATH object." | A negative reply carrying NO-PATH is a PCRep; PCReq is the request message. | error | not checked; **proposed erratum below** |
| RA-0292 | 9, 15.2 | "as stated in [RFC5440], the PCE sends a PCErr message to the upstream PCE with an Error-Type=4 (Not supported object), Error-value=4 (Unsupported parameter). ... The corresponding path computation request is then cancelled by the PCE without further notification." | Error-value 4 of Error-Type 4 is defined by this document (15.2), not by RFC 5440, so "as stated in [RFC5440]" applies only to the procedure. For this case the text does not say whether the upstream PCE relays the PCErr to the PCC (the next paragraph's "The PCErr message MUST be relayed" follows the 13/1 case only), nor whether the upstream PCE may retry another downstream PCE. | ambiguity | not checked |
| RA-0293 | 5, 6 | "path segments computed by a downstream PCE ... MUST be provided along with their respective path costs, the C flag of the METRIC object carried within the PCReq message MUST be set." | Section 6 encodes the VSPT as "a non-ordered list of Explicit Route Objects" without saying where each segment's cost goes (a METRIC object after each ERO in the RFC 5440 <path> grammar is implied), which metric type is used when the PCReq has no METRIC object, and whether a PCE may add a METRIC object the PCC did not ask for. | ambiguity | not checked |

Proposed erratum RA-0290 (RFC 5441, Section 12, 15.3; type: Technical):

```
Original Text
-------------
   Bit number  Meaning                  Reference
   4        BRPC path computation chain unavailable

Corrected Text
--------------
   Bit number  Meaning                  Reference
   28       BRPC path computation chain unavailable

Notes
-----
   Bit numbering of the NO-PATH-VECTOR TLV follows RFC 5440 (bit 0 =
   most significant). Section 12 and the IANA registry use 28.
```

Proposed erratum RA-0291 (RFC 5441, Section 12; type: Technical):

```
Original Text
-------------
   the PCE MUST send a negative path computation reply to the
   requester using a PCReq message as specified in [RFC5440] that
   contains a NO-PATH object.

Corrected Text
--------------
   the PCE MUST send a negative path computation reply to the
   requester using a PCRep message as specified in [RFC5440] that
   contains a NO-PATH object.

Notes
-----
   The NO-PATH object is carried in PCRep (RFC 5440 7.5).
```

### RFC 5520: Preserving Topology Confidentiality in Inter-Domain Path Computation Using a Path-Key-Based Mechanism {#ra_rfc5520}

Depth: light. Errata: errata exist; not read. 

Nothing notable found at this depth.

### RFC 5521: Extensions to the Path Computation Element Communication Protocol (PCEP) for Route Exclusions {#ra_rfc5521}

Depth: light. Errata: errata exist; not read. 

Nothing notable found at this depth.

### RFC 5541: Encoding of Objective Functions in the Path Computation Element Communication Protocol (PCEP) {#ra_rfc5541}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0294 | 3.1.1 | "If the objective function is unknown/unsupported and the P bit is set, the PCE MUST send a PCErr message with error type 3 or 4 (Unknown / Not supported object) and error value 4 (Unrecognized/Unsupported parameter)" | In RFC 5440 (Section 9.12) Error-type 3 "Unknown Object" has only Error-values 1 and 2; Error-value 4 "Unsupported parameter" exists only under Error-type 4 "Not supported object". "Error type 3 ... error value 4" is therefore not a registered combination, and an unknown objective function code in a known OF object is not an unknown object. Only 4/4 is valid here. | error | not checked; **proposed erratum below** |
| RA-0295 | 3.3.1, 6.2.3 | "it MUST send a PCErr message with the PCEP error code "policy-violation" (type 5) and a new error value, "objective function indication not allowed"" | The IANA table registers this value as Error-value 4 "OF bit of the RP object set (request rejected)"; the procedure text and the registry use different names for the same code, and the procedure does not give the number. | editorial | not checked |
| RA-0296 | 3.3 | "When set in a PCReq message, this indicates that the PCE MUST provide the applied objective function (should a path satisfying the constraints be found) in the PCRep message." | The flag definition limits the obligation to replies with a path, while Section 3.2 says "The OF object MAY be associated to a negative reply" and 3.3.1 makes inclusion a MUST whenever policy permits, without the found-path condition. Whether a NO-PATH reply to a request with the OF flag must carry an OF object is left open. | ambiguity | not checked |

Proposed erratum RA-0294 (RFC 5541, Section 3.1.1; type: Technical):

```
Original Text
-------------
   the PCE MUST send a PCErr message with error type 3 or 4 (Unknown
   Not supported object) and error value 4 (Unrecognized/Unsupported
   parameter)

Corrected Text
--------------
   the PCE MUST send a PCErr message with error type 4 (Not
   supported object) and error value 4 (Unsupported parameter)

Notes
-----
   RFC 5440 Section 9.12 defines Error-type 3 values 1-2 and
   Error-type 4 values 1-4 (4 = Unsupported parameter). The OF
   object itself is known in this case; only its OF Code is
   unsupported.
```

### RFC 5886: A Set of Monitoring Tools for Path Computation Element (PCE)-Based Architecture {#ra_rfc5886}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6805: The Application of the Path Computation Element Architecture to the Determination of a Sequence of Domains in MPLS and GMPLS {#ra_rfc6805}

Depth: read. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 7897: Domain Subobjects for the Path Computation Element Communication Protocol (PCEP) {#ra_rfc7897}

Depth: part. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8231: Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE {#ra_rfc8231}

Depth: deep. Errata: checked (checked: 8 (4 verified technical, 2 verified editorial, 1 held technical, 1 rejected technical)). 

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

### RFC 8232: Optimizations of Label Switched Path State Synchronization Procedures for a Stateful PCE {#ra_rfc8232}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0297 | 3.2, 4.2 | "If State Synchronization is required, then prior to completing the initialization phase, the PCE MUST mark any LSPs in the LSP-DB that were previously reported by the PCC as stale. / (Expect delta sync) (DO NOT purge LSP state)" | Section 3.2 requires stale marking and a purge at the end-of-synchronization marker whenever synchronization is required, which would delete every unchanged LSP after an incremental synchronization (Section 4.2), where only changed LSPs are reported. Section 4.2 contradicts it only in Figure 7 ("DO NOT purge LSP state"). Section 4.2 also says deleted LSPs are "reported as part of incremental synchronization" without saying how (presumably a PCRpt with the R flag, RFC 8231 7.3). | contradiction | none found; **proposed erratum below** |
| RA-0298 | 5.2, 6.2 | "The PCUpd message SHOULD include an empty Explicit Route Object (ERO) (with no ERO sub-object and object length of 4) / The PCUpd message MUST include an empty ERO" | The same message (PCUpd, PLSP-ID 0, SYNC set) is required to carry an empty ERO in Section 6.2 but only recommended to in Section 5.2. The RFC 8231 PCUpd grammar requires a <path> (intended path) in every update request, so the ERO is mandatory in both cases. | contradiction | none found; **proposed erratum below** |
| RA-0299 | 5.2, 3.2 | "If the PCE receives a PCRpt message before the PCE has triggered the State Synchronization, the PCE MUST send a PCErr with Error-type=20 and Error-value=3" | When F is negotiated and the LSP-DB versions match, synchronization is skipped (Section 3.2) and the PCE never sends a trigger, so a regular report after session start would literally be "before the PCE has triggered" it. The text also does not say whether the session is closed after 20/3, and what a PCE that advertised F but not T does with a later PCE-triggered resynchronization request (both use PLSP-ID 0 with SYNC set). | ambiguity | none found |
| RA-0300 | 3.2 | "The LSP-DB Version Number MUST start at 1 and may wrap around.  Values 0 and 0xFFFFFFFFFFFFFFFF are reserved." | The wrap rule does not say that the reserved values are skipped (0xFFFFFFFFFFFFFFFE to 1), and Figure 3 shows both speakers including LSP-DB-VERSION in the Open with S = 0, although without S no version is ever reported on PCRpt and the PCE's value ("the last LSP-DB Version Number received on an LSP State Report") is undefined. | ambiguity | none found |
| RA-0301 | 9.1 | "the operator SHOULD be to be allowed to trigger the resynchronization procedures" | Garbled sentence ("SHOULD be to be allowed"); intended "the operator SHOULD be allowed". | editorial | none found |

Proposed erratum RA-0297 (RFC 8232, Section 3.2, 4.2; type: Technical):

```
Original Text
-------------
   If State Synchronization is required, then prior to completing
   the initialization phase, the PCE MUST mark any LSPs in the
   LSP-DB that were previously reported by the PCC as stale.

Corrected Text
--------------
   If full State Synchronization is required, then prior to
   completing the initialization phase, the PCE MUST mark any LSPs
   in the LSP-DB that were previously reported by the PCC as stale.
   (Section 4.2:) During incremental State Synchronization, LSPs are
   not marked stale; an LSP deleted at the PCC is reported in a
   PCRpt with the R flag set [RFC8231].

Notes
-----
   Only Figure 7 states that the PCE does not purge during
   incremental synchronization; the normative text of Section 3.2
   says the opposite. The encoding of deletions during incremental
   synchronization is not specified.
```

Proposed erratum RA-0298 (RFC 8232, Section 5.2, 6.2; type: Technical):

```
Original Text
-------------
   The PCUpd message SHOULD include an empty Explicit Route Object
   (ERO) (with no ERO sub-object and object length of 4) as its
   intended path

Corrected Text
--------------
   The PCUpd message MUST include an empty Explicit Route Object
   (ERO) (with no ERO sub-object and object length of 4) as its
   intended path

Notes
-----
   RFC 8231 Section 6.2 requires the intended path in a PCUpd; the
   trigger messages of Sections 5.2 and 6.2 are identical.
```

### RFC 8233: Extensions to the Path Computation Element Communication Protocol (PCEP) to Compute Service-Aware Label Switched Paths (LSPs) {#ra_rfc8233}

Depth: deep. Errata: checked (checked: 1 (5389 held, editorial, 3.1 METRIC flags)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0302 | 3.1 | "comprising metric-value and metric-type (T field), and a flags field, comprising a number of bit flags (B bit and P bit)." | The METRIC object flags of RFC 5440 7.8 are B (bound) and C (computed); P is a common-header flag. Held as erratum 5389. | editorial | 5389 (Held) |
| RA-0303 | 3.1.5.1 | "Additionally, the PCE MAY insert a second METRIC object with B=1, T=14, metric-value=computed path loss." | RFC 5440 7.8 requires the B flag to be cleared in a METRIC object that reports a computed metric in a PCRep ("the B flag MUST be cleared"). The example sets B=1 in the reply. It also gives the request's first METRIC "metric-value=0x0000" (two octets for a 32-bit field). | contradiction | none found; **proposed erratum below** |
| RA-0304 | 3.2.2, 3.2.3, 7.3 | "3.2.2.  Link Reserved Bandwidth Utilization (LRBU) / Type 2 is LRBU (Link Residual Bandwidth Utilization)" | The same quantity is called "Link Reserved Bandwidth Utilization" in Section 3.2.2 (and is defined from reserved bandwidth) and "Link Residual Bandwidth Utilization" in Section 3.2.3 and in the IANA registry (Section 7.3). "Residual" names a different TE quantity (RFC 7810 / RFC 8570 Residual Bandwidth). | editorial | none found; **proposed erratum below** |
| RA-0305 | 6.2, 3.2.3.1 | "If the bandwidth utilization percentage of any of the links in the path changes to a value less than that required when the path was set up" | The BU object is an upper limit (Section 3.2.3.1: no link may exceed the given value), so degradation is a utilization that rises above the limit, not one that falls below it. As written, the reoptimisation trigger is inverted. | error | none found; **proposed erratum below** |
| RA-0306 | 5.2 | "<PCRep Message> ::= <Common Header> [<svec-list>] <response-list>" | The PCRep grammar adds an <svec-list> that neither RFC 5440 nor RFC 8231 (the stated bases) have in a PCRep; the text gives no semantics for an SVEC in a reply. A receiver following RFC 5440 treats an SVEC in a PCRep as unexpected. | ambiguity | none found |

Proposed erratum RA-0303 (RFC 8233, Section 3.1.5.1; type: Technical):

```
Original Text
-------------
   Additionally, the PCE MAY insert a second METRIC object with B=1,
   T=14, metric-value=computed path loss.

Corrected Text
--------------
   Additionally, the PCE MAY insert a second METRIC object with B=0,
   T=14, metric-value=computed path loss.

Notes
-----
   Per RFC 5440 Section 7.8, a METRIC object reporting the computed
   path metric in a PCRep has the B flag cleared.
```

Proposed erratum RA-0304 (RFC 8233, Section 3.2.2, 3.2.3, 7.3; type: Editorial):

```
Original Text
-------------
   *  Type 2 is LRBU (Link Residual Bandwidth Utilization)

Corrected Text
--------------
   *  Type 2 is LRBU (Link Reserved Bandwidth Utilization)

Notes
-----
   Section 3.2.2 defines LRBU from reserved bandwidth; the expansion
   in Section 3.2.3 and in the IANA "BU Object Type Field" registry
   should match.
```

Proposed erratum RA-0305 (RFC 8233, Section 6.2, 3.2.3.1; type: Technical):

```
Original Text
-------------
   If the bandwidth utilization percentage of any of the links in
   the path changes to a value less than that required when the path
   was set up, or otherwise less than an implementation-specific
   threshold,

Corrected Text
--------------
   If the bandwidth utilization percentage of any of the links in
   the path changes to a value greater than that required when the
   path was set up, or otherwise greater than an
   implementation-specific threshold,

Notes
-----
   Section 3.2.3 defines the BU value as "the upper limit of the
   acceptable link bandwidth utilization percentage".
```

### RFC 8253: PCEPS: Usage of TLS to Provide a Secure Transport for the Path Computation Element Communication Protocol (PCEP) {#ra_rfc8253}

Depth: deep. Errata: checked (checked: 1 (5180 held, editorial)). Updates: RFC 5440.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0082 | 3.4 | "of the TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 [RFC6460] and" | RFC 6460 (Suite B profile) does not define these cipher suites; RFC 5289 does. | editorial | 5180 (Held) |

### RFC 8281: Path Computation Element Communication Protocol (PCEP) Extensions for PCE-Initiated LSP Setup in a Stateful PCE Model {#ra_rfc8281}

Depth: deep. Errata: checked (checked: 1 shown (6301 verified, technical, grammar)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0083 | 5.1, 6 | "<PCE-initiated-lsp-deletion> ::= <SRP>" | The deletion production (SRP and LSP only) is also used for the delegation-reclaim request of section 6, which may carry more objects; the erratum renames it <PCE-initiated-lsp-deletion-or-reclamation>. | ambiguity | 6301 (Verified) |

### RFC 8306: Extensions to the Path Computation Element Communication Protocol (PCEP) for Point-to-Multipoint Traffic Engineering Label Switched Paths {#ra_rfc8306}

Depth: deep. Errata: checked (checked: 1 (5622 verified, technical, 3.13 message length)). Obsoletes: RFC 6006.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0307 | 3.13 | "The total PCEP message length, including the common header, is 16 bytes." | The maximum PCEP message length is (2^16)-1 octets (16-bit Message-Length field), not 16 bytes. Fixed by erratum 5622; RFC 8623 Section 8 already uses the corrected wording. | error | 5622 (Verified) |
| RA-0308 | 3.7, 3.8 | "If the PCE does not understand the P2MP flag in the RP object, then the PCE would send a PCErr message with Error-Type=2 (Capability not supported) as per [RFC5440]." | A PCE that does not understand the N bit cannot recognise the request as P2MP: RFC 5440 7.4.1 requires unassigned RP flags to be ignored, so a back-level PCE treats the request as P2P and fails, if at all, on the END-POINTS Object-Type 3 or 4 (an unknown or unsupported object, Error-Type 3 or 4 of RFC 5440), not with Error-Type 2. Section 3.8 then says such a PCE "SHOULD reject the request", which a back-level PCE cannot be required to do. A PCC therefore cannot rely on Error-Type 2 to detect a PCE without P2MP support. | contradiction | none found; **proposed erratum below** |
| RA-0309 | 3.10 | "To remove old leaves, the PCC MUST build a P2MP request using END-POINTS with leaf type 2.  If no type-2 END-POINTS exist, then the PCE MUST send Error-Type 17, Error-value 1" | A PCE cannot tell from a request without type-2 END-POINTS that a removal was intended, so the condition for 17/1 is not decidable as written. The conditions for 17/2 and 17/3 ("no END-POINTS with leaf type 3 or 4, or in the presence of END-POINTS with leaf type 1 or 2") are given only in prose and do not say which value applies when both type 3 and type 4 are absent. The same paragraph says "if a PCC receives a request", where the receiver of a PCReq is the PCE. | ambiguity | none found; **proposed erratum below** |
| RA-0310 | 3.10 | "For old leaves, the PCC MUST provide the old path as a list of RROs that immediately follows each END-POINTS object. / Case 1 ... END-POINTS for leaf type 1 / RRO list" | New leaves (type 1) have no old path, and Cases 2, 7, 8 and 9 show type-1 END-POINTS without an RRO list, but Cases 1 and 3 show an RRO list after the type-1 END-POINTS. The examples disagree about whether an RRO list may (or must) follow a type-1 END-POINTS object. | contradiction | none found |
| RA-0311 | 3.3.1, 3.5 | "By default, the path returned by the PCE SHOULD use the compressed format. / If the E-bit (ERO-Compress bit) was set to 1 in the request, then the path will be formed by an ERO followed by a list of SEROs." | Section 3.3.1 makes the compressed format the default for replies regardless of the request, while Section 3.5 ties the compressed format to E = 1 in the request. It is not stated whether a PCE may return SEROs to a PCC whose request had E = 0, nor whether E in the reply must mirror E in the request. | ambiguity | none found |
| RA-0312 | 3.13, 3.15 | "the receiver side of the fragmented message may start a timer once it receives the first piece ... Error-Type=18; Error-value=1: if a PCE has not received the last piece of the fragmented message" | The timer value is not given, and only the PCE side (request fragmentation) has an error value; a PCC that does not receive the last fragment of a fragmented PCRep has no defined error (RFC 8623 later adds 18/2 to 18/4 for reports, updates and initiations only). "Response ID" in Section 3.13.2 is undefined; the RP object carries a Request-ID-number. | ambiguity | none found |

Proposed erratum RA-0308 (RFC 8306, Section 3.7, 3.8; type: Technical):

```
Original Text
-------------
   o  If the PCE does not understand the P2MP flag in the RP object,
   then the PCE would send a PCErr message with Error-Type=2
   (Capability not supported) as per [RFC5440].

Corrected Text
--------------
   o  A PCE that does not understand the P2MP flag in the RP object
   ignores it (Section 7.4.1 of [RFC5440]) and is expected to reject
   the request because the P2MP END-POINTS Object-Type is not
   recognised or not supported (Error-Type 3 or 4 [RFC5440]). A PCC
   SHOULD NOT send P2MP requests to a PCE that has not advertised
   the P2MP capability (Sections 3.1.1 and 3.1.2).

Notes
-----
   The described behaviour (Error-Type 2) cannot be produced by a
   PCE that does not implement this document; the observable
   behaviour is governed by the unknown-object rules of RFC 5440.
```

Proposed erratum RA-0309 (RFC 8306, Section 3.10; type: Technical):

```
Original Text
-------------
   A generic "Inconsistent END-POINTS" error will be used if a PCC
   receives a request that has an inconsistent END-POINTS setting

Corrected Text
--------------
   A generic "Inconsistent END-POINTS" error will be used if a PCE
   receives a request that has an inconsistent END-POINTS setting
   ... (and state the exact condition for each of Error-values 1 to
   3 of Error-Type 17).

Notes
-----
   The receiver of a PCReq is a PCE. The conditions for Error-Type
   17 values 1 to 3 are not testable as worded.
```

### RFC 8408: Conveying Path Setup Type in PCE Communication Protocol (PCEP) Messages {#ra_rfc8408}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0313 | 5 | "If the PCE does not support the intended PST, it MUST send a PCErr message with Error-Type = 21 ... Error-value = 1 (Unsupported path setup type) and close the PCEP session." | A single request or update with a PST outside the negotiated set tears down the whole session, including all other LSPs' state and delegations; the text does not distinguish a PST that the peer never advertised (a protocol violation) from one that is advertised but not usable for this LSP. Later documents (RFC 9603 5.2.1, for SRv6) answer the comparable case with a per-LSP error and keep the session, so behaviour for unknown PSTs now differs by document. | ambiguity | none found |
| RA-0314 | 3 | "If there are no sub-TLVs, then the TLV Length field MUST be equal to four bytes plus the size of the PST list, excluding any padding bytes." | The Length counts the PST-list padding when sub-TLVs follow but not when they do not, and excludes only the padding of the final sub-TLV. Senders that count the final padding (the general RFC 5440 7.1 habit of padding the value) produce a Length that the strict check of this section rejects with 10/11 and session close. | ambiguity | none found |

### RFC 8623: Stateful Path Computation Element (PCE) Protocol Extensions for Usage with Point-to-Multipoint TE Label Switched Paths (LSPs) {#ra_rfc8623}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0315 | 12 | "Security considerations for the LSP instantiation mechanism are as per [RFC8231]." | The LSP instantiation mechanism (PCInitiate) is defined in RFC 8281, not RFC 8231; RFC 8231 has no instantiation security text. The preceding bullet already refers to RFC 8231 for the other stateful operations, so the reference appears to be a copy error. | error | none found; **proposed erratum below** |
| RA-0316 | 7.1.1, 6.1, 7.2 | "the PCE MUST respond with a PCErr message carrying error-type 6 ... error-value 14 ("P2MP-LSP-IDENTIFIERS TLV missing") and close the PCEP session." | A PCRpt with N set but no P2MP-LSP-IDENTIFIERS TLV requires the session to be closed, while the comparable omissions of the mandatory S2LS object (6/13, Section 6.1), the END-POINTS object (6/3) and an S2LS / LSP O-field mismatch (10/22, Section 7.2) only require a PCErr. No reason is given for the difference, and the text does not say whether the rest of the PCRpt (other state reports) is processed in the non-closing cases. | ambiguity | none found; **proposed erratum below** |
| RA-0317 | 6.1, 6.6.2 | "<end-point-actual-path-pair-list>::= [<END-POINTS>] [<S2LS>] <actual-path> ... / END-POINTS for leaf type 3 (modify) S2LS (O=UP) RRO list" | The PCRpt grammar requires an <end-point-intended-path-pair-list> (each pair ending in an ERO/SERO) before any actual-path pair, but the Section 6.6.2 examples carry an END-POINTS / S2LS group followed only by an RRO list, and interleave RRO groups and empty-ERO groups. A strict RBNF parser rejects the examples; a parser built from the examples accepts messages the grammar does not. | contradiction | none found; **proposed erratum below** |
| RA-0318 | 5.1, 6.6.1 | "Each P2MP TE LSP Update Request in a PCUpd message MUST contain all LSP parameters that a PCE wishes to set / The update message does not need to encode the full P2MP tree in this case." | Section 5.1 requires a PCUpd to carry all parameters the PCE wishes to set (as RFC 8231 does for P2P, where the ERO replaces the path), while Section 6.6.1 shows an update carrying only the leaves of type 3 being changed. The text does not state that leaves absent from a PCUpd keep their current paths, nor how a PCC distinguishes a partial update from a full replacement of the tree. | contradiction | none found; **proposed erratum below** |
| RA-0319 | 9 | "If the PCC supports the extensions as per this document (understands the N (P2MP-CAPABILITY) and M (P2MP-LSP-UPDATE-CAPABILITY) flags in the LSP object) but did not advertise this capability" | The N (P2MP-CAPABILITY) and M flags are flags of the STATEFUL-PCE-CAPABILITY TLV (Section 5.2), not of the LSP object, whose N flag means "P2MP" (Section 7.1). The section also covers only a receiver that itself did not advertise the capability; a receiver that advertised it while the sender did not (the sender violating the first MUST NOT) is not given an error, and the trigger is "a PCUpd message" rather than a PCUpd with the LSP N flag set. | ambiguity | none found; **proposed erratum below** |
| RA-0320 | 7.1, 8 | "The receiver needs to wait for additional fragments until it receives an LSP with the same PLSP-ID and with the F-bit set to 0." | No timer is given for "does not receive the last part" (18/2 to 18/4), and the text does not say whether messages for other LSPs may be interleaved between fragments, or what happens when a fragment of a second update for the same PLSP-ID (different SRP-ID-number) arrives before the first is complete. | ambiguity | none found |
| RA-0321 | 6.1, 7.1.1 | "Error-value=3 ("END-POINTS object missing") (defined in [RFC5440]. / Tunnel ID:  Remains constant over the lifetime of a tunnel." | A closing parenthesis is missing in Section 6.1; in Section 7.1.1 the IPv6 TLV field list describes "Tunnel ID" a second time after "P2MP ID", apparently a leftover. | editorial | none found |

Proposed erratum RA-0315 (RFC 8623, Section 12; type: Technical):

```
Original Text
-------------
   o  Security considerations for the LSP instantiation mechanism
   are as per [RFC8231].

Corrected Text
--------------
   o  Security considerations for the LSP instantiation mechanism
   are as per [RFC8281].

Notes
-----
   PCE-initiated LSP instantiation is specified in RFC 8281, whose
   Section 9 holds the security considerations for that mechanism;
   RFC 8231 does not define instantiation.
```

Proposed erratum RA-0316 (RFC 8623, Section 7.1.1, 6.1, 7.2; type: Technical):

```
Original Text
-------------
   the PCE MUST respond with a PCErr message carrying error-type 6
   ("mandatory object missing") and error-value 14
   ("P2MP-LSP-IDENTIFIERS TLV missing") and close the PCEP session.

Corrected Text
--------------
   (Clarification requested.) State whether the session is to be
   closed for all of 6/3, 6/13, 6/14 and 10/22 in a P2MP PCRpt, or
   only for 6/14, and whether the remaining state reports in the
   same message are processed.

Notes
-----
   Section 7.1.1 mandates closing the session for 6/14; Sections 6.1
   and 7.2 do not for 6/13, 6/3 and 10/22. Implementations may treat
   these cases differently.
```

Proposed erratum RA-0317 (RFC 8623, Section 6.1, 6.6.2; type: Technical):

```
Original Text
-------------
   END-POINTS for leaf type 3 (modify)
   S2LS (O=UP)
   RRO list
   END-POINTS for leaf type 3 (modify)
   S2LS (O=DOWN)
   ERO list (empty)

Corrected Text
--------------
   (Clarification requested.) Either extend the RBNF so that a pair
   may carry only an actual path, or correct the examples to show
   the intended-path pairs followed by the actual-path pairs.

Notes
-----
   The examples omit the intended path for leaves that are reported
   with an RRO, which the grammar in Section 6.1 does not permit.
```

Proposed erratum RA-0318 (RFC 8623, Section 5.1, 6.6.1; type: Technical):

```
Original Text
-------------
   Each P2MP TE LSP Update Request in a PCUpd message MUST contain
   all LSP parameters that a PCE wishes to set for a given P2MP TE
   LSP.

Corrected Text
--------------
   Each P2MP TE LSP Update Request in a PCUpd message MUST contain
   all LSP parameters that a PCE wishes to set for a given P2MP TE
   LSP. Leaves that are not listed in any END-POINTS object of the
   update keep their current path; leaves are removed only when
   listed with leaf type 2.

Notes
-----
   The partial-update semantics are implied by the example and by
   Section 3.1 but are not stated as a rule.
```

Proposed erratum RA-0319 (RFC 8623, Section 9; type: Technical):

```
Original Text
-------------
   (understands the N (P2MP-CAPABILITY) and M
   (P2MP-LSP-UPDATE-CAPABILITY) flags in the LSP object)

Corrected Text
--------------
   (understands the N (P2MP-CAPABILITY) and M
   (P2MP-LSP-UPDATE-CAPABILITY) flags in the STATEFUL-PCE-CAPABILITY
   TLV) ... upon receipt of a PCUpd message with the N (P2MP) flag
   set in the LSP object, ... The same error applies when either
   speaker has not advertised the capability.

Notes
-----
   The text mixes the capability flags (STATEFUL-PCE-CAPABILITY TLV)
   with the P2MP flag of the LSP object, and does not cover a
   speaker that receives P2MP messages from a peer that did not
   advertise the capability.
```

### RFC 8664: Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing {#ra_rfc8664}

Depth: deep. Errata: checked (checked: 1 (6753 verified, technical)). Updates: RFC 8408.

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

### RFC 8685: Path Computation Element Communication Protocol (PCEP) Extensions for the Hierarchical Path Computation Element (H-PCE) Architecture {#ra_rfc8685}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0322 | 4.2 | "If the domain path computation succeeds, the parent PCE sends a PCRep message ... Otherwise, it sends a PCReq message that carries the NO-PATH object to the child PCE." | The negative reply is a PCRep carrying NO-PATH (Section 5 and Section 3.8), not a PCReq. The same paragraph calls the flag the "Domain Path Request bit", while Section 3.3.1 and the IANA registry name it "S (Domain Sequence bit)". | error | none found; **proposed erratum below** |
| RA-0323 | 3.2.1, 4.1 | "If the PCE understands the H-PCE PCReq message but did not advertise its H-PCE capability, it MUST send a PCErr message with Error-Type=28 / the peer PCE SHOULD send a PCErr message to the child PCE and MUST specify Error-Type=28 (H-PCE Error) and Error-Value=1" | Section 3.2.1 makes the 28/1 PCErr a MUST, Section 4.1 makes sending it a SHOULD (with a MUST only on the error values). Neither section says what happens to the request itself (whether it is also answered, or silently dropped) or whether the session stays up. | contradiction | none found; **proposed erratum below** |
| RA-0324 | 3.2.1.1 | "the receiving PCE will ignore the H-PCE related parameters because they are all encoded in TLVs in standard PCEP objects." | Not all H-PCE parameters are TLVs: the OF codes 12 to 14 (Section 3.4.1) are values of the OF object, METRIC types 20 and 21 (Section 3.5) are values of the METRIC T field, and the SVEC O bit and the NO-PATH-VECTOR bits are flags. A legacy PCE does not ignore an unknown OF code or METRIC type with the P flag set; Section 3.4.2 itself sends such cases to the RFC 5440 / RFC 5541 error procedures. The backward-compatibility claim is therefore true only for the H-PCE-CAPABILITY, H-PCE-FLAG and Domain-ID TLVs. | contradiction | none found; **proposed erratum below** |
| RA-0325 | 3.4.1, 3.5 | "A path P passes through K unique domains {Dpi, (i=1...K)}. / If a domain is re-entered, then the domain should be double counted." | MTD ("Minimize the number of Transit Domains") is defined by K, the number of unique domains including ingress and egress, while the Domain Count metric (T=20) counts a re-entered domain twice. The two quantities differ for paths with re-entry, and neither says whether ingress and egress domains count. The MBN formula counts domain transitions between consecutive links, which equals the number of border nodes only when each transition has a single border node (area boundaries), not for inter-AS links with an ASBR on each side, and it does not say to which domain an inter-AS link belongs. | ambiguity | none found |
| RA-0326 | 3.2.2 | "Type=1: The Domain ID field carries a 2-byte AS number. Padded with trailing zeros to a 4-byte boundary." | It is not stated whether the TLV Length includes the padding of the Domain ID (Length 8) or excludes it as RFC 5440 7.1 TLV padding (Length 6), nor whether Area-Len for type 4 counts octets of the area address. Both encodings are found. | ambiguity | none found |

Proposed erratum RA-0322 (RFC 8685, Section 4.2; type: Technical):

```
Original Text
-------------
   Otherwise, it sends a PCReq message that carries the NO-PATH
   object to the child PCE.

Corrected Text
--------------
   Otherwise, it sends a PCRep message that carries the NO-PATH
   object to the child PCE.

Notes
-----
   A NO-PATH object is carried in a PCRep (RFC 5440 7.5). Section
   4.2 also refers to the S bit of Section 3.3.1 as the "Domain Path
   Request bit"; "Domain Sequence bit (S)" would match Section 3.3.1
   and Section 7.4.
```

Proposed erratum RA-0323 (RFC 8685, Section 3.2.1, 4.1; type: Technical):

```
Original Text
-------------
   the peer PCE SHOULD send a PCErr message to the child PCE and
   MUST specify Error-Type=28 (H-PCE Error) and Error-Value=1 (H-PCE
   Capability not advertised) in the PCEP-ERROR object.

Corrected Text
--------------
   the peer PCE MUST send a PCErr message to the child PCE with
   Error-Type=28 (H-PCE Error) and Error-Value=1 (H-PCE Capability
   not advertised) in the PCEP-ERROR object, and MUST NOT process
   the request further.

Notes
-----
   The two sections state the same rule with different requirement
   levels.
```

Proposed erratum RA-0324 (RFC 8685, Section 3.2.1.1; type: Technical):

```
Original Text
-------------
   the receiving PCE will ignore the H-PCE related parameters
   because they are all encoded in TLVs in standard PCEP objects.

Corrected Text
--------------
   the receiving PCE will ignore the H-PCE-related TLVs. The OF
   codes, METRIC types and flags defined in this document are
   handled by such a PCE as unknown values according to [RFC5440]
   and [RFC5541]; in particular, a request carrying them with the P
   flag set may be rejected.

Notes
-----
   Section 3.4.2 (last paragraph) already recognises that unknown OF
   codes are handled per RFC 5440, which contradicts the "all
   encoded in TLVs" statement.
```

### RFC 8697: Path Computation Element Communication Protocol (PCEP) Extensions for Establishing Relationships between Sets of Label Switched Paths (LSPs) {#ra_rfc8697}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0327 | 5 | "Range MUST be greater than 0, and it MUST be such that (Start-Assoc-ID + Range) does not cross the largest Association ID value of 0xffff." | "Does not cross" does not say whether Start-Assoc-ID + Range = 0xffff is allowed. The range covers Start-Assoc-ID .. Start-Assoc-ID + Range - 1, so a sum of 0xffff ends at 0xfffe and is valid, and a sum of 0x10000 would include the reserved value 0xffff; an implementation reading "cross" as "reach" rejects a valid Open with 1/1. | ambiguity | none found; **proposed erratum below** |
| RA-0328 | 6.3.1 | "Any subsequent PCRpt message SHOULD include only the associations that are being modified or removed." | Removal is signalled by the R flag, so a later PCRpt that omits an association means "unchanged". During State Synchronization the associations "MUST be included", but the text does not say whether an association missing from a synchronization report (for an LSP already known from a previous session or an incremental synchronization) means removal. | ambiguity | none found |
| RA-0329 | 5.1 | "the local PCEP speaker MUST remove any associations that are not in the new operator-configured range (by disassociating any LSPs that are part of it (and notifying the PCEP peer of this change))." | The rule applies to every session established with the Association Source, but the text does not say what happens when two sessions (for example to two PCEs) announce different ranges for the same source, or when the session later goes down (whether the configured associations come back). | ambiguity | none found |

Proposed erratum RA-0327 (RFC 8697, Section 5; type: Technical):

```
Original Text
-------------
   it MUST be such that (Start-Assoc-ID + Range) does not cross the
   largest Association ID value of 0xffff.

Corrected Text
--------------
   it MUST be such that (Start-Assoc-ID + Range) is less than or
   equal to 0xffff, i.e., the last Association ID in the range
   (Start-Assoc-ID + Range - 1) is not greater than 0xfffe.

Notes
-----
   The same wording is repeated in Section 5.1 ("crosses the largest
   Association ID value of 0xffff").
```

### RFC 8741: Ability for a Stateful Path Computation Element (PCE) to Request and Obtain Control of a Label Switched Path (LSP) {#ra_rfc8741}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0330 | 3, 4 | "If a PCE wishes to gain control over an LSP, it sends a PCUpd message with the C flag set to 1 in the SRP object." | The PCUpd grammar of RFC 8231 requires a <path> (ERO and attributes) for each LSP; this document does not say what the ERO of a control request carries (empty, the current path, or anything) nor that the PCC must not act on it. With PLSP-ID 0 there is no single LSP whose path could be given. The text also does not say whether a refused request is answered (it "MAY choose to not respond"). | ambiguity | none found |

### RFC 8745: Path Computation Element Communication Protocol (PCEP) Extensions for Associating Working and Protection Label Switched Paths (LSPs) with St {#ra_rfc8745}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0331 | 3.1 vs 4.5 | "A PPAG can have one working LSP and/or one or more protection LSPs. (3.1) / When the protection type is set to 1:N ... there MUST be at maximum only one protection LSP, and the number of working LSPs MUST NOT be more than N within a PPAG. (4.5)" | Section 3.1 limits a group to one working LSP and allows several protection LSPs; Section 4.5 allows up to N working LSPs and only one protection LSP for 1:N. N itself is not carried anywhere in PCEP, so the "more than N" check (26/10) has no defined bound. | contradiction | none found; **proposed erratum below** |
| RA-0332 | 4.5 | "During the make-before-break (MBB) procedure, two paths will briefly coexist. The error handling related to the number of LSPs allowed in a PPAG MUST NOT be applied during MBB." | Nothing in the PCEP messages tells the receiver that an MBB is in progress; the receiver has to infer it (for example same PLSP-ID and Tunnel ID with a new LSP-ID in LSP-IDENTIFIERS). Without a stated rule a PCE may count the MBB copy as an extra working LSP (26/10) or never apply the limit. | ambiguity | none found |
| RA-0333 | 3.1, 4.5 | "In case of Path Protection, an LSP-IDENTIFIERS TLV SHOULD be included for all LSPs" | The MUST in 3.1 (same source, destination and Tunnel ID) and the 26/9 check in 4.5 rely on LSP-IDENTIFIERS, which is only a SHOULD (and for SR LSPs is not otherwise required). For a member without the TLV the check cannot be made, and the text does not say whether such a member is accepted unchecked or refused. | ambiguity | none found |

Proposed erratum RA-0331 (RFC 8745, Section 3.1 vs 4.5; type: Technical):

```
Original Text
-------------
   A PPAG can have one working LSP and/or one or more protection
   LSPs.

Corrected Text
--------------
   A PPAG can have one or more working LSPs and/or one or more
   protection LSPs, subject to the limits for the Protection Type
   given in Section 4.5.

Notes
-----
   The 1:N limit needs N to be configured or signalled; otherwise
   26/10 cannot be applied consistently.
```

### RFC 8751: Hierarchical Stateful Path Computation Element (PCE) {#ra_rfc8751}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8779: Path Computation Element Communication Protocol (PCEP) Extensions for GMPLS {#ra_rfc8779}

Depth: part. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0334 | 2.5.2.5 | "O: Old label. ... If the L bit is set, this bit SHOULD be set to 0 and ignored on receipt. / A LABEL-SET TLV with the O and L bits set MUST trigger a PCErr message with Error-Type=10 (Reception of an invalid object) and Error-value=29" | The definition of the O bit tells the receiver to ignore O when L is set; the following paragraph makes the same combination an error (10/29). A receiver cannot do both. | contradiction | none found; **proposed erratum below** |
| RA-0335 | 2.5.2.1-2.5.2.3 | "This TLV MAY be ignored, in which case a PCRep with NO-PATH SHOULD be returned, as described in Section 2.5.1." | The address TLVs are defined for the Generalized END-POINTS object, and their "MAY be ignored ... NO-PATH" handling only fits a PCReq. RFC 9050 7.3.1 reuses them in the CCI object (PCInitiate / PCRpt), where NO-PATH does not exist; the handling there comes from RFC 9050 (31/5) and is not a property of these TLVs. | ambiguity | none found |

Proposed erratum RA-0334 (RFC 8779, Section 2.5.2.5; type: Technical):

```
Original Text
-------------
   If the L bit is set, this bit SHOULD be set to 0 and ignored on
   receipt.

Corrected Text
--------------
   If the L bit is set, this bit MUST be set to 0; see below for the
   error handling when both are set.

Notes
-----
   Both sentences are in Section 2.5.2.5.
```

### RFC 8786: Updated Rules for Processing Stateful PCE Request Parameters Flags {#ra_rfc8786}

Depth: deep. Errata: not checked. Updates: RFC 8231.

Nothing notable found at this depth.

### RFC 8800: Path Computation Element Communication Protocol (PCEP) Extension for Label Switched Path (LSP) Diversity Constraint Signaling {#ra_rfc8800}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0336 | 5.1 | "The Operator-configured Association Range MUST be set for this association-type to mark a range of Association Identifiers that are used for operator-configured associations" | RFC 8697 5.1 makes the OP-CONF-ASSOC-RANGE TLV a SHOULD for types that are both dynamic and operator-configured and lets each Association Type define a default range; this document makes the range a MUST but defines no default. When a peer's Open has no range for the Disjoint type, the receiver cannot tell whether an Association ID it receives is operator-configured or dynamic, and so cannot apply the 26/4 / 26/8 checks of RFC 8697 6.4. "MUST be set" also does not say whether it is a configuration requirement or a requirement to send the TLV. | ambiguity | none found; **proposed erratum below** |
| RA-0337 | 5.3 | "If the OF-List TLV is included in the ASSOCIATION object, the first OF-code inside the OF object MUST be one of the disjoint OFs defined in this document." | The OF-codes are inside the OF-List TLV, not an OF object (the OF object of RFC 5541 is a separate object in PCReq/PCRep). | editorial | none found; **proposed erratum below** |
| RA-0338 | 5.6, 5.1 | "In case of a PCRpt message, the PCE MUST return a PCErr message with Error-Type 26 (Association Error) and Error-value 7 (Cannot join the association group)." | For a strict (T) group the same condition (disjointness impossible) gives 26/7 when the LSP is reported, but a PCUpd with an empty ERO when it arises from a network event. Whether a member whose join was refused stays delegated without a path, and whether a later topology change must re-admit it, is not said. An LSP reported in a PCRpt is already set up, so "cannot join" leaves the PCC with an LSP outside the group it was configured for. | ambiguity | none found |

Proposed erratum RA-0336 (RFC 8800, Section 5.1; type: Technical):

```
Original Text
-------------
   The Operator-configured Association Range MUST be set for this
   association-type to mark a range of Association Identifiers that
   are used for operator-configured associations

Corrected Text
--------------
   The Operator-configured Association Range MUST be configured for
   this Association Type and SHOULD be advertised in the
   OP-CONF-ASSOC-RANGE TLV [RFC8697]. If no range is advertised by
   the Association Source, the default range is [state the default],
   to mark a range of Association Identifiers that are used for
   operator-configured associations

Notes
-----
   Without a default, the Operator-configured
   dynamic distinction of RFC 8697 cannot be applied to peers that
   omit the TLV.
```

Proposed erratum RA-0337 (RFC 8800, Section 5.3; type: Editorial):

```
Original Text
-------------
   the first OF-code inside the OF object MUST be one of the
   disjoint OFs defined in this document.

Corrected Text
--------------
   the first OF-code inside the OF-List TLV MUST be one of the
   disjoint OFs defined in this document.

Notes
-----
   Editorial; the meaning is clear from the preceding sentence.
```

### RFC 9005: Path Computation Element Communication Protocol (PCEP) Extension for Associating Policies and Label Switched Paths (LSPs) {#ra_rfc9005}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9050: Path Computation Element Communication Protocol (PCEP) Procedures and Extensions for Using the PCE as a Central Controller (PCECC) of LSPs {#ra_rfc9050}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0339 | 3 vs 5.5.8, 7.3 | "The PCC MUST NOT make allocations from the label space set aside for the PCE to avoid overlap and collisions of label allocations. (3) / The PCE can request the PCC to allocate the label using the PCInitiate message. (5.5.8)" | Section 3 forbids PCC allocations from the PCE's label space, while Section 5.5.8 lets the PCE ask the PCC to allocate (C flag), including a specific value 'n', and Section 7.3 says the PCC allocates "from its label space". The text does not say which range a C-flag allocation is taken from, nor whether a requested value 'n' inside the PCE range is "invalid" (31/3) or must be honoured. | contradiction | none found; **proposed erratum below** |
| RA-0340 | 5.5.1, 7.3 | "Also, the CC-ID is unique in each PCEP session (5.5.1) / the value is unique within the scope of the PCE and is constant for the lifetime of a PCEP session. (7.3)" | Section 5.5.1 scopes CC-ID uniqueness to a PCEP session, Section 7.3 to the PCE. With re-delegation (5.5.5) a new PCE takes over instructions by CC-ID, so the CC-ID of one PCE can collide with one a second PCE already uses on the same PCC; no error is defined for a CC-ID that is already in use with different content. | ambiguity | none found |
| RA-0341 | 5.5.8 | "If the PCC wishes to withdraw or modify the previously assigned label, it MUST send a PCRpt message without any label or with the label containing the new value" | The Label field of the CCI object (7.3, Figure 8) is a fixed 20-bit field, so a CCI "without any label" cannot be encoded; presumably label value 0 is meant, but 0 is also the IPv4 Explicit NULL label, which an egress may legitimately allocate. The PCE cannot distinguish a withdrawal from an allocation of label 0. | ambiguity | none found; **proposed erratum below** |
| RA-0342 | 5.5.1, 5.5.2 | "then, the PCC would send a PCRpt message with the allocated label encoded in the CC-ID object" | There is no "CC-ID object"; the CC-ID is a field of the CCI object (7.3). The same wording appears in 5.5.1 and 5.5.2. | editorial | none found; **proposed erratum below** |
| RA-0343 | 5.5.3.2, 5.5.1 | "In the case where the label allocation is made by the PCC itself (see Section 5.5.8), the removal procedure remains the same, adding the sequence constraint." | "The sequence constraint" is never defined. The text sets no order for cleanup; Figure 5 removes the egress label first and the ingress LSP last, which leaves traffic entering the LSP while downstream labels are already gone. | ambiguity | none found |
| RA-0344 | 5.5.1, 6.1 | "A node can determine its role based on the setting of the O bit in the CCI object(s) and the LSP-IDENTIFIERS TLV (5.5.1) / The CCI object received at the ingress node MUST have the O bit (out-label) set. (6.1)" | Section 5.5.1 lets the O bit determine the role, while 6.1 checks the O bit against the role (31/3) and says the role is identified via the addresses in the LSP-IDENTIFIERS TLV. If the role is derived from the O bit the check is vacuous; the TLV-based reading needs a definition of which local addresses count as "ours". | ambiguity | none found |
| RA-0345 | 5.4 | "If the PCECC-CAPABILITY sub-TLV is advertised and the STATEFUL-PCE-CAPABILITY TLV is not advertised, or is advertised without the I flag set, in the OPEN object, the receiver MUST: ... Error-value=17" | The precedence between this rule and "If it is present without the corresponding PST listed ... it MUST be ignored" is not stated (a sub-TLV without PST 2 and without stateful capability: ignore, or 19/17 and close?). The case of PST 2 with the sub-TLV but L = 0 is also not covered: no error is named, and the session presumably runs without label download. | ambiguity | none found |

Proposed erratum RA-0339 (RFC 9050, Section 3 vs 5.5.8, 7.3; type: Technical):

```
Original Text
-------------
   The PCC MUST NOT make allocations from the label space set aside
   for the PCE to avoid overlap and collisions of label allocations.

Corrected Text
--------------
   The PCC MUST NOT make allocations from the label space set aside
   for the PCE to avoid overlap and collisions of label allocations,
   except when the PCE requests an allocation by setting the C flag
   (Section 5.5.8); such allocations are made from the label space
   set aside for the PCE.

Notes
-----
   Either the C-flag allocation is an explicit exception to Section
   3, or it must come from the PCC's own space; the document should
   say which, and how a requested value outside that range is
   answered.
```

Proposed erratum RA-0341 (RFC 9050, Section 5.5.8; type: Technical):

```
Original Text
-------------
   it MUST send a PCRpt message without any label or with the label
   containing the new value, respectively, in the CCI object.

Corrected Text
--------------
   it MUST send a PCRpt message with the Label field set to 0 and
   the C flag clear (withdrawal) or with the Label field containing
   the new value (modification), respectively, in the CCI object.

Notes
-----
   The encoding of a withdrawal needs to be stated; label 0 alone is
   ambiguous with an allocated IPv4 Explicit NULL.
```

Proposed erratum RA-0342 (RFC 9050, Section 5.5.1, 5.5.2; type: Editorial):

```
Original Text
-------------
   the PCC would send a PCRpt message with the allocated label
   encoded in the CC-ID object

Corrected Text
--------------
   the PCC would send a PCRpt message with the allocated label
   encoded in the CCI object

Notes
-----
   Sections 5.5.1 and 5.5.2.
```

### RFC 9059: Path Computation Element Communication Protocol (PCEP) Extensions for Associated Bidirectional Label Switched Paths (LSPs) {#ra_rfc9059}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0346 | 4.2 | "The Bidirectional LSP Association Group TLV is an OPTIONAL TLV ... * For co-routed LSPs, this TLV MUST be present and the C flag set. * For reverse LSPs, this TLV MUST be present and the R flag set." | The TLV is called OPTIONAL but is mandatory for reverse and co-routed LSPs; no error is defined for its absence. A receiver of a member without the TLV cannot tell a forward non-co-routed LSP from a reverse or co-routed LSP whose sender omitted it, so the direction (26/17) and co-routed (26/18) checks of 5.7 depend on a TLV whose absence has no defined handling (RFC 8697 would suggest 6/x "Mandatory Object missing", but no value is allocated). | ambiguity | none found |
| RA-0347 | 5.7 | "If a PCE speaker attempts to add an LSP in a Single-Sided Bidirectional LSP Association for a different tunnel, the PCE speaker MUST send PCErr" | "PCE speaker" (here and in every rule of 5.7) is not a defined term; the rules apply to any PCEP speaker receiving the message (a PCC receiving a PCInitiate as well as a PCE receiving a PCRpt). In this sentence the speaker that "attempts to add" is also the one told to send the PCErr; the receiving speaker is meant. | editorial | none found; **proposed erratum below** |
| RA-0348 | 5.5, 5.7 | "For an associated bidirectional LSP, the LSP-IDENTIFIERS TLV [RFC8231] MUST be included in all forward and reverse LSPs." | No error is defined for a member without LSP-IDENTIFIERS, yet the tunnel (26/15) and endpoint (26/19) checks need it. | ambiguity | none found |

Proposed erratum RA-0347 (RFC 9059, Section 5.7; type: Editorial):

```
Original Text
-------------
   If a PCE speaker attempts to add an LSP in a Single-Sided
   Bidirectional LSP Association for a different tunnel, the PCE
   speaker MUST send PCErr

Corrected Text
--------------
   If a PCEP speaker receives a request to add an LSP in a
   Single-Sided Bidirectional LSP Association for a different
   tunnel, the receiving PCEP speaker MUST send PCErr

Notes
-----
   Section 5.7 uses "PCE speaker" six times.
```

### RFC 9357: Label Switched Path (LSP) Object Flag Extension for Stateful PCE {#ra_rfc9357}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0349 | 3.1 | "Length (16 bits): This indicates the length of the value portion in bytes. It MUST be in multiples of 4 and greater than 0." | No receive behaviour is given for a Length of 0 or not a multiple of 4 (malformed TLV, ignore the TLV, or use the whole words present). Section 3.2 only covers lengths longer or shorter than supported. | ambiguity | none found |

### RFC 9488: Local Protection Enforcement in the Path Computation Element Communication Protocol (PCEP) {#ra_rfc9488}

Depth: deep. Errata: not checked. Updates: RFC 5440.

Nothing notable found at this depth.

### RFC 9603: Path Computation Element Communication Protocol (PCEP) Extensions for IPv6 Segment Routing {#ra_rfc9603}

Depth: deep. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0350 | 5.2.1 vs 4.3.1, 4.3.1.1 | "If NT=0, the F bit MUST be 1, the S bit MUST be zero, and the Length MUST be 24." | The Length values in 5.2.1 (24/40/48/56/64) leave out the optional 8-octet SID Structure that the T bit adds (4.3.1, 4.3.1.1). A subobject with T = 1 and a SID (for example NT = 0, S = 0, T = 1, Length 32) is valid per 4.3.1 but "inconsistent" per the literal 5.2.1 table, which then requires 10/11 for the whole ERO. Only "If the T bit is 1, then the S bit MUST be zero" mentions T. | contradiction | none found; **proposed erratum below** |
| RA-0351 | 4.3.1 vs 5.2.1 | "The T bit MUST be set to 0 when the S bit is set to 1. If the T bit is set when the S bit is set, the T bit MUST be ignored. (4.3.1) / If the T bit is 1, then the S bit MUST be zero. ... it MUST consider the entire ERO invalid (5.2.1)" | 4.3.1 tells the receiver to ignore T when S is set; 5.2.1 lists T = 1 with S = 1 as an inconsistency that invalidates the whole ERO (10/11). The two receive rules cannot both be followed. | contradiction | none found; **proposed erratum below** |
| RA-0352 | 5.2.1 | "If a PCC receives an SRv6-ERO subobject in which the S and F bits are both set to 1 ... Error-value = 42" | A subobject with S = 1 and F = 1 also violates the NT/Length consistency rules earlier in the same section (for NT = 0 "the S bit MUST be zero"), which call for 10/11. Which of 10/11 and 10/42 is sent is not stated; the same overlap exists in RFC 8664 (10/7 vs 10/11). | ambiguity | none found |
| RA-0353 | 5.1, 8.8 | "Error-Value = 34 ("Missing PCE-SRv6-CAPABILITY sub-TLV")" | The sub-TLV is named SRv6-PCE-CAPABILITY everywhere else (4.1.1, 8.5); the error name reverses the words. The 10/40 rule is also stated twice (end of 5.1 and of 5.2.1). | editorial | none found |

Proposed erratum RA-0350 (RFC 9603, Section 5.2.1 vs 4.3.1, 4.3.1.1; type: Technical):

```
Original Text
-------------
   If NT=0, the F bit MUST be 1, the S bit MUST be zero, and the
   Length MUST be 24.

Corrected Text
--------------
   If NT=0, the F bit MUST be 1, the S bit MUST be zero, and the
   Length MUST be 24 (32 if the T bit is 1). [Likewise, add 8 to
   each Length below when the T bit is 1.]

Notes
-----
   The lengths listed for NT = 2, 4 and 6 with S = 0 also need "+8
   when T = 1".
```

Proposed erratum RA-0351 (RFC 9603, Section 4.3.1 vs 5.2.1; type: Technical):

```
Original Text
-------------
   If the T bit is set when the S bit is set, the T bit MUST be
   ignored.

Corrected Text
--------------
   (delete the sentence, or delete "If the T bit is 1, then the S
   bit MUST be zero." from Section 5.2.1)

Notes
-----
   Implementations following 4.3.1 accept what implementations
   following 5.2.1 reject.
```

### RFC 9604: Carrying Binding Label/SID in PCE-Based Networks {#ra_rfc9604}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0354 | 5 | "If a PCC receives a TE-PATH-BINDING TLV in any message other than PCUpd or PCInitiate, it MUST close the corresponding PCEP session with the reason "Reception of a malformed PCEP message"" | Section 4 lets the TLV be carried in the PCEP-ERROR object, and Section 5 says a PCE rejecting a PCRpt "MAY include the offending TE-PATH-BINDING TLV in the PCEP-ERROR object". A PCC receiving that PCErr (a message other than PCUpd or PCInitiate) is then required to close the session, so a PCE that follows the MAY turns every binding error into a session teardown. The PCE-side rule correctly allows "an LSP or PCEP-ERROR object", the PCC-side rule does not. | contradiction | none found; **proposed erratum below** |
| RA-0355 | 7 | "[RFC9603] defines the "SRv6-ERO subobject" for an SRv6 SID. Similarly to SR-ERO (Section 6), the NAI MUST NOT be included and the NT MUST be set to zero. Section 5.2.1 of [RFC8664] specifies bit settings and error handling in the case when NT=0." | For the SRv6-ERO the NT = 0 bit settings and error handling are in Section 5.2.1 of RFC 9603 (Length 24, F = 1, S = 0, error 10/11), not RFC 8664, whose NT = 0 rules (Length 8, F = 1) are for the SR-ERO. | error | none found; **proposed erratum below** |
| RA-0356 | 5, 8 | "To request that the PCE allocate the binding label/SID, a PCC MUST set P=1, D=1, and include an empty TE-PATH-BINDING TLV in the PCRpt message." | Section 5 defines an empty TLV only as a PCE request in PCUpd / PCInitiate; an empty TLV in a PCRpt with P = 0 (or with P = 1 when PCECC is not negotiated, which gives 19/16) has no stated meaning, and the BT of an empty TLV (which type to allocate) is only implied by "per BT". | ambiguity | none found |

Proposed erratum RA-0354 (RFC 9604, Section 5; type: Technical):

```
Original Text
-------------
   If a PCC receives a TE-PATH-BINDING TLV in any message other than
   PCUpd or PCInitiate, it MUST close the corresponding PCEP session

Corrected Text
--------------
   If a PCC receives a TE-PATH-BINDING TLV in any message other than
   PCUpd, PCInitiate, or PCErr (in the PCEP-ERROR object), it MUST
   close the corresponding PCEP session

Notes
-----
   Sections 4 and 5 allow the TLV in the PCEP-ERROR object in both
   directions.
```

Proposed erratum RA-0355 (RFC 9604, Section 7; type: Technical):

```
Original Text
-------------
   Section 5.2.1 of [RFC8664] specifies bit settings and error
   handling in the case when NT=0.

Corrected Text
--------------
   Section 5.2.1 of [RFC9603] specifies bit settings and error
   handling in the case when NT=0.

Notes
-----
   The sentence was copied from Section 6 (SR-ERO).
```

### RFC 9757: Path Computation Element Communication Protocol (PCEP) Extensions for Native IP Networks {#ra_rfc9757}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9862: Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing (SR) Policy Candidate Paths {#ra_rfc9862}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 8231.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0357 | 4 | "An SRPA MUST be assigned for all SR Policy LSPs by the PCEP speaker originating the LSP if the capability was advertised by both PCEP speakers. If the above condition is not satisfied, then the receiving PCEP speaker MUST send a PCErr message with: ... Error-value = 22" | The receiver can only know that an LSP is an SR Policy candidate path from its SRPA, so an LSP that lacks the SRPA cannot be detected as an "SR Policy LSP"; the 6/22 rule is not implementable without some other indication (none is defined). | ambiguity | none found |
| RA-0358 | 4.4 | "If a PCEP speaker receives an SRPA object whose association parameters do not follow the above specification, then the PCEP speaker MUST send a PCErr message with: * Error-Type = 26 "Association Error" * Error-value = 20 "SR Policy Identifier Mismatch"" | RFC 8697 Section 6.4 says invalid association parameters make the object malformed ("process it as a malformed message"). Section 4.4 instead answers malformed SRPA parameters with 26/20, an error whose name ("Identifier Mismatch") describes a different condition (4.1: identifiers not uniform across sessions or changed). A receiver cannot tell from 26/20 whether the encoding or the identity is wrong. | contradiction | none found |
| RA-0359 | 4.1, 6.3 | "Error-value = 20 "SR Policy Identifier Mismatch" (4.1, 4.4) / 20: SR Policy Identifiers Mismatch (Table in 6.3)" | The error name differs between the body (singular) and the IANA table (plural). | editorial | none found |
| RA-0360 | 4.5.2 | "the "(In PCEP or when BGP-LS Producer is PCE)", then variants MUST be used in PCEP." | The sentence is garbled ("the ..., then variants"); the intent is that the "(In PCEP or when BGP-LS Producer is PCE)" variants (for example 10 rather than 1) MUST be used in PCEP. | editorial | none found; **proposed erratum below** |
| RA-0361 | 4.5.2 | "When sending a PCInitiate message, the PCE is acting as the originator and therefore MAY set this to an address that it owns." | The Originator (ASN, Address) is part of the candidate path identity of RFC 9256 2.4 and must distinguish originators. With a MAY, a PCE may send an address it does not own or zero; two PCEs doing so (with ASN 0 when unconfigured) give the same originator, and the tie-break of RFC 9256 2.9 then compares identical values. The text does not say what the PCE puts there when it does not use an owned address. | ambiguity | none found |
| RA-0362 | 5.1, 5.3 | "If the PCE set this flag to 0, then the PCC MUST NOT send PCReq messages to this PCE for the SR Policy. (5.1) / When this flag is cleared, or when the SRPOLICY-CAPABILITY TLV is absent, the given peer MUST NOT be sent PCReq/PCRep messages for SR Policy LSPs. (5.3)" | 5.1 restricts PCReq from PCC to PCE when the PCE clears L; 5.3 extends it to any peer and to PCRep, and to the absence of the TLV. The PCC's L flag has no defined effect in 5.1, while 5.3 makes a PCC's L = 0 forbid the PCE's PCRep (which only answers a PCReq the PCC itself sent). | ambiguity | none found |

Proposed erratum RA-0360 (RFC 9862, Section 4.5.2; type: Editorial):

```
Original Text
-------------
   for example 1 - "PCEP" and 10 - "PCEP (In PCEP or when BGP-LS
   Producer is PCE)", the "(In PCEP or when BGP-LS Producer is
   PCE)", then variants MUST be used in PCEP.

Corrected Text
--------------
   for example 1 - "PCEP" and 10 - "PCEP (In PCEP or when BGP-LS
   Producer is PCE)", then the "(In PCEP or when BGP-LS Producer is
   PCE)" variants MUST be used in PCEP.

Notes
-----
   Editorial.
```

### RFC 9933: Carrying SR-Algorithm in Path Computation Element Communication Protocol (PCEP) {#ra_rfc9933}

Depth: light. Errata: not checked. Updates: RFC 8664, RFC 9603.

Nothing notable found at this depth.

## Multicast: PIM, IGMP, MLD and MVPN {#ra_mcast}

22 RFCs in this area (10 deep, 1 part, 3 read, 5 light, 3 scan); 22 findings, 7 of them proposed errata.

### RFC 2236: Internet Group Management Protocol, Version 2 {#ra_rfc2236}

Depth: scan (mechanical checks only). Errata: not checked. Updates: RFC 1112.

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

### RFC 2710: Multicast Listener Discovery (MLD) for IPv6 {#ra_rfc2710}

Depth: light (normative statements extracted). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4604: Using Internet Group Management Protocol Version 3 (IGMPv3) and Multicast Listener Discovery Protocol Version 2 (MLDv2) for Source-Specific {#ra_rfc4604}

Depth: read (normative statements). Errata: not checked. Updates: RFC 3376, RFC 3810.

Nothing notable found at this depth.

### RFC 4607: Source-Specific Multicast for IP {#ra_rfc4607}

Depth: read (normative statements). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0363 | 9 | "IANA allocates IPv4 addresses in the range 232.0.0.1 through 232.0.0.255 and IPv6 addresses in the range FF3x:4000:0001 to FF3x::7FFF:FFFF." | "FF3x:4000:0001" lacks the "::" (as written it is a different, malformed address); Section 1 gives the same range as FF3x::4000:0001 through FF3x::7FFF:FFFF. | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0363 (RFC 4607, Section 9; type: Editorial):

```
Original Text
-------------
   IPv6 addresses in the range FF3x:4000:0001 to FF3x::7FFF:FFFF.

Corrected Text
--------------
   IPv6 addresses in the range FF3x::4000:0001 to FF3x::7FFF:FFFF.

Notes
-----
   Section 1 states the range correctly.
```

### RFC 4610: Anycast-RP Using Protocol Independent Multicast (PIM) {#ra_rfc4610}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 5015: Bidirectional Protocol Independent Multicast (BIDIR-PIM) {#ra_rfc5015}

Depth: deep (Sections 3.1 to 3.7 and 5 read; 3.3 / 3.4 forwarding and Join/Prune rules read for state only). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0364 | 3.5.3.5, 3.6, 3.7.2 | "DFT = BOperiod + OPlow; MC = 0 / DFT = OPlow_int; MC = 0 / Interval: The backoff interval in milliseconds to be used by routers with worse metrics than the offering router." | The state table uses "BOperiod" and "OPlow_int", neither of which is defined in Section 3.6 (which defines Offer_Period, Backoff_Period, OPlow, OPhigh). For a router receiving a Backoff it is not said whether BOperiod is the Interval carried in the received Backoff message (the natural reading of 3.7.2) or the local Backoff_Period; for the DF sending Backoff ("DFT = BOperiod") it is presumably the local value. If a receiver uses a local value shorter than the DF's, it re-offers and takes over (Offer, MC reaches Election_Robustness) before the DF sends Pass, giving two acting DFs. 3.5.2.1 also uses "Offer_Interval" for the Offer_Period of 3.6. | ambiguity | not checked; **proposed erratum below** |
| RA-0365 | 3.5.3.1, 3.7.1 | "Used by the DF to record the identity and advertised metrics of the router that has made the last offer, for use when sending the Path message." | PIM has no Path message; the Pass message is meant. Section 3.7.1: "A standard checksum IP checksum is used" (doubled word). | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0364 (RFC 5015, Section 3.5.3.5, 3.6, 3.7.2; type: Technical):

```
Original Text
-------------
   DFT = BOperiod + OPlow; MC = 0

Corrected Text
--------------
   DFT = Backoff Interval (from the received Backoff message) +
   OPlow; MC = 0   [and define OPlow_int as OPlow in Section 3.6]

Notes
-----
   Section 3.6 defines neither value; the Interval field of the
   Backoff message (3.7.2) is otherwise unused by the state machine.
```

Proposed erratum RA-0365 (RFC 5015, Section 3.5.3.1, 3.7.1; type: Editorial):

```
Original Text
-------------
   for use when sending the Path message.

Corrected Text
--------------
   for use when sending the Pass message.

Notes
-----
   Best-Offer is used to fill the New Winner fields of the Pass
   message (3.7.3).
```

### RFC 5059: Bootstrap Router (BSR) Mechanism for Protocol Independent Multicast (PIM) {#ra_rfc5059}

Depth: deep. Errata: checked (checked: 3 (1321, 1322 verified editorial; 1323 held editorial)). Obsoletes: RFC 2362. Updates: RFC 4601.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0086 | 3.1, 3.3 | "group range in the message, which can be any sub-range of 224/4." | Abbreviated prefix; 224.0.0.0/4 is meant. Erratum 1322 corrects the fragment RP count range ("1..m" for "1..n"). | editorial | 1321 (Verified) |
| RA-0366 | 3.1.2 | "However, because the router immediately transitions to the AA state unconditionally, the NoInfo state can be considered to be virtual in a certain sense." | The NoInfo state table says "Receive BSM -> AP state; Forward BSM; Store RP-Set; Set Bootstrap Timer to BS_Timeout", i.e. a direct transition to Accept Preferred, not to Accept Any. The prose and the table give different next states; the table is the one consistent with storing the RP-Set and starting the BST. | contradiction | not among 1321-1323; **proposed erratum below** |
| RA-0367 | 3.1.2, 5 | "Accept Preferred ... Bootstrap Timer Expires -> AA state ... Set SZT to SZ_Timeout / Accept Any ... Receive BSM -> AP state ... Set Bootstrap Timer to BS_Timeout" | The SZT is started on AP -> AA but no transition stops it: on AA -> AP the table does not cancel the SZT, and the AP state has no "Scope-Zone Expiry Timer Expires" event. If the SZT keeps running in AP, its expiry there is undefined (removing a zone with an active BSR would be wrong); the intended "cancel SZT on leaving AA" has to be inferred. | ambiguity | not checked |
| RA-0368 | 3.1.5, 4.1.1 | "A BSM is empty if it contains no group ranges, or if it only contains a single group range where that group range has the Admin Scope Zone bit set (a scoped BSM) and an RP count of zero. / for a BSR to remove a group range, it should include that group range, but with an RP Count of zero" | For a scoped BSM whose only range is the scope range itself, the removal method of 4.1.1 (RP Count zero) produces exactly what 3.1.5 defines as an empty BSM, for which "Store RP-Set" is skipped; the RPs previously advertised for the whole scope range are then not removed and linger until their holdtimes expire. | contradiction | not checked |
| RA-0369 | 3.6 | "Routers that support only one of these protocols MUST NOT ignore ranges indicated as being for the other protocol.  They MUST NOT treat them as being for the protocol they support." | The two prohibitions do not say what the router must do with such a range. The intended behaviour (the range still takes part in longest-match RP selection, so the groups in it are not served by a less specific range of the supported protocol, and are treated as having no usable RP) is not stated. | ambiguity | not checked |

Proposed erratum RA-0366 (RFC 5059, Section 3.1.2; type: Technical):

```
Original Text
-------------
   However, because the router immediately transitions to the AA
   state unconditionally, the NoInfo state can be considered to be
   virtual in a certain sense.

Corrected Text
--------------
   However, because the router immediately transitions to the AP
   state unconditionally, the NoInfo state can be considered to be
   virtual in a certain sense.

Notes
-----
   The state table for NoInfo shows "Receive BSM -> AP state".
```

### RFC 5771: IANA Guidelines for IPv4 Multicast Address Assignments {#ra_rfc5771}

Depth: light. Errata: no verified errata in the index; page not read. Obsoletes: RFC 3138, RFC 3171. Updates: RFC 2780.

Nothing notable found at this depth.

### RFC 6037: Cisco Systems' Solution for Multicast in BGP/MPLS IP VPNs {#ra_rfc6037}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6513: Multicast in MPLS/BGP IP VPNs {#ra_rfc6513}

Depth: deep (5.1, 7.1, 9.1 in full; other normative sections by MUST/SHOULD). Errata: checked (checked: 2 (8851 verified, editorial 9.3.2; 3658 held, editorial 5.3.1 reference)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0370 | 5.1.3 | "1. The PEs in the candidate set are numbered from lowest to highest IP address, starting from 0. ... The result is taken modulo n, where n is the number of PEs in the candidate set." | The candidate set is defined as a set of triples <route, Upstream PE, Upstream RD>, one per route with the same prefix, so one PE can appear several times (one route per RD). Step 1 numbers "PEs", but whether a PE appearing under two RDs is numbered once or twice, and so whether n counts PEs or routes, is not stated; PEs that differ select different upstream PEs, and steady-state duplication or loss follows. The default procedure also defines ordering only for "a 32-bit IP address", leaving IPv6 Upstream PEs (and mixed sets) to the implementer. | ambiguity | none found |
| RA-0371 | 5.1.3 | "Another procedure, which SHOULD be implemented, is to use the Installed UMH Route as the Selected UMH Route." | Three procedures are given (one MUST and default, one MUST but disabled, one SHOULD) without a mechanism for PEs to agree which is in use; the text itself notes that mixing them leads to "steady state duplication of traffic" unless wrong-PE discard (9.1.1) is in place. Consistency is left to configuration. | ambiguity | none found |

### RFC 6514: BGP Encodings and Procedures for Multicast in MPLS/BGP IP VPNs {#ra_rfc6514}

Depth: deep. Errata: checked (checked: 3 (all held: 5724 technical, 3801 and 3802 editorial)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0087 | 11.1.3 | "The Source AS field in the C-multicast route is set to value of the Originating Router's IP Address field of the found Intra-AS I-PMSI A-D route." | The Source AS field is 4 octets; with RFC 6515 the Originating Router's IP Address may be a 16-octet IPv6 address, which cannot be stored. The held erratum limits the rule to IPv4 Originating Router addresses; nothing says what to use for IPv6. | error | 5724 (Held) |
| RA-0088 | 4.1, 4.2 | "Usage of Intra-AS I-PMSI A-D routes is described in Section 9.2." | The two references are swapped: intra-AS usage is section 9.1, inter-AS usage 9.2. | editorial | 3801, 3802 (Held) |

### RFC 6515: IPv4 and IPv6 Infrastructure Addresses in BGP Updates for Multicast VPN {#ra_rfc6515}

Depth: deep (read in full). Errata: no verified errata in the index; page not read. Updates: RFC 6514.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0372 | 2 | "If the length of the next hop address is neither 4 nor 16, the MP_REACH_NLRI attribute MUST be considered to be "incorrect", and MUST be handled as specified in Section 7 of [BGP-MP]." | An IPv6 next hop of 32 octets (global plus link-local, RFC 2545) is common on BGP sessions over IPv6; this text makes such an MCAST-VPN UPDATE an MP_REACH_NLRI error, which under RFC 4760 Section 7 resets the session (RFC 7606 later softens the handling but does not change what is "incorrect"). Whether a 32-octet next hop is intended to be an error for MCAST-VPN routes is not stated. Item 4 also has the typo "is following by". | ambiguity | not checked |

### RFC 6625: Wildcards in Multicast VPN Auto-Discovery Routes {#ra_rfc6625}

Depth: deep (3, 4 in full). Errata: checked (checked: 1 (5605 held, technical, 3.2.1: "Otherwise" chain lets only one S-PMSI route match)). Updates: RFC 6514.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0373 | 3.2.1 | "Otherwise, if there is an installed S-PMSI A-D route originated by PE2, whose NLRI contains (C-*,C-*), then (C-S,C-G) matches that route." | The "Otherwise" chain makes the match exclusive: a (C-S,C-G) state matches only the most specific installed S-PMSI route from its upstream PE. Erratum 5605 (held) argues that several routes can match at once (for example while switching from a (C-*,C-*) to a (C-S,C-G) S-PMSI), and the AD note points to the later changes in RFC 7582, RFC 7900 and RFC 8534. A receiver that joins only the best match may lose packets while the ingress moves the flow between trees. | ambiguity | 5605 (Held) |

### RFC 7385: IANA Registry for P-Multicast Service Interface (PMSI) Tunnel Type Code Points {#ra_rfc7385}

Depth: light. Errata: no verified errata in the index; page not read. Updates: RFC 6514.

Nothing notable found at this depth.

### RFC 7442: Carrying Protocol Independent Multicast - Sparse Mode (PIM-SM) in Any-Source Multicast (ASM) Mode Trees over Multipoint LDP (mLDP) {#ra_rfc7442}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0374 | 3.4 | "The LSR MUST keep the (S,G,RPT-bit) downstream state machine in the Prune state for as long as (a) ... (b) ... (c) ..." | In the PIM-SM (S,G,rpt) downstream state machine (RFC 4601 4.5.4, now RFC 7761) the Prune state is held by an Expiry Timer refreshed by received Prune(S,G,rpt) messages; the "as if received" prune has no refresh, and the text does not say whether the Expiry Timer is disabled, set to infinity, or refreshed internally. The section also cites RFC 4601, which RFC 7761 has since obsoleted. | ambiguity | not checked |

### RFC 7524: Inter-Area Point-to-Multipoint (P2MP) Segmented Label Switched Paths (LSPs) {#ra_rfc7524}

Depth: part. Errata: no errata page found by search (not confirmed). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0375 | 4, 5.1.3 | "This document defines a new Transitive IPv4-Address-Specific Extended Community Sub-Type: "Inter-Area P2MP Next-Hop". / these routes MUST carry the Inter-Area P2MP Segmented Next-Hop Extended Community." | The community is registered as "Inter-Area P2MP Next-Hop" but is called "Inter-Area P2MP Segmented Next-Hop Extended Community" everywhere else, and once "P2MP Next-Hop Extended Community". Section 4 also reads "may be the loopback address or the PE, ABR, or ASBR" for "of the PE, ABR, or ASBR". | editorial | none found |

### RFC 7761: Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised) {#ra_rfc7761}

Depth: deep. Errata: checked (checked: 4 (5342 verified technical, 7857 verified editorial, 5367 held technical, 5343 rejected)). Obsoletes: RFC 4601.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0089 | 4.4.2, 4.11 | "set KeepaliveTimer(S,G) to RP_Keepalive_Period;" | The RP pseudocode sets the (S,G) Keepalive Timer to RP_Keepalive_Period alone, while section 4.11 says the KAT "is set to max(Keepalive_Period, RP_Keepalive_Period) when a Register-Stop is sent". With default timers RP_Keepalive_Period (3 x Register_Suppression_Time + Register_Probe_Time = 185 s) is shorter than Keepalive_Period (210 s), so the two readings differ. The verified erratum makes the pseudocode use the maximum; 5367 asks for the same in the restart value. | contradiction | 5342 (Verified), 5367 (Held), 5343 (Rejected) |
| RA-0090 | 4.6.5 | "(AssertWinnerMetric(S,G,I) is better than spt_assert_metric(S,I) )" | Unbalanced / excess parentheses in the lost_assert(S,G,I) pseudocode; no change of meaning. | editorial | 7857 (Verified) |

### RFC 9026: Multicast VPN Fast Upstream Failover {#ra_rfc9026}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9776: Internet Group Management Protocol, Version 3 {#ra_rfc9776}

Depth: deep (sections 4, 6, 7.3, 8 and Appendix C in full; host-side 5 and 7.2 scanned). Errata: not checked. Obsoletes: RFC 3376. Updates: RFC 2236.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0376 | 8.12 vs 9777 9.12 | "This value SHOULD be [Robustness Variable] times [Query Interval] plus (10 times the Max Response Time in the last received Query Message)." | Section 4.1.1 defines Max Response Time "in units of 1/10 second", so converting it to seconds divides by 10; "10 times the Max Response Time" gives a value 100 times too large if read in seconds, or one second-unit per 1/100 s if read in units. The MLDv2 republication (RFC 9777 9.12) keeps "plus ([Query Response Interval])" for the same timer, so the two documents, updated together, disagree on the formula. The text also turns the RFC 3376 MUST into a SHOULD and says hosts should use default values for a figure that depends on the last received Query. | error | none found; **proposed erratum below** |
| RA-0377 | 8.4, 8.13 | "This value MUST be ([Robustness Variable] times [Query Interval]) plus (2 * [Query Response Interval]). (8.4) / This value MUST be ([Robustness Variable] times [Query Interval]) plus [Query Response Interval]. (8.13)" | In RFC 3376 the Older Host Present Interval equalled the Group Membership Interval, so a group kept its older-version compatibility mode for as long as the older host's membership lasted. With 8.4 changed (Erratum 6725) and 8.13 unchanged, compatibility mode now ends one Query Response Interval before the membership created by the older report expires; during that window IGMPv3 BLOCK and TO_IN records are processed for a group whose only member may be an IGMPv1/v2 host. Whether 8.13 was meant to follow 8.4 is not said. RFC 9777 9.4 / 9.13 has the same split. | ambiguity | none found |

Proposed erratum RA-0376 (RFC 9776, Section 8.12 vs 9777 9.12; type: Technical):

```
Original Text
-------------
   This value SHOULD be [Robustness Variable] times [Query Interval]
   plus (10 times the Max Response Time in the last received Query
   Message).

Corrected Text
--------------
   This value SHOULD be [Robustness Variable] times [Query Interval]
   plus (the Max Response Time in the last received Query Message,
   converted to seconds, i.e., one tenth of its value in units of
   1/10 second).

Notes
-----
   RFC 3376 Erratum 4375 (Held for Document Update) proposed "plus
   (one Query Response Interval in the last Query received)", i.e.
   the received Max Response Time converted to seconds; the
   published text multiplies by 10 instead of dividing. Whichever
   formula is intended, IGMPv3 and MLDv2 should agree.
```

### RFC 9777: Multicast Listener Discovery Version 2 (MLDv2) for IPv6 {#ra_rfc9777}

Depth: deep (sections 5, 7, 8 router parts, 9; host-side scanned). Errata: not checked. Obsoletes: RFC 3810. Updates: RFC 2710.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0378 | 9.5 | "This value MUST be ([Robustness Variable] times ([Query Interval]) plus (0.5 times [Query Response Interval])." | Unbalanced parentheses (three opening, two closing before "plus"); RFC 9776 8.5 has the correct form. | editorial | none found; **proposed erratum below** |

Proposed erratum RA-0378 (RFC 9777, Section 9.5; type: Editorial):

```
Original Text
-------------
   This value MUST be ([Robustness Variable] times ([Query
   Interval]) plus (0.5 times [Query Response Interval]).

Corrected Text
--------------
   This value MUST be ([Robustness Variable] times [Query Interval])
   plus (0.5 times [Query Response Interval]).

Notes
-----
   Editorial.
```

### Other RFCs in this area {#ra_mcast_other}

Mechanical checks only, no finding: RFC 3376 (Internet Group Management Protocol, Version 3), RFC 3810 (Multicast Listener Discovery Version 2 (MLDv2) for IPv6).

## BFD, LSP ping, measurement and time {#ra_oam}

30 RFCs in this area (20 deep, 3 part, 1 read, 5 light, 1 scan); 42 findings, 14 of them proposed errata.

### RFC 2330: Advanced Network & Services {#ra_rfc2330}

Depth: light (only (IPPM framework, informational; IPPM framework, Informational; TWAMP set, no protocol mechanics). Errata: not checked. 

Nothing notable found at this depth.

### RFC 4656: A One-way Active Measurement Protocol (OWAMP) {#ra_rfc4656}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 5357: A Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc5357}

Depth: deep. Errata: checked (checked: 13 (6 verified, 4 of them technical; 6 held; 1 rejected)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0091 | 4.1.2, 4.2.1 | "unauthenticated mode is 41 octets, and 104 octets in both" | The minimum authenticated / encrypted TWAMP-Test packet is 112 octets, not 104, and sender padding is at least 64 octets, not 56 ("least 56 octets"). Implementations sizing buffers or validating lengths from the text reject valid packets. | error | 5045, 5046 (Verified) |
| RA-0092 | 8.1, 8.2 | "document.  Thus, this registry may contain sixteen possible values." | The Command Number field is one octet, so the registry has 256 values. | error | 1593 (Verified) |
| RA-0379 | 4.2 | "In authenticated or encrypted mode, decrypt the appropriate sections of the packet body (first block (16 octets) for authenticated, 96 octets for encrypted), and then check integrity of sections covered by the HMAC." | The packet the Session-Reflector receives is a Session-Sender packet, whose format is that of OWAMP-Test (Section 4.1.2, referring to RFC 4656 4.1.2): in encrypted mode only "the first two blocks (32 octets) are encrypted" and covered by the HMAC (RFC 4656 4.1.2). 96 octets is the coverage of the Session-Reflector's own packet (Section 4.2.1). A reflector decrypting 96 octets of a sender packet would decrypt the HMAC and padding and fail the integrity check. | error | none found; **proposed erratum below** |
| RA-0380 | 4.2 vs 4.2.1 | "Copy the packet sequence number into the corresponding reflected packet to the Session-Sender. (4.2) / The Sequence Number generated by the Session-Reflector is independent from the sequence number of the arriving packets. (4.2.1)" | The 4.2 step reads as copying the received sequence number into the reflected Sequence Number field, while 4.2.1 makes that field the reflector's own counter and puts the received value in Sender Sequence Number. Appendix I (TWAMP Light) then lets a stateless reflector copy it, which RFC 8762 later formalised as "stateless" mode. | ambiguity | related: 1590 (Verified) scopes the reflector Sequence Number per session |
| RA-0381 | 3.8 | "If the Accept-Session message was not transmitted at all (for whatever reason, including failure of the TCP connection used for TWAMP-Control), the results of all TWAMP-Test sessions spawned by this TWAMP-Control session MAY be considered invalid." | The paragraph discusses the Accept field of the Stop-Sessions command; the message that may not have been transmitted is the Stop-Sessions message, not Accept-Session (which is the Server's reply to Request-TW-Session). | editorial | none found (1594 concerns the HMAC wording of 3.8); **proposed erratum below** |
| RA-0382 | 4.2.1, 6 | "Thus, in authenticated mode, HMAC covers the first block (16 octets); in encrypted mode, HMAC covers the first six blocks (96 octets)." | Security gap: In authenticated mode the reflected packet's first block holds only the reflector Sequence Number and MBZ; the Timestamp, Receive Timestamp, Sender Sequence Number, Sender Timestamp and Sender TTL are neither encrypted nor integrity-protected, so an on-path attacker can alter every value used to compute delay and loss without detection. Section 6 (Security Considerations) does not state this limitation of authenticated mode. | error | none found |

Proposed erratum RA-0379 (RFC 5357, Section 4.2; type: Technical):

```
Original Text
-------------
   (first block (16 octets) for authenticated, 96 octets for
   encrypted)

Corrected Text
--------------
   (first block (16 octets) for authenticated, first two blocks (32
   octets) for encrypted, as for OWAMP-Test packets [RFC4656])

Notes
-----
   The 96-octet figure applies to the reflected packet format of
   Section 4.2.1; Session-Sender packets follow RFC 4656 Section
   4.1.2.
```

Proposed erratum RA-0381 (RFC 5357, Section 3.8; type: Editorial):

```
Original Text
-------------
   If the Accept-Session message was not transmitted at all

Corrected Text
--------------
   If the Stop-Sessions message was not transmitted at all

Notes
-----
   The preceding sentence concerns the Accept field of
   Stop-Sessions.
```

### RFC 5618: Mixed Security Mode for the Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc5618}

Depth: deep (TWAMP set). Errata: no verified errata in the index; page not read. Updates: RFC 5357.

Nothing notable found at this depth.

### RFC 5880: Bidirectional Forwarding Detection (BFD) {#ra_rfc5880}

Depth: deep. Errata: checked (checked: 8 (4 verified: 2530, 7082, 7083 technical, 6926 editorial; 3 held: 5205, 7240 technical, 4410 editorial; 1 rejected)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0093 | 6.7.3, 6.7.4 | "Otherwise (bfd.AuthSeqKnown is 0), bfd.AuthSeqKnown MUST be set to 1, and bfd.RcvAuthSeq MUST be set to the value of the received Sequence Number field." | In the MD5 and SHA1 procedures the sequence variables are updated before the digest is checked, so a forged packet with a bad digest can still move bfd.RcvAuthSeq and make later genuine packets fall outside the window. The errata move the update after a successful check. Security gap in the original text. | error | 7082, 7083 (Verified) |
| RA-0094 | 6.8.4 | "Detection Time passes without receiving a BFD Control packet from the remote system, and bfd.SessionState is Init or Up, the session has gone down" | In Down state an expired Detection Time changes nothing here, although 6.8.1 requires bfd.RemoteDiscr to be zeroed whenever a Detection Time passes without a valid packet, so the timer must still run in Down. The held erratum would drop the "Init or Up" condition and always set Diag 1; that is not yet the text. | ambiguity | 5205 (Held) |
| RA-0095 | 6.8.1 | "The diagnostic code specifying the reason for the most recent change in the local session state." | Whether bfd.LocalDiag returns to 0 when the session comes Up again is not said; implementations differ (some keep the last failure reason while Up). The erratum was held for a future revision without text. | ambiguity | 7240 (Held) |

### RFC 5881: Bidirectional Forwarding Detection (BFD) for IPv4 and IPv6 (Single Hop) {#ra_rfc5881}

Depth: deep. Errata: checked (checked: 1 (2293 verified, technical: IANA port 3875 for 3785)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0383 | 8 | "Ports 3784 and 3875 were assigned by IANA for use with the BFD Control and BFD Echo protocols, respectively." | The Echo port is 3785 (Section 4: "destination UDP port 3785"); 3875 in Section 8 is a transposition, already corrected by verified erratum 2293. | error | 2293 (Verified) |
| RA-0384 | 6 | "On a point-to-point link, the source address of a BFD Control packet MUST NOT be used to identify the session. This means that the initial BFD packet MUST be accepted with any source address" | Section 6 has one rule for "a multiaccess network" (addresses on the subnet) and another for "a point-to-point link" (the session MUST NOT be identified by source address; the source address may change). Which rule applies to a broadcast medium operated as a point-to-point circuit (for example an Ethernet link that an IGP runs in point-to-point mode, or an unnumbered interface) is not stated, and RFC 5880 6.8.6 adds that a nonzero Your Discriminator selects the session on its own. An implementation that also checks the source address on such links will never bring up, or will drop, a session whose peer sources from another address on the link. | ambiguity | none found |
| RA-0385 | 6, 5 | "Note that the TTL/Hop Limit check described in section 5 (or the use of authentication) precludes the BFD packets from having come from any source other than the immediate neighbor." | Section 5 makes the TTL check optional ("MAY be discarded") when authentication is in use, and authentication by itself proves the key holder, not that the sender is one hop away. The sentence therefore overstates what authentication alone gives for the one-hop property. | ambiguity | none found |

### RFC 5882: Generic Application of Bidirectional Forwarding Detection (BFD) {#ra_rfc5882}

Depth: deep. Errata: checked (checked: 1 (4812 held, editorial: "Label Switched Paths" for IS-IS Link State PDUs in 10.1.2)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0386 | 4.3.2.2, 10.1.2 | "it is likely that the BFD session will time out prior to the onset of Graceful Restart, in which case a topology change SHOULD be signaled in the control protocol as specified in Section 3.2." | Section 3.2 is "AdminDown State"; the procedure for signalling a topology change on a BFD failure is Section 4.2 (4.2.1, 4.2.2). Section 10.1.2 has two more stale references: "The basic mechanisms are covered in Section 3 above" (reactions are in Section 4.2) and "The appropriate mechanisms outlined in Section 3.3 should be used" for planned restart, which are in Section 4.3.2 (3.3 is hitless establishment). The references look left over from an earlier numbering. | error | none found (4812 is on a different sentence of 10.1.2); **proposed erratum below** |
| RA-0387 | 10.1.2, 4.3.2.1 | "OSPF has a planned restart signaling mechanism, whereas IS-IS does not." | The statement routes IS-IS to 4.3.2.2 (no planned restart signalling); RFC 8706 has since added planned restart signalling to IS-IS, so 4.3.2.1 applies to IS-IS routers that support it. The non-normative section is outdated rather than wrong at publication. | ambiguity | none found |
| RA-0388 | 3.2, 4.2 | "If a client does not have any independent means of liveness detection, a system SHOULD indicate a connectivity failure to a client, and assume the semantics of Down state" | Section 3.2 treats AdminDown as Down for clients without independent liveness detection, while 4.2 tells clients to take no action on Up to AdminDown without that qualification. For clients such as static routes (Section 5) or BFD for LSPs the two texts point opposite ways; which client classes count as having "independent means" is left to the implementer. | ambiguity | none found |

Proposed erratum RA-0386 (RFC 5882, Section 4.3.2.2, 10.1.2; type: Technical):

```
Original Text
-------------
   (4.3.2.2) ... a topology change SHOULD be signaled in the control
   protocol as specified in Section 3.2. (10.1.2) The basic
   mechanisms are covered in Section 3 above. ... The appropriate
   mechanisms outlined in Section 3.3 should be used.

Corrected Text
--------------
   (4.3.2.2) ... as specified in Section 4.2. (10.1.2) The basic
   mechanisms are covered in Section 4.2 above. ... The appropriate
   mechanisms outlined in Section 4.3 should be used.

Notes
-----
   Section 3.2 (AdminDown) and Section 3.3 (hitless establishment)
   do not describe topology-change signalling or graceful restart
   interaction; Sections 4.2 and 4.3 do.
```

### RFC 5883: Bidirectional Forwarding Detection (BFD) for Multihop Paths {#ra_rfc5883}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0389 | 5, 3 | "The encapsulation of BFD Control packets for multihop application in IPv4 and IPv6 is identical to that defined in [BFD-1HOP], except that the UDP destination port MUST have a value of 4784." | Taken literally, "identical" imports RFC 5881 Section 5 (send with TTL 255, discard unless received TTL is 255 when not authenticated), which Section 3 says "obviously does not work across multiple hops". No transmit TTL and no receive check replace it, so implementations choose their own (send 255 and accept above a configured minimum, or no check), and an unauthenticated multihop session has no anti-spoofing rule at all. | ambiguity | not checked |

### RFC 5884: Bidirectional Forwarding Detection (BFD) for MPLS Label Switched Paths (LSPs) {#ra_rfc5884}

Depth: deep. Errata: checked (checked: 3 (5085 verified technical; 5087, 5088 held editorial)). Updates: RFC 1122.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0096 | 6 | "The egress LSR MAY respond with an LSP Ping Echo reply message that carries the local discriminator assigned by it for the BFD session." | The MAY can be read as making the Echo Reply itself optional, while RFC 8029 requires the egress to report the verification result; the erratum makes only the discriminator optional. RFC 7726 also clarifies the bootstrap procedure. | ambiguity | 5085 (Verified) |
| RA-0097 | 7 | "from the 0:0:0:0:0:FFFF:7F00/104 range for IPv6 with the following" | "0:0:0:0:0:FFFF:7F00/104" has only seven groups and is not a valid IPv6 prefix; 0:0:0:0:0:FFFF:7F00:0/104 (::ffff:127.0.0.0/104) is meant. Erratum 5088 also corrects "[5085]" to RFC 5885. | editorial | 5087 (Held) |

### RFC 5885: Bidirectional Forwarding Detection (BFD) for the Pseudowire Virtual Circuit Connectivity Verification (VCCV) {#ra_rfc5885}

Depth: deep. Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0390 | 3.3, 4 | "BFD CV Types used for fault detection and status signaling (i.e., CV Types 0x08 and 0x20) SHOULD NOT be used when a control protocol such as LDP [RFC4447] or L2TPV3 [RFC3931] is available" | Section 4 ranks 0x20 first and 0x08 third "after applying the rules in Section 3.3", but rule 1 of 3.3 is only a SHOULD NOT. Each PE selects on its own; if one PE drops 0x20 / 0x08 under rule 1 and its peer does not, the two ends of an LDP-signalled PW select different CV types (0x10 and 0x20, or 0x04 and 0x08). The encapsulation is the same, so the session comes up, but the ends disagree on whether BFD carries AC / PW fault status. The text does not say whether rule 1 is applied before the ranking on both ends. | ambiguity | not checked |

### RFC 5905: Network Time Protocol Version 4: Protocol and Algorithms Specification {#ra_rfc5905}

Depth: light (section 6 timestamp formats only, as used by STAMP; diagram hit at line 1018 is the LI / VN / Mode header, field widths 2 + 3 + 3 + 8 + 8 + 8 = 32, not a defect). Errata: errata exist; not read. Obsoletes: RFC 1305, RFC 4330.

Nothing notable found at this depth.

### RFC 5938: Individual Session Control Feature for the Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc5938}

Depth: deep (TWAMP set). Errata: errata exist; not read. Updates: RFC 5357.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0391 | 3.2, 3.4 | "Start-N-Ack messages SHALL have the format defined in the next session." | "Next session" should be "next section" (also for Stop-N-Ack in 3.4). In 3.4 the sentence "The SID is as defined in Section 3.5 of OWAMP [RFC4656] (and TWAMP), and the value MUST be one or greater" attaches the "one or greater" rule to the SID, while 3.2 states it for the Number of Sessions field; the Number of Sessions is meant. | editorial | none found; **proposed erratum below** |

Proposed erratum RA-0391 (RFC 5938, Section 3.2, 3.4; type: Editorial):

```
Original Text
-------------
   Start-N-Ack messages SHALL have the format defined in the next
   session.
   The SID is as defined in Section 3.5 of OWAMP [RFC4656] (and
   TWAMP), and the value MUST be one or greater.

Corrected Text
--------------
   Start-N-Ack messages SHALL have the format defined in the next
   section.
   The SID is as defined in Section 3.5 of OWAMP [RFC4656] (and
   TWAMP). The value of the Number of Sessions field MUST be one or
   greater.

Notes
-----
   Editorial.
```

### RFC 6038: Two-Way Active Measurement Protocol (TWAMP) Reflect Octets and Symmetrical Size Features {#ra_rfc6038}

Depth: scan (mechanical checks only). Errata: errata exist; not read. Updates: RFC 5357.

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

### RFC 6425: Detecting Data-Plane Failures in Point-to-Multipoint MPLS - Extensions to LSP Ping {#ra_rfc6425}

Depth: deep (3, 4.1, 4.2 in full; 4.3 by MUST/SHOULD). Errata: checked (checked: 1 (3306 verified, editorial, 3.1.1: sub-type 18 length 56 should be 44)). Updates: RFC 4379.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0392 | 3.1.1 | "18         56                RSVP P2MP IPv6 Session" | The RSVP P2MP IPv6 Session sub-TLV replaces the 16-octet IPv6 tunnel end point of RFC 4379 by a 4-octet P2MP ID, giving 44 octets; 56 is carried over from RFC 4379 and corrected by verified erratum 3306. | error | 3306 (Verified) |
| RA-0393 | 3.2.1 | "If a node receives these TLVs in an echo request carrying Multicast LDP, then it will not respond since it is unaware of whether it lies on the path to the address in the sub-TLV." | The same section says a node "MUST respond if the node lies on the path to the address in the sub-TLV". An mLDP egress or bud node whose own address is in the Egress Address sub-TLV knows that it lies on that path, so the blanket "will not respond" for Multicast LDP contradicts the MUST for that node. | contradiction | none found |

### RFC 6426: MPLS On-Demand Connectivity Verification and Route Tracing {#ra_rfc6426}

Depth: deep (2, 3 in full; 4 by MUST/SHOULD). Errata: errata exist; not read. Updates: RFC 4379.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0099 | 7.2 | "22       Static LSP              this document (Section 2.4.1)" | The IANA table points to sections 2.4.1 and 2.4.2, which do not exist; the Static LSP and Static Pseudowire sub-TLVs are defined in 2.3.1 and 2.3.2. | error | not checked; **proposed erratum below** |
| RA-0394 | 2.1, 2.1.1 | "5         Non IP                       12 ... The new address type is also applicable to the Detailed Downstream Mapping (DDMAP) TLV defined in [RFC6424]." | K is the length of the initial fixed part of the mapping TLV. For the DSMAP, the Non IP layout of Figure 2 (MTU / Address Type / DS Flags, Ingress IF_Num, Egress IF_Num) is 12 octets, the same as IPv4 (K = 12 in RFC 8029 for the DSMAP). The DDMAP adds Return Code, Return Subcode and Sub-tlv Length, which is why its IPv4 K is 16; a single K of 12 "also applicable to" the DDMAP is therefore 4 octets short for that TLV. RFC 8029 copies 12 into its DDMAP Address Type registry, so the inconsistency persists. | contradiction | not checked; **proposed erratum below** |
| RA-0395 | 2.2.2, 2.2.3 | "If more than one such TLV is present in an on-demand CV request packet, then error 1 (Malformed echo request received; see Section 3.1 of [RFC4379]) MUST be returned, if it is possible to unambiguously identify the source of the packet." | For the Source Identifier TLV, a request carrying two Source Identifiers has, by construction, no unambiguous source when IP is not used, so the MUST never applies there and the request is silently dropped; the same sentence was copied to the Destination Identifier TLV, where the condition should concern the request's source, as written. What "unambiguously identify" means (an IP header, the reverse LSP of the ACH channel) is not stated. | ambiguity | not checked |
| RA-0396 | 3.4.1 | "The Validate FEC Stack (V) flag MAY be set in the echo response when reverse-path connectivity verification is being performed." | In RFC 4379 the V flag is a request flag ("the sender wants FEC validation"); its meaning in an echo response is not defined, and nothing says what the requester does with it. | ambiguity | not checked |

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

Proposed erratum RA-0394 (RFC 6426, Section 2.1, 2.1.1; type: Technical):

```
Original Text
-------------
   5         Non IP                       12

Corrected Text
--------------
   5         Non IP                       12 (DSMAP), 16 (DDMAP)

Notes
-----
   DDMAP K values are 4 larger than DSMAP K values for the same
   address type (RFC 8029: IPv4 12 vs 16, IPv6 numbered 36 vs 40)
   because of the Return Code, Return Subcode and Sub-tlv Length
   fields.
```

### RFC 7110: Return Path Specified Label Switched Path (LSP) Ping {#ra_rfc7110}

Depth: deep. Errata: checked (checked: 1 (4197 verified, technical, 4: "one or more" sub-TLVs should be "zero or more")). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0397 | 4, 5.1 | "The Reply Path TLV includes one or several reply path sub-TLV(s) to identify the return path(s) the egress LSR should use for its reply." | Verified erratum 4197 corrects Section 4 ("one or more nested sub-TLVs") to zero or more, matching 4.2 (A and B bits need no sub-TLV; "can contain zero, one or more"). The same "one or several" wording remains in 5.1, and 5.3 adds that a pure IP return path carries no sub-TLVs. A receiver applying 5.1 literally would treat a Reply Path TLV with only the B bit as malformed. | contradiction | 4197 (Verified, covers Section 4 only); **proposed erratum below** |
| RA-0398 | 4.1 | "The value of the Reply via Specified Path mode is 5 (This has been allocated by IANA using early allocation and is to be confirmed by IANA)." | Early-allocation wording left in the published RFC; Section 7.3 records the permanent assignment. | editorial | none found |

Proposed erratum RA-0397 (RFC 7110, Section 4, 5.1; type: Technical):

```
Original Text
-------------
   The Reply Path TLV includes one or several reply path sub-TLV(s)
   to identify the return path(s) the egress LSR should use for its
   reply.

Corrected Text
--------------
   The Reply Path TLV includes zero or more reply path sub-TLV(s) to
   identify the return path(s) the egress LSR should use for its
   reply; no sub-TLV is needed when the A or B flag is set.

Notes
-----
   Erratum 4197 fixed the same statement in Section 4. Section 4.2
   permits zero sub-TLVs and says sub-TLVs SHOULD be ignored when A
   or B is set.
```

### RFC 7130: Bidirectional Forwarding Detection (BFD) on Link Aggregation Group (LAG) Interfaces {#ra_rfc7130}

Depth: deep. Errata: checked (checked: 2 (both held, editorial IEEE names)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0399 | 2.2 | "The micro-BFD session's negotiation MUST follow the same procedures defined in [RFC5880] and [RFC5881]. ... At least one system MUST take the Active role (possibly both)." | RFC 5881 Section 3 requires that "both sides of a session MUST take the 'Active' role"; this section imports RFC 5881 and in the same paragraph allows one side to be Passive. A Passive member-link endpoint is permitted by RFC 7130 but not by the procedures it says MUST be followed. | contradiction | none found |
| RA-0400 | 3 | "The micro-BFD sessions for a particular LAG member link MUST be requested when a member link state is either Distributing or Standby." | "Distributing" and "Standby" are LACP states; for a statically configured LAG without LACP the trigger for creating and deleting the sessions is not defined. Combined with the rule that a member "MUST NOT be used by the load balancer until all the micro-BFD sessions ... are in Up state", whether a static member starts in or out of the load-balancing table is left to the implementer. | ambiguity | none found |

### RFC 7506: IPv6 Router Alert Option for MPLS Operations, Administration, and Maintenance (OAM) {#ra_rfc7506}

Depth: deep. Errata: not checked. Updates: RFC 4379.

Nothing notable found at this depth.

### RFC 7679: A One-Way Delay Metric for IP Performance Metrics (IPPM) {#ra_rfc7679}

Depth: light (one-way delay metric; TWAMP set, definitions only). Errata: not checked. Obsoletes: RFC 2679.

Nothing notable found at this depth.

### RFC 7680: A One-Way Loss Metric for IP Performance Metrics (IPPM) {#ra_rfc7680}

Depth: light (IPPM one-way loss metric; one-way loss metric; TWAMP set, definitions only). Errata: not checked. Obsoletes: RFC 2680.

Nothing notable found at this depth.

### RFC 7717: IKEv2-Derived Shared Secret Key for the One-Way Active Measurement Protocol (OWAMP) and Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc7717}

Depth: part (TWAMP set: sections 4, 5.1-5.4, 7 read; key derivation formula not re-derived). Errata: not checked. Updates: RFC 4656, RFC 5357.

Nothing notable found at this depth.

### RFC 7726: Clarifying Procedures for Establishing BFD Sessions for MPLS Label Switched Paths (LSPs) {#ra_rfc7726}

Depth: deep. Errata: no errata page found by search (not confirmed). Updates: RFC 5884.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0401 | 2.3, 2.4 | "it MAY transmit BFD packets indicating the State as Down(1), diagnostic code AdminDown(7) detectMultiplier number of times.  Upon receiving such a packet, the egress LSR MAY remove the BFD session, without triggering a change of state." | Under RFC 5880 6.8.6 a session in Up that receives State Down moves to Down, so a packet with State Down(1) does trigger a state change at the egress; the RFC 5880 way to stop a session without a failure indication is State AdminDown(0) (with diagnostic 7), which Section 2.4 itself refers to ("a graceful transition to AdminDown state"). An egress that implements RFC 5880 strictly will report a failure (and its clients may react) before removal. | contradiction | none found; **proposed erratum below** |
| RA-0402 | 2.1 | "Ensure the uniqueness of the <MPLS LSP, FEC, Remote Discriminator> tuple." | For FECs with many ingress LSRs (LDP prefix FECs, which are multipoint-to-point), two ingresses may choose the same discriminator for the same FEC; the tuple does not include the ingress, so the egress would treat the second bootstrap as the existing session. The ingress address (source of the echo request) is needed to make the tuple unique. "Reset this to zero" in Section 2.3 also has no clear antecedent (Your Discriminator, presumably). | ambiguity | none found |
| RA-0403 | 2.1 | "When the egress LSR disallows the creation of a BFD session due to policy, it MUST drop the MPLS Echo request message." | RFC 5884 erratum 5085 (verified) makes the egress LSR's echo reply to a bootstrap echo request mandatory, so that the egress reports LSP Ping verification status to the ingress, with only the BFD discriminator optional. RFC 7726 2.1, which updates RFC 5884 Section 4 to 6, requires the egress to drop the echo request when policy refuses the session. The two texts now disagree about whether a refused bootstrap is answered. | contradiction | RFC 5884: 5085 (Verified); **proposed erratum below** |

Proposed erratum RA-0401 (RFC 7726, Section 2.3, 2.4; type: Technical):

```
Original Text
-------------
   it MAY transmit BFD packets indicating the State as Down(1),
   diagnostic code AdminDown(7) detectMultiplier number of times.

Corrected Text
--------------
   it MAY transmit BFD packets indicating the State as AdminDown(0),
   diagnostic code Administratively Down(7), detectMultiplier number
   of times.

Notes
-----
   RFC 5880 Section 6.8.6 moves a session from Up to Down on receipt
   of State Down; State AdminDown is the value that avoids
   signalling a failure (RFC 5880 Section 6.8.16), as Section 2.4 of
   this document also says.
```

Proposed erratum RA-0403 (RFC 7726, Section 2.1; type: Technical):

```
Original Text
-------------
   When the egress LSR disallows the creation of a BFD session due
   to policy, it MUST drop the MPLS Echo request message.

Corrected Text
--------------
   When the egress LSR disallows the creation of a BFD session due
   to policy, it MUST reply to the MPLS Echo request as specified in
   [RFC8029] without including a BFD Discriminator TLV, and MUST NOT
   create the session.

Notes
-----
   Erratum 5085 on RFC 5884 Section 6 states that the echo reply is
   mandatory and only the BFD discriminator in it is optional.
```

### RFC 7750: Differentiated Service Code Point and Explicit Congestion Notification Monitoring in the Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc7750}

Depth: deep (TWAMP set). Errata: no errata page found by search (not confirmed). Updates: RFC 5357.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0404 | 2.2.1 | "the six (least-significant) bits of the Differentiated Service field MUST be copied from the received Session-Sender test packet into the Sender DSCP (S-DSCP) field;" | In the IPv4 TOS / IPv6 Traffic Class octet the DSCP is the six most significant bits and ECN the two least significant ones (RFC 2474, RFC 3168). "Least-significant" is only correct if "Differentiated Service field" means the 6-bit DS field of RFC 3260; read against the 8-bit octet, an implementer copies ECN plus four DSCP bits. Figure 1 places S-DSCP in bits 0-5 and S-ECN in bits 6-7 of the new octet, which matches the most-significant reading. | ambiguity | none found; **proposed erratum below** |

Proposed erratum RA-0404 (RFC 7750, Section 2.2.1; type: Technical):

```
Original Text
-------------
   the six (least-significant) bits of the Differentiated Service
   field MUST be copied

Corrected Text
--------------
   the six bits of the DSCP (the most significant six bits of the
   IPv4 TOS octet or IPv6 Traffic Class octet [RFC2474]) MUST be
   copied

Notes
-----
   Correct only under the RFC 3260 6-bit DS field definition; Figure
   1 and RFC 3168 suggest the most-significant reading.
```

### RFC 7820: UDP Checksum Complement in the One-Way Active Measurement Protocol (OWAMP) and Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc7820}

Depth: part (TWAMP set: section 3 read). Errata: not checked. 

Nothing notable found at this depth.

### RFC 8029: Detecting Multiprotocol Label Switched (MPLS) Data-Plane Failures {#ra_rfc8029}

Depth: deep. Errata: checked (checked: 5 (7639 verified technical, 7892 verified editorial, 8788 reported technical, 5102 and 5103 held editorial)). Obsoletes: RFC 4379, RFC 6424, RFC 6829, RFC 7537. Updates: RFC 1122.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0100 | 3.4, 3.7, 3.8, A.2 | "If an LSR does not know the IP address of its neighbor, then it MUST set the Address Type to either IPv4 Unnumbered or IPv6 Unnumbered." | "IPv6 Unnumbered" (Router ID plus interface index) has no defined IPv6 Router ID semantics; the open erratum proposes deprecating the IPv6 Unnumbered address types and also reports a K-octets mismatch in Appendix A.2. Until it is resolved, what to send and accept for IPv6 unnumbered links is unclear. | ambiguity | 8788 (Reported) |

### RFC 8186: Support of the IEEE 1588 Timestamp Format in a Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc8186}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8287: Label Switched Path (LSP) Ping/Traceroute for Segment Routing (SR) IGP-Prefix and IGP-Adjacency Segment Identifiers (SIDs) with MPLS Data Pl {#ra_rfc8287}

Depth: deep. Errata: checked (checked: 3 (6389 verified editorial 5.2 "IPv4 Anycast"; 6101 held editorial 7.2 "Post Office Protocol (POP)"; 5290 rejected technical 5.1 sub-TLV length, later clarified by RFC 8690)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0405 | 7.4 | "Validate that the Node Segment ID is advertised with the No-PHP flag. {  o  When the Protocol is IS-IS, the P-Flag defined in Section 6.1 of [SR-IS-IS] MUST be set to 0." | The P-Flag of RFC 8667 is the No-PHP flag; "advertised with the No-PHP flag" reads as "flag set", while the condition requires P = 0 (PHP performed), which is also what the comment above it says ("advertised with the PHP bit set"). The heading states the opposite of the check. In the IPv6, label-stack-depth > 0 branch the text also says "advertised for the IPv4 Prefix". | contradiction | none found; **proposed erratum below** |
| RA-0406 | 5.3, 7.4 | "If the Protocol field is set to 0, then this field is 4 octets and MUST be set to zero. / Validate that the IGP-Adjacency Segment ID is advertised by the Advertising Node Identifier of the Protocol in the local IGP database" | With Protocol 0 the Advertising and Receiving Node Identifiers are all zeros, so the 7.4 checks "Receiving Node Identifier is the local IGP identifier" and "advertised by the Advertising Node Identifier" cannot succeed (or must be skipped, which the text does not say). Step 4a also gives validation rules only for Adj. Types 1, 4 and 6; Adj. Type 0 (unnumbered, defined in 5.3 and 9.3) has none, so its result depends on the implementation. | ambiguity | none found |

Proposed erratum RA-0405 (RFC 8287, Section 7.4; type: Technical):

```
Original Text
-------------
   -  Validate that the Node Segment ID is advertised with the
   No-PHP flag. {

Corrected Text
--------------
   -  Validate that the Node Segment ID is advertised with the
   No-PHP flag clear (i.e., with penultimate hop popping). {   (and,
   in the fourth branch: "advertised for the IPv6 Prefix")

Notes
-----
   The check (NP-Flag
   P-Flag MUST be 0) and the comment ("advertised with the PHP bit
   set") agree; only the heading line is reversed. The IPv6 branch
   for label-stack-depth > 0 refers to an IPv4 prefix.
```

### RFC 8545: Well-Known Port Assignments for the One-Way Active Measurement Protocol (OWAMP) and the Two-Way Active Measurement Protocol (TWAMP) {#ra_rfc8545}

Depth: read (Sections 1 to 5.1). Errata: not checked. Updates: RFC 4656, RFC 5357.

Nothing notable found at this depth.

### RFC 8762: Simple Two-Way Active Measurement Protocol {#ra_rfc8762}

Depth: deep. Errata: checked (checked via mail archive: 8518 (Reported, Technical, 4.3.1: reflector MUST set Session-Sender TTL to 255 when it cannot read the received TTL / Hop Limit; not yet verified)). 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0407 | 4.6, 4.3, 7 | "A STAMP Session-Reflector ... will transmit the base packet (Figure 5) if it receives a packet smaller than the STAMP base packet. (4.6)" | Security gap: For TWAMP Light interworking the reflector answers a packet shorter than the 44-octet base packet with a 44-octet reply, so its reply can be larger than the request; with UDP and no source validation (unauthenticated mode, Section 4.4 being optional) this makes a reflector an amplifier for spoofed senders. Section 7 discusses load and recommends secured control but does not mention the amplification or require that replies not exceed requests. | error | none found; **proposed erratum below** |
| RA-0408 | 4, 4.3.1 | "That implies that the STAMP Session-Reflector MUST maintain a state for each configured STAMP-Test session, thereby uniquely associating STAMP-Test packets with one such session instance" | The document does not say how a stateful reflector associates a packet with a session (5-tuple, interface, configuration), nor when a session starts or ends; a sender that restarts its Sequence Number at zero on the same 5-tuple cannot be told from a continuing session, so the reflector's counter (Sequence Number, "starts with zero ... for each test session") and the sender's loss computation disagree. RFC 8972 later adds the SSID, which this document lacks. | ambiguity | none found |
| RA-0409 | 4.3, 4 | "The Session-Reflector receives the STAMP-Test packet and verifies it. If the base STAMP-Test packet is validated, the Session-Reflector ... prepares and transmits the reflected test packet" | The checks that make a base packet "validated" are not listed (length, MBZ, HMAC in authenticated mode, Error Estimate), and nothing in the packet indicates whether it is authenticated or not, so the receiver can only know the mode from configuration. | ambiguity | none found |

Proposed erratum RA-0407 (RFC 8762, Section 4.6, 4.3, 7; type: Technical):

```
Original Text
-------------
   (Section 7, new paragraph)

Corrected Text
--------------
   A Session-Reflector that answers packets shorter than the base
   packet (Section 4.6) returns more octets than it receives. Such a
   reflector SHOULD restrict the senders it answers (for example by
   access list or rate limit), since otherwise it can be used to
   amplify traffic towards a spoofed source.

Notes
-----
   Symmetrical size (Section 4) avoids amplification only for
   packets at least as large as the base packet.
```

### RFC 8972: Simple Two-Way Active Measurement Protocol Optional Extensions {#ra_rfc8972}

Depth: part. Errata: checked (checked: 4 (8199 Verified technical 4.4 ECN also copied to the ECN field; 8339 Verified technical 4.7 Length check limited to the Follow-Up Telemetry TLV; 8591 Verified editorial 4.3 timestamp wording; 8592 Verified editorial 4.7 SW Local timestamp placement)). Updates: RFC 8762.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0410 | 4 | "A STAMP Session-Sender that has received a reflected STAMP test packet with extension TLVs MUST validate each TLV: ... * If an implementation of a Session-Reflector does not recognize the Type field value, it MUST include a copy of the TLV in the reflected STAMP packet." | The list is introduced as the Session-Sender's validation of a reflected packet, but its last two items are Session-Reflector rules (unrecognized Type, malformed TLV). The Session-Reflector's handling of the U, M and I flags on receipt is therefore stated only inside the sender's list and in the flag definitions, which a reader of either role can miss. | editorial | none found (errata 8199, 8339, 8591, 8592 concern 4.4, 4.7, 4.3, 4.7); **proposed erratum below** |

Proposed erratum RA-0410 (RFC 8972, Section 4; type: Editorial):

```
Original Text
-------------
   A STAMP Session-Sender that has received a reflected STAMP test
   packet with extension TLVs MUST validate each TLV:

Corrected Text
--------------
   (Split the list:) A STAMP Session-Sender that has received a
   reflected STAMP test packet with extension TLVs MUST validate
   each TLV: [U, M and I items]. A Session-Reflector that supports
   TLVs processes a received extended packet as follows:
   [unrecognized Type and malformed TLV items].

Notes
-----
   Editorial; may overlap with the verified erratum 8591, whose text
   was not re-checked here.
```

## IP, ICMP, neighbour discovery, transport and security {#ra_ip}

77 RFCs in this area (11 deep, 2 part, 16 read, 33 light, 15 scan); 23 findings, 4 of them proposed errata.

### RFC 768: User Datagram Protocol {#ra_rfc768}

Depth: read (whole text). Errata: not checked. 

Nothing notable found at this depth.

### RFC 791: INTERNET PROTOCOL {#ra_rfc791}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 792: Internet Control Message Protocol {#ra_rfc792}

Depth: read (message formats). Errata: not checked. 

Nothing notable found at this depth.

### RFC 826: An Ethernet Address Resolution Protocol -- or -- Converting Network Protocol Addresses to 48.bit Ethernet Address for Transmission on Ethern {#ra_rfc826}

Depth: read (packet reception algorithm and formats). Errata: not checked. 

Nothing notable found at this depth.

### RFC 1042: A Standard for the Transmission of IP Datagrams over IEEE 802 Networks {#ra_rfc1042}

Depth: read (normative statements). Errata: not checked. 

Nothing notable found at this depth.

### RFC 1071: Computing the Internet Checksum {#ra_rfc1071}

Depth: read (Sections 1 to 4; the IEN 45 reprint skimmed). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0411 | 4.1 | "sum += * (unsigned short) addr++;" | The cast converts the address itself to unsigned short and then dereferences it, which is not valid C; a pointer cast "* (unsigned short *) addr" is meant (with addr advanced by 2 octets, not by sizeof(*addr) of whatever type addr has). The odd-byte line "sum += * (unsigned char *) addr;" adds the last octet as the low-order byte, which is correct only on little-endian hosts; Section 2 (A) defines the pad as a zero octet after the last octet, i.e. the high-order byte of the final 16-bit word in network order. The fragment also begins with the stray text "in 6" and has no function header. | error | not checked; **proposed erratum below** |

Proposed erratum RA-0411 (RFC 1071, Section 4.1; type: Technical):

```
Original Text
-------------
   sum += * (unsigned short) addr++;

Corrected Text
--------------
   sum += * (unsigned short *) addr;  addr += 2;

Notes
-----
   The odd trailing octet must be treated as the high-order octet of
   a 16-bit word padded with zero (Section 2 (A)); on big-endian
   hosts the sample adds it as the low-order octet.
```

### RFC 1122: Requirements for Internet Hosts -- Communication Layers {#ra_rfc1122}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 1191: Path MTU Discovery {#ra_rfc1191}

Depth: read (normative statements of 3 to 6). Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0101 | 3, 6.3 | "A host MUST not increase its estimate of the Path MTU in response to" | Mixed-case "MUST not" (three times in RFC 1191; also RFC 1812 "A router MUST not believe any ARP reply"). The intent is MUST NOT; listed once here for the whole group (see Method). | editorial | not checked |
| RA-0412 | 3, 8 | "When a host receives a Datagram Too Big message, it MUST reduce its estimate of the PMTU for the relevant path, based on the value of the Next-Hop MTU field" | Security gap: The host is required to act on any Datagram Too Big message without any check that the quoted original datagram belongs to a connection it has (sequence-number or port validation), so a forged message can force the path MTU down to 68 octets for any destination; Section 8 describes this attack ("at 8 octets of IP data per datagram, progress could be slow") but offers no mitigation. Later work (RFC 5927, RFC 8201 5) adds validation; this document's MUST predates and conflicts with that advice. | error | not checked |

### RFC 1624: Computation of the Internet Checksum via Incremental Update {#ra_rfc1624}

Depth: deep. Errata: not checked. Updates: RFC 1141.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0413 | 5 | "the two additional instructions can be eliminated by subtracting complements with borrow [see Sec. 7]." | Section 7 is the Acknowledgments; the subtraction-of-complements remark is in Section 6 (Historical Note). The claim in Section 3 that the checksum field "can never contain ... -0 (0xFFFF)" holds for the IPv4 header (some field is always non-zero) and should not be carried over to other checksums (e.g. UDP, where 0x0000 is transmitted as 0xFFFF). | editorial | not checked; **proposed erratum below** |

Proposed erratum RA-0413 (RFC 1624, Section 5; type: Editorial):

```
Original Text
-------------
   subtracting complements with borrow [see Sec. 7].

Corrected Text
--------------
   subtracting complements with borrow [see Sec. 6].

Notes
-----
   The historical note on subtraction as the primitive is Section 6.
```

### RFC 1812: Requirements for IP Version 4 Routers {#ra_rfc1812}

Depth: deep. Errata: checked (checked: 5 (2 verified, 2 held, 1 reported; all editorial)). Obsoletes: RFC 1716, RFC 1009.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0102 | 4.3.3.4 | "is reduced to 0, the requirements of section [5.2.3.8] apply." | Section 5.2.3.8 does not cover TTL expiry; the TTL rules are in 5.3.1. | error | 5553 (Held) |
| RA-0103 | 4.3.3.6 | "an ICMP Echo Request datagram at least as the maximum of 576 and the" | Missing words: "at least as large as the maximum of 576 and the MTUs of the connected networks". | editorial | 2704 (Held) |

### RFC 1982: Serial Number Arithmetic {#ra_rfc1982}

Depth: read. Errata: not checked. Updates: RFC 1034, RFC 1035.

Nothing notable found at this depth.

### RFC 2104: HMAC: Keyed-Hashing for Message Authentication {#ra_rfc2104}

Depth: read (algorithm definition, Sections 2 and 3). Errata: not checked. 

Nothing notable found at this depth.

### RFC 2113: IP Router Alert Option {#ra_rfc2113}

Depth: deep. Errata: not checked. 

Nothing notable found at this depth.

### RFC 2464: Transmission of IPv6 Packets over Ethernet Networks {#ra_rfc2464}

Depth: read. Errata: not checked. Obsoletes: RFC 1972.

Nothing notable found at this depth.

### RFC 2711: IPv6 Router Alert Option {#ra_rfc2711}

Depth: deep. Errata: not checked. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0414 | 2.1, 2.2 | "There MUST only be one option of this type, regardless of value, per Hop-by-Hop header. / E.g., for RSVP messages, the datagram will have to undergo UDP and RSVP protocol processing." | The duplicate rule constrains senders only; a router receiving two Router Alert options (possibly with different values) has no stated behaviour (process by the first, ignore, or discard). The RSVP example names UDP processing although RSVP is carried directly over IP (protocol 46) and UDP encapsulation is an optional host mode of RFC 2205 Appendix C. Section 4 allows rate limiting but gives no guidance on what to do with excess packets (forward normally or drop), later addressed by RFC 6398. | ambiguity | not checked |

### RFC 3021: Using 31-Bit Prefixes on IPv4 Point-to-Point Links {#ra_rfc3021}

Depth: read. Errata: not checked. 

Nothing notable found at this depth.

### RFC 4291: IP Version 6 Addressing Architecture {#ra_rfc4291}

Depth: read (normative statements). Errata: not checked. Obsoletes: RFC 3513.

Nothing notable found at this depth.

### RFC 4443: Internet Control Message Protocol (ICMPv6) for the Internet Protocol Version 6 (IPv6) Specification {#ra_rfc4443}

Depth: deep. Errata: checked (checked: 6 (1 reported technical, 1 held technical, 3 held editorial, 1 rejected)). Obsoletes: RFC 2463. Updates: RFC 2780.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0104 | 3.1 | "beyond the scope of the source address, the Code field is set to 2." | "Scope" is used where RFC 4007 defines scope zones; read literally, Code 2 would apply to any global destination when the source is link-local, rather than only when forwarding would cross the source's zone boundary. The report is still open; a related report on Codes 0 and 6 was rejected. | ambiguity | 6153 (Reported), 4445 (Rejected) |
| RA-0415 | 2.2, 4.2 | "the Source Address of the ICMPv6 packet MUST be a unicast address belonging to the node. The address SHOULD be chosen according to the rules ... / In this case, the source address of the reply MUST be a unicast address belonging to the interface on which the Echo Request message was received." | For an Echo Reply to a multicast or anycast Echo Request, Section 2.2 (b) allows any unicast address of the node chosen by normal source selection (or "an alternative way"), while Section 4.2 requires an address of the receiving interface. On a router with unnumbered or loopback-sourced interfaces the two rules give different addresses; the text does not say that 4.2 overrides 2.2 for Echo Replies. | contradiction | none found; **proposed erratum below** |
| RA-0416 | 2.4 | "(e) An ICMPv6 error message MUST NOT be originated as a result of receiving the following:" | The list omits the RFC 1812 4.3.2.7 rule against errors for non-first fragments, and gives no rule for the Packet Too Big exception (e.3 (1)) when the multicast packet is itself an ICMPv6 error. The NOTE says (e) and (f) take precedence "over any requirement elsewhere in this document" but not over other documents (e.g., RFC 4884, RFC 8200 4.x) that also mandate errors. | ambiguity | none found |
| RA-0417 | 5.2 | "The exception number 2 of rule e.3 in Section 2.4 gives a malicious node the opportunity to cause a denial-of-service attack to a multicast source." | Security gap: The only mitigation offered is "securing the multicast traffic"; the general rate limit of 2.4 (f) applies per originator and does not bound the aggregate from many receivers. The text does not recommend that routers or hosts rate-limit Parameter Problem Code 2 responses to multicast sources specifically. | error | none found |

Proposed erratum RA-0415 (RFC 4443, Section 2.2, 4.2; type: Technical):

```
Original Text
-------------
   An Echo Reply SHOULD be sent in response to an Echo Request
   message sent to an IPv6 multicast or anycast address.  In this
   case, the source address of the reply MUST be a unicast address
   belonging to the interface on which the Echo Request message was
   received.

Corrected Text
--------------
   An Echo Reply SHOULD be sent in response to an Echo Request
   message sent to an IPv6 multicast or anycast address.  In this
   case, and notwithstanding Section 2.2 (b), the source address of
   the reply MUST be a unicast address belonging to the interface on
   which the Echo Request message was received.

Notes
-----
   Section 2.2 (b) permits any unicast address of the node chosen by
   source address selection; Section 4.2 restricts it to the
   receiving interface. Clarify that 4.2 is the specific rule for
   Echo Replies.
```

### RFC 4861: Neighbor Discovery for IP version 6 (IPv6) {#ra_rfc4861}

Depth: deep. Errata: checked (checked: 9 (5 verified, 4 of them technical; 3 held, 2 technical; 1 rejected)). Obsoletes: RFC 2461.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0105 | 6.2.1 | "MUST be no less than 3 seconds and no greater than .75 * MaxRtrAdvInterval.  Default: 0.33 * MaxRtrAdvInterval If MaxRtrAdvInterval >= 9 seconds; otherwise, the Default is MaxRtrAdvInterval." | For MaxRtrAdvInterval below 9 seconds the stated default (equal to MaxRtrAdvInterval) violates the MUST in the same definition (at most 0.75 x MaxRtrAdvInterval). The erratum makes the default 0.75 x MaxRtrAdvInterval. | contradiction | 3154 (Verified) |
| RA-0106 | Appendix C | "This appendix contains a summary of the rules specified in Sections 7.2 and 7.3." | The summary table disagrees with 7.2.5: it has no row for a solicited NA without a target link-layer address in PROBE (so a reachable neighbour can be discarded), and labels a Solicited = 1 row INCOMPLETE where PROBE is meant. An implementation built from the table rather than 7.2.5 gets NUD wrong. | error | 2709 (Verified), 2797 (Held) |

### RFC 4862: IPv6 Stateless Address Autoconfiguration {#ra_rfc4862}

Depth: read. Errata: not checked. Obsoletes: RFC 2462.

Nothing notable found at this depth.

### RFC 4884: Extended ICMP to Support Multi-Part Messages {#ra_rfc4884}

Depth: deep. Errata: not checked. Updates: RFC 792, RFC 4443.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0418 | 7, 9 | "An all-zero value means that no checksum was transmitted. / The extension checksum must be verified." | Section 7 allows a zero Extension Header checksum ("no checksum was transmitted"), while Section 9 says the checksum "must be verified" and Section 5.2 / 5.5 use a valid checksum as the only test for a non-compliant (fixed-offset) extension structure; a zero-checksum structure cannot be detected that way and the text does not say whether a receiver should accept it. Section 7's "As stated above, the total length ... MUST NOT exceed the minimum reassembly buffer size" refers to text that is not normative (5.3 "Provided that ..."). Section 8 does not say how a receiver treats an object Length that is zero, not a multiple of 4, or beyond the end of the message (Section 9 only warns of buffer overruns). | ambiguity | not checked |

### RFC 5082: The Generalized TTL Security Mechanism (GTSM) {#ra_rfc5082}

Depth: deep. Errata: no errata page found by search (not confirmed). Obsoletes: RFC 3682.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0419 | 3, 6.1 | "This specification mandates setting and verifying TTL=255 of those as well as the main protocol packets. / The exact policies applied to packets of different classifications are not postulated in this document and are expected to be configurable." | Section 6.1 (and Appendix B) say the document requires related ICMP errors to be checked for TTL 255, but the receive procedure of Section 3 defines classification only for packets "belonging to one of the GTSM-enabled sessions" and leaves policy for related messages configurable; it never says how an ICMP error is associated with a session (by the quoted inner header) or that one with TTL below 255 is Dangerous. On the sending side, related ICMP errors are usually generated by the IP stack, which has no knowledge of GTSM sessions, so "MUST be set to 255" for them is hard to meet. "Expected range" is not defined for the single-hop case other than by the 255 of Section 2.2. | contradiction | not checked |

### RFC 5227: IPv4 Address Conflict Detection {#ra_rfc5227}

Depth: read (normative statements of 1 to 5). Errata: not checked. Updates: RFC 826.

Nothing notable found at this depth.

### RFC 5424: The Syslog Protocol {#ra_rfc5424}

Depth: light (syslog format, normative statements). Errata: not checked. Obsoletes: RFC 3164.

Nothing notable found at this depth.

### RFC 5480: Elliptic Curve Cryptography Subject Public Key Information {#ra_rfc5480}

Depth: light. Errata: errata exist; not read. Updates: RFC 3279.

Nothing notable found at this depth.

### RFC 5758: Internet X.509 Public Key Infrastructure: Additional Algorithms and Identifiers for DSA and ECDSA {#ra_rfc5758}

Depth: light. Errata: no verified errata in the index; page not read. Updates: RFC 3279.

Nothing notable found at this depth.

### RFC 5869: HMAC-based Extract-and-Expand Key Derivation Function (HKDF) {#ra_rfc5869}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 5925: The TCP Authentication Option {#ra_rfc5925}

Depth: deep. Errata: checked (checked: 7 (3 verified technical, 1 reported technical, 1 held editorial, 2 rejected)). Obsoletes: RFC 2385.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0107 | 6.2 | "&& (RCV.PREV_SEQ > 0x7fff) && (SEG.SEQ < 0x7fff)) {" | The Sequence Number Extension pseudocode compares 32-bit sequence numbers with a 16-bit midpoint; it must be 0x7fffffff. Taken literally the SNE increments at the wrong time and MACs fail after the first 2^15 octets of a connection crossing the midpoint. | error | 5672 (Verified) |
| RA-0108 | 7.6 | "This leaves 40 bytes for options, of which 15 are expected in current ... TCP-AO consumes 16 bytes, leaving 9 bytes for additional SYN options" | MSS was left out of the SYN option count, so the stated room left for other options is wrong (the erratum: 21 octets left, 5 for other SYN options). | error | 4365 (Verified) |
| RA-0109 | 5.1 (Figure 6) | "\|      Zero       \|   Next Header   \|" | The figure draws Zero and Next Header as 2 octets each; they are 3 and 1. An implementer building the MAC input from the figure computes a wrong MAC for IPv6. | editorial | 6406 (Held) |
| RA-0110 | 5.2 | "remote ISN), and the destination (remote) ISN is unknown (and so" | In the receive-SYN traffic key both ISNs are called "remote"; the destination ISN is the local one. The erratum is still open. | error | 7899 (Reported) |

### RFC 5926: Cryptographic Algorithms for the TCP Authentication Option (TCP-AO) {#ra_rfc5926}

Depth: deep (2, 3 in full). Errata: no verified errata in the index; page not read. 

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0420 | 3.1.1 | "Output_Length:  The length, in bits, of the key that the KDF will produce.  The Output_length is represented within two octets." | The byte order of the counter-mode input fields is not stated (Output_Length as two octets, implicitly network order), and the Figure 1 pseudo-code lists "len (length of M in octets)" although no M is defined (the input is I). The worked example also writes KDF_alg(Master_Key, 1 \|\| ...) where the PRF is meant, so the KDF appears to call itself. | ambiguity | not checked; **proposed erratum below** |

Proposed erratum RA-0420 (RFC 5926, Section 3.1.1; type: Technical):

```
Original Text
-------------
   The Output_length is represented within two octets.

Corrected Text
--------------
   The Output_Length is represented as a two-octet unsigned integer
   in network byte order.

Notes
-----
   Also, in Figure 1, "len (length of M in octets)" should read "len
   (length of I in octets)".
```

### RFC 5952: A Recommendation for IPv6 Address Text Representation {#ra_rfc5952}

Depth: light. Errata: errata exist; not read. Updates: RFC 4291.

Nothing notable found at this depth.

### RFC 6040: Tunnelling of Explicit Congestion Notification {#ra_rfc6040}

Depth: light. Errata: no verified errata in the index; page not read. Updates: RFC 3168, RFC 4301, RFC 4774.

Nothing notable found at this depth.

### RFC 6066: Transport Layer Security (TLS) Extensions: Extension Definitions {#ra_rfc6066}

Depth: light. Errata: errata exist; not read. Obsoletes: RFC 4366.

Nothing notable found at this depth.

### RFC 6125: Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Ce {#ra_rfc6125}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6234: US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF) {#ra_rfc6234}

Depth: light. Errata: errata exist; not read. Obsoletes: RFC 4634. Updates: RFC 3174.

Nothing notable found at this depth.

### RFC 6398: IP Router Alert Considerations and Usage {#ra_rfc6398}

Depth: light. Errata: no verified errata in the index; page not read. Updates: RFC 2113, RFC 2711.

Nothing notable found at this depth.

### RFC 6454: The Web Origin Concept {#ra_rfc6454}

Depth: light. Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6455: The WebSocket Protocol {#ra_rfc6455}

Depth: light. Errata: errata exist; not read. 

Nothing notable found at this depth.

### RFC 6583: Operational Neighbor Discovery Problems {#ra_rfc6583}

Depth: read (7 in full; Informational). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6890: Special-Purpose IP Address Registries {#ra_rfc6890}

Depth: light. Errata: errata exist; not read. Obsoletes: RFC 4773, RFC 5156, RFC 5735, RFC 5736.

Nothing notable found at this depth.

### RFC 6901: JavaScript Object Notation (JSON) Pointer {#ra_rfc6901}

Depth: light (JSON Pointer, 3 to 5). Errata: no verified errata in the index; page not read. 

Nothing notable found at this depth.

### RFC 6979: Deterministic Usage of the Digital Signature Algorithm (DSA) and Elliptic Curve Digital Signature Algorithm (ECDSA) {#ra_rfc6979}

Depth: light. Errata: errata exist; not read. 

Nothing notable found at this depth.

### RFC 6980: Security Implications of IPv6 Fragmentation with IPv6 Neighbor Discovery {#ra_rfc6980}

Depth: light (short; libarp follows the MUST NOT on fragmented ND). Errata: no verified errata in the index; page not read. Updates: RFC 3971, RFC 4861.

Nothing notable found at this depth.

### RFC 7112: Implications of Oversized IPv6 Header Chains {#ra_rfc7112}

Depth: light. Errata: no verified errata in the index; page not read. Updates: RFC 2460.

Nothing notable found at this depth.

### RFC 7525: Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS) {#ra_rfc7525}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 7748: Elliptic Curves for Security {#ra_rfc7748}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 8017: PKCS #1: RSA Cryptography Specifications Version 2.2 {#ra_rfc8017}

Depth: light (PKCS #1 v2.2; used through OpenSSL). Errata: not checked. Obsoletes: RFC 3447.

Nothing notable found at this depth.

### RFC 8032: Edwards-Curve Digital Signature Algorithm (EdDSA) {#ra_rfc8032}

Depth: light (EdDSA; used through OpenSSL). Errata: not checked. 

Nothing notable found at this depth.

### RFC 8200: Internet Protocol, Version 6 (IPv6) Specification {#ra_rfc8200}

Depth: part (Sections 3, 4, 4.1 to 4.3 read; 4.4 to 4.8, 5 to 8 checked against the errata list only). Errata: checked (checked: 11 records on the errata page (5945 verified technical 4.5 fragment offset reference; 5256 verified editorial 4.8; 6248 reported technical 4.5; 5933 held technical 4; 5259, 5506 held editorial Appendix B; 5170 to 5173 and 6003 rejected) plus 8698 (reported, technical, 4.5 "within 60 seconds" reassembly time), not yet shown on that page). Obsoletes: RFC 2460.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0421 | 4, 4.3, 4.2 | "it is now expected that nodes along a packet's delivery path only examine and process the Hop-by-Hop Options header if explicitly configured to do so. / The Hop-by-Hop Options header is used to carry optional information that may be examined and processed by every node along a packet's delivery path." | Section 4 (with its NOTE) makes Hop-by-Hop processing at transit nodes optional and configuration-driven, while Section 4.3 still describes the header as information for "every node". The option-type action bits of Section 4.2 (skip, discard, discard and send ICMP) only make sense for a node that processes the header; the text does not say whether a transit node configured not to process the header must forward the packet unchanged (ignoring an option whose action bits say "discard"), nor whether it may drop packets with a Hop-by-Hop header altogether. Held erratum 5933 covers the related question for the other extension headers. | ambiguity | 5933 (Held, related) |

### RFC 8201: Path MTU Discovery for IP version 6 {#ra_rfc8201}

Depth: light (lines with requirement words scanned only). Errata: not checked. Obsoletes: RFC 1981.

Nothing notable found at this depth.

### RFC 8259: The JavaScript Object Notation (JSON) Data Interchange Format {#ra_rfc8259}

Depth: deep. Errata: checked (checked: 12 on the errata page (10 reported: 5218, 5853, 7383, 7600, 7603, 7617, 7650, 7673 technical, 5210, 5318 editorial; 2 rejected: 6208, 7307); WG mail-archive titles describe 5210, 5318, 7383, 7600, 7603 as verified and list 7650 as held, so the page state could not be confirmed; none of them changes the findings below). Obsoletes: RFC 7159.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0422 | 9, 4, 8.2 | "A JSON parser MUST accept all texts that conform to the JSON grammar. / The names within an object SHOULD be unique. / Other implementations report an error or fail to parse the object" | Objects with duplicate names and strings with unpaired surrogate escapes ("\uDEAD") conform to the grammar, so Section 9 requires a parser to accept them, while Sections 4 and 8.2 describe rejecting them as existing, unpredictable behaviour and Section 9 itself allows limits on "character contents of strings". Whether rejecting duplicate names (a common security hardening) is conformant is therefore not clear. | ambiguity | not checked |

### RFC 8439: ChaCha20 and Poly1305 for IETF Protocols {#ra_rfc8439}

Depth: light (ChaCha20-Poly1305; used through OpenSSL). Errata: not checked. Obsoletes: RFC 7539.

Nothing notable found at this depth.

### RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3 {#ra_rfc8446}

Depth: light. Errata: not checked. Obsoletes: RFC 5077, RFC 5246, RFC 6961. Updates: RFC 5705, RFC 6066.

Nothing notable found at this depth.

### RFC 8448: Example Handshake Traces for TLS 1.3 {#ra_rfc8448}

Depth: light (TLS 1.3 example traces, informational). Errata: not checked. 

Nothing notable found at this depth.

### RFC 9000: QUIC: A UDP-Based Multiplexed and Secure Transport {#ra_rfc9000}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9001: Using TLS to Secure QUIC {#ra_rfc9001}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9002: QUIC Loss Detection and Congestion Control {#ra_rfc9002}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9110: HTTP Semantics {#ra_rfc9110}

Depth: light. Errata: not checked. Obsoletes: RFC 2818, RFC 7230, RFC 7231, RFC 7232, RFC 7233, RFC 7235, RFC 7538, RFC 7615, RFC 7694. Updates: RFC 3864.

Nothing notable found at this depth.

### RFC 9112: HTTP/1.1 {#ra_rfc9112}

Depth: light. Errata: not checked. Obsoletes: RFC 7230.

Nothing notable found at this depth.

### RFC 9114: HTTP/3 {#ra_rfc9114}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9204: QPACK: Field Compression for HTTP/3 {#ra_rfc9204}

Depth: light. Errata: not checked. 

Nothing notable found at this depth.

### RFC 9325: Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS) {#ra_rfc9325}

Depth: light. Errata: not checked. Obsoletes: RFC 7525. Updates: RFC 5288, RFC 6066.

Nothing notable found at this depth.

### RFC 9525: Service Identity in TLS {#ra_rfc9525}

Depth: part. Errata: not checked. Obsoletes: RFC 6125.

| ID | Section | Quote | Issue | Severity | Erratum |
|---|---|---|---|---|---|
| RA-0423 | 1.3, 6 vs RFC 8253 3.4 | "The client MUST construct a list of acceptable reference identifiers and MUST do so independently of the identifiers presented by the server." | RFC 9525 (which obsoletes RFC 6125) no longer allows matching on the subject Common Name (CN-ID), while RFC 8253 3.4 (PCEPS) still lists a CN-ID check as one of the peer identity options. A PCEP implementation following RFC 9525 cannot interoperate with a peer whose certificate carries the identity only in the CN, and RFC 8253 has not been updated. | contradiction | none found |

### Other RFCs in this area {#ra_ip_other}

Mechanical checks only, no finding: RFC 1321 (The MD5 Message-Digest Algorithm), RFC 1858 (Security Considerations for IP Fragment Filtering), RFC 2202 (Test Cases for HMAC-MD5 and HMAC-SHA-1), RFC 2253 (Lightweight Directory Access Protocol (v3): UTF-8 String Representatio), RFC 2863 (The Interfaces Group MIB), RFC 3174 (US Secure Hash Algorithm 1 (SHA1)), RFC 3339 (Date and Time on the Internet: Timestamps), RFC 3629 (UTF-8, a transformation format of ISO 10646), RFC 3971 (SEcure Neighbor Discovery (SEND)), RFC 4231 (Identifiers and Test Vectors for HMAC-SHA-224, HMAC-SHA-256, HMAC-SHA-), RFC 4648 (The Base16, Base32, and Base64 Data Encodings), RFC 4868 (Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec), RFC 5116 (An Interface and Algorithms for Authenticated Encryption), RFC 5246 (The Transport Layer Security (TLS) Protocol Version 1.2), RFC 5280 (Internet X.509 Public Key Infrastructure Certificate and Certificate R).

## Coverage by RFC {#ra_index}

Every RFC reviewed, with the depth of reading (best of the two passes) and the errata status. Depth and errata categories are defined in [Coverage](#ra_coverage).

| RFC | Title | Area | Depth | Errata | Findings | Proposed errata |
|---|---|---|---|---|---|---|
| [RFC 768](#ra_rfc768) | User Datagram Protocol | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 791](#ra_rfc791) | INTERNET PROTOCOL | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 792](#ra_rfc792) | Internet Control Message Protocol | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 826](#ra_rfc826) | An Ethernet Address Resolution Protocol -- or -- Converting Network Protocol Addresses to  | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 1042](#ra_rfc1042) | A Standard for the Transmission of IP Datagrams over IEEE 802 Networks | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 1071](#ra_rfc1071) | Computing the Internet Checksum | [IP](#ra_ip) | read | not checked | 1 | 1 |
| [RFC 1122](#ra_rfc1122) | Requirements for Internet Hosts -- Communication Layers | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 1142](#ra_rfc1142) | OSI IS-IS Intra-domain Routing Protocol | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 1191](#ra_rfc1191) | Path MTU Discovery | [IP](#ra_ip) | read | not checked | 2 | 0 |
| [RFC 1195](#ra_rfc1195) | Use of OSI IS-IS for Routing in TCP/IP and Dual Environments | [IS-IS](#ra_isis) | deep | checked | 2 | 0 |
| RFC 1321 | The MD5 Message-Digest Algorithm | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 1624](#ra_rfc1624) | Computation of the Internet Checksum via Incremental Update | [IP](#ra_ip) | deep | not checked | 1 | 1 |
| [RFC 1812](#ra_rfc1812) | Requirements for IP Version 4 Routers | [IP](#ra_ip) | deep | checked | 2 | 0 |
| RFC 1858 | Security Considerations for IP Fragment Filtering | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 1982](#ra_rfc1982) | Serial Number Arithmetic | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 1997](#ra_rfc1997) | BGP Communities Attribute | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 2042](#ra_rfc2042) | Registering New BGP Attribute Types | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 2104](#ra_rfc2104) | HMAC: Keyed-Hashing for Message Authentication | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 2113](#ra_rfc2113) | IP Router Alert Option | [IP](#ra_ip) | deep | not checked | 0 | 0 |
| RFC 2202 | Test Cases for HMAC-MD5 and HMAC-SHA-1 | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 2205](#ra_rfc2205) | Resource ReSerVation Protocol (RSVP) -- Version 1 Functional Specification | [RSVP](#ra_rsvp) | deep | checked | 1 | 0 |
| [RFC 2209](#ra_rfc2209) | Resource ReSerVation Protocol (RSVP) -- Version 1 Message Processing Rules | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 2210](#ra_rfc2210) | The Use of RSVP with IETF Integrated Services | [RSVP](#ra_rsvp) | deep | not checked | 2 | 1 |
| RFC 2211 | Specification of the Controlled-Load Network Element Service | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| RFC 2212 | Specification of Guaranteed Quality of Service | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| [RFC 2236](#ra_rfc2236) | Internet Group Management Protocol, Version 2 | [Multicast](#ra_mcast) | scan | not checked | 1 | 1 |
| RFC 2253 | Lightweight Directory Access Protocol (v3): UTF-8 String Representation of Distinguished N | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 2330](#ra_rfc2330) | Advanced Network & Services | [OAM](#ra_oam) | light | not checked | 0 | 0 |
| [RFC 2385](#ra_rfc2385) | Protection of BGP Sessions via the TCP MD5 Signature Option | [BGP](#ra_bgp) | deep | not checked | 1 | 1 |
| [RFC 2464](#ra_rfc2464) | Transmission of IPv6 Packets over Ethernet Networks | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 2545](#ra_rfc2545) | Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 2710](#ra_rfc2710) | Multicast Listener Discovery (MLD) for IPv6 | [Multicast](#ra_mcast) | light | not checked | 0 | 0 |
| [RFC 2711](#ra_rfc2711) | IPv6 Router Alert Option | [IP](#ra_ip) | deep | not checked | 1 | 0 |
| [RFC 2747](#ra_rfc2747) | RSVP Cryptographic Authentication | [RSVP](#ra_rsvp) | deep | checked | 1 | 0 |
| [RFC 2750](#ra_rfc2750) | RSVP Extensions for Policy Control | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| RFC 2863 | The Interfaces Group MIB | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 2918](#ra_rfc2918) | Route Refresh Capability for BGP-4 | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 2961](#ra_rfc2961) | RSVP Refresh Overhead Reduction Extensions | [RSVP](#ra_rsvp) | deep | exist, not read | 6 | 1 |
| [RFC 3021](#ra_rfc3021) | Using 31-Bit Prefixes on IPv4 Point-to-Point Links | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 3032](#ra_rfc3032) | MPLS Label Stack Encoding | [MPLS/LDP](#ra_ldp) | deep | checked | 2 | 0 |
| [RFC 3036](#ra_rfc3036) | LDP Specification | [MPLS/LDP](#ra_ldp) | read | not checked | 0 | 0 |
| [RFC 3097](#ra_rfc3097) | RSVP Cryptographic Authentication -- Updated Message Type Value | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| RFC 3174 | US Secure Hash Algorithm 1 (SHA1) | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| RFC 3175 | Aggregation of RSVP for IPv4 and IPv6 Reservations | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| [RFC 3209](#ra_rfc3209) | RSVP-TE: Extensions to RSVP for LSP Tunnels | [RSVP](#ra_rsvp) | deep | checked | 2 | 0 |
| [RFC 3212](#ra_rfc3212) | Constraint-Based LSP Setup using LDP | [MPLS/LDP](#ra_ldp) | scan | not checked | 1 | 1 |
| [RFC 3270](#ra_rfc3270) | Multi-Protocol Label Switching (MPLS) Support of Differentiated Services | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| RFC 3339 | Date and Time on the Internet: Timestamps | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 3358](#ra_rfc3358) | Optional Checksums in Intermediate System to Intermediate System (ISIS) | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| RFC 3376 | Internet Group Management Protocol, Version 3 | [Multicast](#ra_mcast) | scan | not checked | 0 | 0 |
| [RFC 3429](#ra_rfc3429) | Assignment of the 'OAM Alert Label' for Multiprotocol Label Switching Architecture (MPLS)  | [MPLS/LDP](#ra_ldp) | light | not checked | 0 | 0 |
| [RFC 3443](#ra_rfc3443) | Time To Live (TTL) Processing in Multi-Protocol Label Switching (MPLS) Networks | [MPLS/LDP](#ra_ldp) | read | not checked | 0 | 0 |
| RFC 3468 | The Multiprotocol Label Switching (MPLS) Working Group decision on MPLS signaling protocol | [MPLS/LDP](#ra_ldp) | scan | not checked | 0 | 0 |
| [RFC 3471](#ra_rfc3471) | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Functional Description | [RSVP](#ra_rsvp) | read | not checked | 1 | 0 |
| [RFC 3472](#ra_rfc3472) | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Constraint-based Routed Label | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 3473](#ra_rfc3473) | Generalized Multi-Protocol Label Switching (GMPLS) Signaling Resource ReserVation Protocol | [RSVP](#ra_rsvp) | deep | checked | 3 | 0 |
| [RFC 3475](#ra_rfc3475) | Documentation of IANA assignments for Constraint-Based LSP setup using LDP (CR-LDP) Extens | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 3477](#ra_rfc3477) | Signalling Unnumbered Links in Resource ReSerVation Protocol - Traffic Engineering (RSVP-T | [RSVP](#ra_rsvp) | deep | not checked | 2 | 0 |
| [RFC 3478](#ra_rfc3478) | Graceful Restart Mechanism for Label Distribution Protocol | [MPLS/LDP](#ra_ldp) | deep | no page found | 4 | 2 |
| [RFC 3479](#ra_rfc3479) | Fault Tolerance for the Label Distribution Protocol (LDP) | [MPLS/LDP](#ra_ldp) | read | not checked | 1 | 0 |
| RFC 3629 | UTF-8, a transformation format of ISO 10646 | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| RFC 3630 | Traffic Engineering (TE) Extensions to OSPF Version 2 | [IS-IS](#ra_isis) | scan | not checked | 0 | 0 |
| [RFC 3719](#ra_rfc3719) | Recommendations for Interoperable Networks using Intermediate System to Intermediate Syste | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| [RFC 3765](#ra_rfc3765) | NOPEER Community for Border Gateway Protocol (BGP) Route Scope Control | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 3787](#ra_rfc3787) | Recommendations for Interoperable IP Networks using Intermediate System to Intermediate Sy | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| RFC 3810 | Multicast Listener Discovery Version 2 (MLDv2) for IPv6 | [Multicast](#ra_mcast) | scan | not checked | 0 | 0 |
| [RFC 3906](#ra_rfc3906) | Calculating Interior Gateway Protocol (IGP) Routes Over Traffic Engineering Tunnels | [IS-IS](#ra_isis) | deep | not checked | 2 | 1 |
| RFC 3971 | SEcure Neighbor Discovery (SEND) | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 3988](#ra_rfc3988) | Maximum Transmission Unit Signalling Extensions for the Label Distribution Protocol | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 4090](#ra_rfc4090) | Fast Reroute Extensions to RSVP-TE for LSP Tunnels | [RSVP](#ra_rsvp) | deep | checked | 3 | 0 |
| [RFC 4105](#ra_rfc4105) | Requirements for Inter-Area MPLS Traffic Engineering | [RSVP](#ra_rsvp) | light | not checked | 0 | 0 |
| [RFC 4124](#ra_rfc4124) | Protocol Extensions for Support of Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | deep | not checked | 4 | 1 |
| [RFC 4125](#ra_rfc4125) | Maximum Allocation Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | deep | not checked | 0 | 0 |
| RFC 4126 | Max Allocation with Reservation Bandwidth Constraints Model for Diffserv-aware MPLS Traffi | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| [RFC 4127](#ra_rfc4127) | Russian Dolls Bandwidth Constraints Model for Diffserv-aware MPLS Traffic Engineering | [RSVP](#ra_rsvp) | deep | not checked | 0 | 0 |
| [RFC 4206](#ra_rfc4206) | Label Switched Paths (LSP) Hierarchy with Generalized Multi-Protocol Label Switching (GMPL | [RSVP](#ra_rsvp) | read | not checked | 1 | 0 |
| RFC 4231 | Identifiers and Test Vectors for HMAC-SHA-224, HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-51 | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 4271](#ra_rfc4271) | A Border Gateway Protocol 4 (BGP-4) | [BGP](#ra_bgp) | deep | checked | 11 | 1 |
| [RFC 4291](#ra_rfc4291) | IP Version 6 Addressing Architecture | [IP](#ra_ip) | read | not checked | 0 | 0 |
| [RFC 4360](#ra_rfc4360) | BGP Extended Communities Attribute | [BGP](#ra_bgp) | read | not checked | 1 | 0 |
| [RFC 4364](#ra_rfc4364) | BGP/MPLS IP Virtual Private Networks (VPNs) | [BGP](#ra_bgp) | deep | checked | 2 | 0 |
| [RFC 4385](#ra_rfc4385) | Pseudowire Emulation Edge-to-Edge (PWE3) Control Word for Use over an MPLS PSN | [PW](#ra_pw) | deep | checked | 2 | 1 |
| [RFC 4443](#ra_rfc4443) | Internet Control Message Protocol (ICMPv6) for the Internet Protocol Version 6 (IPv6) Spec | [IP](#ra_ip) | deep | checked | 4 | 1 |
| RFC 4444 | Management Information Base for Intermediate System to Intermediate System (IS-IS) | [IS-IS](#ra_isis) | scan | not checked | 0 | 0 |
| [RFC 4446](#ra_rfc4446) | IANA Allocations for Pseudowire Edge to Edge Emulation (PWE3) | [PW](#ra_pw) | read | not checked | 0 | 0 |
| [RFC 4447](#ra_rfc4447) | Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) | [PW](#ra_pw) | read | not checked | 0 | 0 |
| [RFC 4448](#ra_rfc4448) | Encapsulation Methods for Transport of Ethernet over MPLS Networks | [PW](#ra_pw) | deep | not checked | 2 | 1 |
| [RFC 4456](#ra_rfc4456) | BGP Route Reflection: An Alternative to Full Mesh Internal BGP (IBGP) | [BGP](#ra_bgp) | deep | checked | 2 | 0 |
| [RFC 4486](#ra_rfc4486) | Subcodes for BGP Cease Notification Message | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 4561](#ra_rfc4561) | Definition of a Record Route Object (RRO) Node-Id Sub-Object | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 4604](#ra_rfc4604) | Using Internet Group Management Protocol Version 3 (IGMPv3) and Multicast Listener Discove | [Multicast](#ra_mcast) | read | not checked | 0 | 0 |
| [RFC 4607](#ra_rfc4607) | Source-Specific Multicast for IP | [Multicast](#ra_mcast) | read | not checked | 1 | 1 |
| [RFC 4610](#ra_rfc4610) | Anycast-RP Using Protocol Independent Multicast (PIM) | [Multicast](#ra_mcast) | read | not checked | 0 | 0 |
| [RFC 4623](#ra_rfc4623) | Pseudowire Emulation Edge-to-Edge (PWE3) Fragmentation and Reassembly | [PW](#ra_pw) | read | not checked | 0 | 0 |
| RFC 4648 | The Base16, Base32, and Base64 Data Encodings | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 4656](#ra_rfc4656) | A One-way Active Measurement Protocol (OWAMP) | [OAM](#ra_oam) | light | not checked | 0 | 0 |
| [RFC 4659](#ra_rfc4659) | BGP-MPLS IP Virtual Private Network (VPN) Extension for IPv6 VPN | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 4724](#ra_rfc4724) | Graceful Restart Mechanism for BGP | [BGP](#ra_bgp) | deep | checked | 4 | 1 |
| RFC 4726 | A Framework for Inter-Domain Multiprotocol Label Switching Traffic Engineering | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| [RFC 4760](#ra_rfc4760) | Multiprotocol Extensions for BGP-4 | [BGP](#ra_bgp) | deep | checked | 4 | 0 |
| [RFC 4761](#ra_rfc4761) | Virtual Private LAN Service (VPLS) Using BGP for Auto-Discovery and Signaling | [PW](#ra_pw) | light | not checked | 0 | 0 |
| [RFC 4762](#ra_rfc4762) | Virtual Private LAN Service (VPLS) Using Label Distribution Protocol (LDP) Signaling | [PW](#ra_pw) | deep | checked | 1 | 0 |
| [RFC 4798](#ra_rfc4798) | Connecting IPv6 Islands over IPv4 MPLS Using IPv6 Provider Edge Routers (6PE) | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 4861](#ra_rfc4861) | Neighbor Discovery for IP version 6 (IPv6) | [IP](#ra_ip) | deep | checked | 2 | 0 |
| [RFC 4862](#ra_rfc4862) | IPv6 Stateless Address Autoconfiguration | [IP](#ra_ip) | read | not checked | 0 | 0 |
| RFC 4868 | Using HMAC-SHA-256, HMAC-SHA-384, and HMAC-SHA-512 with IPsec | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 4872](#ra_rfc4872) | RSVP-TE Extensions in Support of End-to-End Generalized Multi-Protocol Label Switching (GM | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 4873](#ra_rfc4873) | GMPLS Segment Recovery | [RSVP](#ra_rsvp) | read | not checked | 1 | 1 |
| [RFC 4874](#ra_rfc4874) | Exclude Routes - Extension to Resource ReserVation Protocol-Traffic Engineering (RSVP-TE) | [RSVP](#ra_rsvp) | read | not checked | 1 | 1 |
| [RFC 4875](#ra_rfc4875) | Extensions to Resource Reservation Protocol - Traffic Engineering (RSVP-TE) for Point-to-M | [RSVP](#ra_rsvp) | deep | checked | 2 | 0 |
| [RFC 4884](#ra_rfc4884) | Extended ICMP to Support Multi-Part Messages | [IP](#ra_ip) | deep | not checked | 1 | 0 |
| RFC 4920 | Crankback Signaling Extensions for MPLS and GMPLS RSVP-TE | [RSVP](#ra_rsvp) | scan | not checked | 0 | 0 |
| [RFC 4950](#ra_rfc4950) | ICMP Extensions for Multiprotocol Label Switching | [MPLS/LDP](#ra_ldp) | deep | not checked | 0 | 0 |
| [RFC 5003](#ra_rfc5003) | Attachment Individual Identifier (AII) Types for Aggregation | [PW](#ra_pw) | read | not checked | 0 | 0 |
| [RFC 5004](#ra_rfc5004) | Avoid BGP Best Path Transitions from One External to Another | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 5015](#ra_rfc5015) | Bidirectional Protocol Independent Multicast (BIDIR-PIM) | [Multicast](#ra_mcast) | deep | not checked | 2 | 2 |
| [RFC 5036](#ra_rfc5036) | LDP Specification | [MPLS/LDP](#ra_ldp) | deep | checked | 4 | 1 |
| [RFC 5059](#ra_rfc5059) | Bootstrap Router (BSR) Mechanism for Protocol Independent Multicast (PIM) | [Multicast](#ra_mcast) | deep | checked | 5 | 1 |
| [RFC 5063](#ra_rfc5063) | Extensions to GMPLS Resource Reservation Protocol (RSVP) Graceful Restart | [RSVP](#ra_rsvp) | deep | not checked | 3 | 1 |
| [RFC 5065](#ra_rfc5065) | Autonomous System Confederations for BGP | [BGP](#ra_bgp) | deep | not checked | 3 | 0 |
| [RFC 5082](#ra_rfc5082) | The Generalized TTL Security Mechanism (GTSM) | [IP](#ra_ip) | deep | no page found | 1 | 0 |
| [RFC 5085](#ra_rfc5085) | Pseudowire Virtual Circuit Connectivity Verification (VCCV): A Control Channel for Pseudow | [PW](#ra_pw) | deep | not checked | 4 | 1 |
| [RFC 5088](#ra_rfc5088) | OSPF Protocol Extensions for Path Computation Element (PCE) Discovery | [PCEP](#ra_pcep) | scan | not checked | 1 | 1 |
| RFC 5089 | IS-IS Protocol Extensions for Path Computation Element (PCE) Discovery | [IS-IS](#ra_isis) | scan | not checked | 0 | 0 |
| RFC 5116 | An Interface and Algorithms for Authenticated Encryption | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 5120](#ra_rfc5120) | M-ISIS: Multi Topology (MT) Routing in Intermediate System to Intermediate Systems (IS-ISs | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 5130](#ra_rfc5130) | A Policy Control Mechanism in IS-IS Using Administrative Tags | [IS-IS](#ra_isis) | read | not checked | 1 | 0 |
| [RFC 5150](#ra_rfc5150) | Label Switched Path Stitching with Generalized Multiprotocol Label Switching Traffic Engin | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 5151](#ra_rfc5151) | Inter-Domain MPLS and GMPLS Traffic Engineering -- Resource Reservation Protocol-Traffic E | [RSVP](#ra_rsvp) | deep | not checked | 3 | 1 |
| [RFC 5152](#ra_rfc5152) | A Per-Domain Path Computation Method for Establishing Inter-Domain Traffic Engineering (TE | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 5227](#ra_rfc5227) | IPv4 Address Conflict Detection | [IP](#ra_ip) | read | not checked | 0 | 0 |
| RFC 5246 | The Transport Layer Security (TLS) Protocol Version 1.2 | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| RFC 5280 | Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) | [IP](#ra_ip) | scan | not checked | 0 | 0 |
| [RFC 5283](#ra_rfc5283) | LDP Extension for Inter-Area Label Switched Paths (LSPs) | [MPLS/LDP](#ra_ldp) | read | not checked | 0 | 0 |
| [RFC 5284](#ra_rfc5284) | User-Defined Errors for RSVP | [RSVP](#ra_rsvp) | read | not checked | 0 | 0 |
| [RFC 5286](#ra_rfc5286) | Basic Specification for IP Fast Reroute: Loop-Free Alternates | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| [RFC 5291](#ra_rfc5291) | Outbound Route Filtering Capability for BGP-4 | [BGP](#ra_bgp) | read | not checked | 1 | 0 |
| [RFC 5301](#ra_rfc5301) | Dynamic Hostname Exchange Mechanism for IS-IS | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| [RFC 5302](#ra_rfc5302) | Domain-Wide Prefix Distribution with Two-Level IS-IS | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| [RFC 5303](#ra_rfc5303) | Three-Way Handshake for IS-IS Point-to-Point Adjacencies | [IS-IS](#ra_isis) | deep | not checked | 2 | 0 |
| [RFC 5304](#ra_rfc5304) | IS-IS Cryptographic Authentication | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 5305](#ra_rfc5305) | IS-IS Extensions for Traffic Engineering | [IS-IS](#ra_isis) | deep | no page found | 3 | 2 |
| RFC 5306 | Restart Signaling for IS-IS | [IS-IS](#ra_isis) | scan | not checked | 0 | 0 |
| [RFC 5307](#ra_rfc5307) | IS-IS Extensions in Support of Generalized Multi-Protocol Label Switching (GMPLS) | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| [RFC 5308](#ra_rfc5308) | Routing IPv6 with IS-IS | [IS-IS](#ra_isis) | part | not checked | 1 | 0 |
| [RFC 5310](#ra_rfc5310) | IS-IS Generic Cryptographic Authentication | [IS-IS](#ra_isis) | deep | no page found | 3 | 1 |
| [RFC 5311](#ra_rfc5311) | Simplified Extension of Link State PDU (LSP) Space for IS-IS | [IS-IS](#ra_isis) | read | not checked | 0 | 0 |
| RFC 5316 | ISIS Extensions in Support of Inter-Autonomous System (AS) MPLS and GMPLS Traffic Engineer | [IS-IS](#ra_isis) | scan | not checked | 0 | 0 |
| [RFC 5331](#ra_rfc5331) | MPLS Upstream Label Assignment and Context-Specific Label Space | [MPLS/LDP](#ra_ldp) | deep | not checked | 2 | 1 |
| [RFC 5332](#ra_rfc5332) | MPLS Multicast Encapsulations | [MPLS/LDP](#ra_ldp) | read | not checked | 0 | 0 |
| [RFC 5357](#ra_rfc5357) | A Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | deep | checked | 6 | 2 |
| [RFC 5398](#ra_rfc5398) | Autonomous System (AS) Number Reservation for Documentation Use | [BGP](#ra_bgp) | read | not checked | 0 | 0 |
| [RFC 5420](#ra_rfc5420) | Encoding of Attributes for MPLS LSP Establishment Using Resource Reservation Protocol Traf | [RSVP](#ra_rsvp) | deep | not checked | 3 | 1 |
| [RFC 5424](#ra_rfc5424) | The Syslog Protocol | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 5440](#ra_rfc5440) | Path Computation Element (PCE) Communication Protocol (PCEP) | [PCEP](#ra_pcep) | deep | checked | 3 | 0 |
| [RFC 5441](#ra_rfc5441) | A Backward-Recursive PCE-Based Computation (BRPC) Procedure to Compute Shortest Constraine | [PCEP](#ra_pcep) | deep | not checked | 4 | 2 |
| [RFC 5443](#ra_rfc5443) | LDP IGP Synchronization | [MPLS/LDP](#ra_ldp) | deep | not checked | 1 | 1 |
| [RFC 5480](#ra_rfc5480) | Elliptic Curve Cryptography Subject Public Key Information | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 5492](#ra_rfc5492) | Capabilities Advertisement with BGP-4 | [BGP](#ra_bgp) | part | checked | 1 | 0 |
| [RFC 5495](#ra_rfc5495) | Description of the Resource Reservation Protocol - Traffic-Engineered (RSVP-TE) Graceful R | [RSVP](#ra_rsvp) | light | none verified in index | 0 | 0 |
| [RFC 5520](#ra_rfc5520) | Preserving Topology Confidentiality in Inter-Domain Path Computation Using a Path-Key-Base | [PCEP](#ra_pcep) | light | exist, not read | 0 | 0 |
| [RFC 5521](#ra_rfc5521) | Extensions to the Path Computation Element Communication Protocol (PCEP) for Route Exclusi | [PCEP](#ra_pcep) | light | exist, not read | 0 | 0 |
| [RFC 5541](#ra_rfc5541) | Encoding of Objective Functions in the Path Computation Element Communication Protocol (PC | [PCEP](#ra_pcep) | deep | none verified in index | 3 | 1 |
| [RFC 5543](#ra_rfc5543) | BGP Traffic Engineering Attribute | [BGP](#ra_bgp) | light | none verified in index | 0 | 0 |
| [RFC 5561](#ra_rfc5561) | LDP Capabilities | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 1 | 0 |
| [RFC 5586](#ra_rfc5586) | MPLS Generic Associated Channel | [MPLS/LDP](#ra_ldp) | deep | exist, not read | 0 | 0 |
| [RFC 5618](#ra_rfc5618) | Mixed Security Mode for the Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | deep | none verified in index | 0 | 0 |
| [RFC 5668](#ra_rfc5668) | 4-Octet AS Specific BGP Extended Community | [BGP](#ra_bgp) | deep | none verified in index | 0 | 0 |
| [RFC 5701](#ra_rfc5701) | IPv6 Address Specific BGP Extended Community Attribute | [BGP](#ra_bgp) | read | none verified in index | 0 | 0 |
| [RFC 5712](#ra_rfc5712) | MPLS Traffic Engineering Soft Preemption | [RSVP](#ra_rsvp) | light | none verified in index | 0 | 0 |
| [RFC 5758](#ra_rfc5758) | Internet X.509 Public Key Infrastructure: Additional Algorithms and Identifiers for DSA an | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 5771](#ra_rfc5771) | IANA Guidelines for IPv4 Multicast Address Assignments | [Multicast](#ra_mcast) | light | none verified in index | 0 | 0 |
| [RFC 5869](#ra_rfc5869) | HMAC-based Extract-and-Expand Key Derivation Function (HKDF) | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 5880](#ra_rfc5880) | Bidirectional Forwarding Detection (BFD) | [OAM](#ra_oam) | deep | checked | 3 | 0 |
| [RFC 5881](#ra_rfc5881) | Bidirectional Forwarding Detection (BFD) for IPv4 and IPv6 (Single Hop) | [OAM](#ra_oam) | deep | checked | 3 | 0 |
| [RFC 5882](#ra_rfc5882) | Generic Application of Bidirectional Forwarding Detection (BFD) | [OAM](#ra_oam) | deep | checked | 3 | 1 |
| [RFC 5883](#ra_rfc5883) | Bidirectional Forwarding Detection (BFD) for Multihop Paths | [OAM](#ra_oam) | deep | none verified in index | 1 | 0 |
| [RFC 5884](#ra_rfc5884) | Bidirectional Forwarding Detection (BFD) for MPLS Label Switched Paths (LSPs) | [OAM](#ra_oam) | deep | checked | 2 | 0 |
| [RFC 5885](#ra_rfc5885) | Bidirectional Forwarding Detection (BFD) for the Pseudowire Virtual Circuit Connectivity V | [OAM](#ra_oam) | deep | none verified in index | 1 | 0 |
| [RFC 5886](#ra_rfc5886) | A Set of Monitoring Tools for Path Computation Element (PCE)-Based Architecture | [PCEP](#ra_pcep) | light | none verified in index | 0 | 0 |
| [RFC 5905](#ra_rfc5905) | Network Time Protocol Version 4: Protocol and Algorithms Specification | [OAM](#ra_oam) | light | exist, not read | 0 | 0 |
| [RFC 5918](#ra_rfc5918) | Label Distribution Protocol (LDP) 'Typed Wildcard' Forward Equivalence Class (FEC) | [MPLS/LDP](#ra_ldp) | deep | exist, not read | 2 | 1 |
| [RFC 5919](#ra_rfc5919) | Signaling LDP Label Advertisement Completion | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 1 | 0 |
| [RFC 5925](#ra_rfc5925) | The TCP Authentication Option | [IP](#ra_ip) | deep | checked | 4 | 0 |
| [RFC 5926](#ra_rfc5926) | Cryptographic Algorithms for the TCP Authentication Option (TCP-AO) | [IP](#ra_ip) | deep | none verified in index | 1 | 1 |
| [RFC 5938](#ra_rfc5938) | Individual Session Control Feature for the Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | deep | exist, not read | 1 | 1 |
| [RFC 5952](#ra_rfc5952) | A Recommendation for IPv6 Address Text Representation | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6037](#ra_rfc6037) | Cisco Systems' Solution for Multicast in BGP/MPLS IP VPNs | [Multicast](#ra_mcast) | light | none verified in index | 0 | 0 |
| [RFC 6038](#ra_rfc6038) | Two-Way Active Measurement Protocol (TWAMP) Reflect Octets and Symmetrical Size Features | [OAM](#ra_oam) | scan | exist, not read | 1 | 1 |
| [RFC 6040](#ra_rfc6040) | Tunnelling of Explicit Congestion Notification | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6066](#ra_rfc6066) | Transport Layer Security (TLS) Extensions: Extension Definitions | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6073](#ra_rfc6073) | Segmented Pseudowire | [PW](#ra_pw) | deep | none verified in index | 4 | 2 |
| [RFC 6074](#ra_rfc6074) | Provisioning, Auto-Discovery, and Signaling in Layer 2 Virtual Private Networks (L2VPNs) | [PW](#ra_pw) | deep | none verified in index | 2 | 1 |
| [RFC 6107](#ra_rfc6107) | Procedures for Dynamically Signaled Hierarchical Label Switched Paths | [RSVP](#ra_rsvp) | read | exist, not read | 0 | 0 |
| [RFC 6119](#ra_rfc6119) | IPv6 Traffic Engineering in IS-IS | [IS-IS](#ra_isis) | deep | none verified in index | 1 | 1 |
| [RFC 6125](#ra_rfc6125) | Representation and Verification of Domain-Based Application Service Identity within Intern | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6138](#ra_rfc6138) | LDP IGP Synchronization for Broadcast Networks | [MPLS/LDP](#ra_ldp) | read | none verified in index | 0 | 0 |
| [RFC 6213](#ra_rfc6213) | IS-IS BFD-Enabled TLV | [IS-IS](#ra_isis) | deep | none verified in index | 1 | 1 |
| [RFC 6232](#ra_rfc6232) | Purge Originator Identification TLV for IS-IS | [IS-IS](#ra_isis) | deep | none verified in index | 1 | 0 |
| [RFC 6233](#ra_rfc6233) | IS-IS Registry Extension for Purges | [IS-IS](#ra_isis) | deep | none verified in index | 1 | 0 |
| [RFC 6234](#ra_rfc6234) | US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF) | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6286](#ra_rfc6286) | Autonomous-System-Wide Unique BGP Identifier for BGP-4 | [BGP](#ra_bgp) | deep | none verified in index | 1 | 1 |
| [RFC 6368](#ra_rfc6368) | Internal BGP as the Provider/Customer Edge Protocol for BGP/MPLS IP Virtual Private Networ | [BGP](#ra_bgp) | deep | exist, not read | 1 | 0 |
| [RFC 6370](#ra_rfc6370) | MPLS Transport Profile (MPLS-TP) Identifiers | [MPLS/LDP](#ra_ldp) | light | none verified in index | 0 | 0 |
| [RFC 6378](#ra_rfc6378) | MPLS Transport Profile (MPLS-TP) Linear Protection | [MPLS/LDP](#ra_ldp) | light | none verified in index | 0 | 0 |
| [RFC 6388](#ra_rfc6388) | Label Distribution Protocol Extensions for Point-to-Multipoint and Multipoint-to-Multipoin | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 3 | 0 |
| [RFC 6389](#ra_rfc6389) | MPLS Upstream Label Assignment for LDP | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 1 | 1 |
| [RFC 6391](#ra_rfc6391) | Flow-Aware Transport of Pseudowires over an MPLS Packet Switched Network | [PW](#ra_pw) | deep | none verified in index | 1 | 1 |
| [RFC 6398](#ra_rfc6398) | IP Router Alert Considerations and Usage | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6425](#ra_rfc6425) | Detecting Data-Plane Failures in Point-to-Multipoint MPLS - Extensions to LSP Ping | [OAM](#ra_oam) | deep | checked | 2 | 0 |
| [RFC 6426](#ra_rfc6426) | MPLS On-Demand Connectivity Verification and Route Tracing | [OAM](#ra_oam) | deep | exist, not read | 4 | 2 |
| [RFC 6454](#ra_rfc6454) | The Web Origin Concept | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6455](#ra_rfc6455) | The WebSocket Protocol | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6512](#ra_rfc6512) | Using Multipoint LDP When the Backbone Has No Route to the Root | [MPLS/LDP](#ra_ldp) | deep | exist, not read | 0 | 0 |
| [RFC 6513](#ra_rfc6513) | Multicast in MPLS/BGP IP VPNs | [Multicast](#ra_mcast) | deep | checked | 2 | 0 |
| [RFC 6514](#ra_rfc6514) | BGP Encodings and Procedures for Multicast in MPLS/BGP IP VPNs | [Multicast](#ra_mcast) | deep | checked | 2 | 0 |
| [RFC 6515](#ra_rfc6515) | IPv4 and IPv6 Infrastructure Addresses in BGP Updates for Multicast VPN | [Multicast](#ra_mcast) | deep | none verified in index | 1 | 0 |
| [RFC 6583](#ra_rfc6583) | Operational Neighbor Discovery Problems | [IP](#ra_ip) | read | none verified in index | 0 | 0 |
| [RFC 6608](#ra_rfc6608) | Subcodes for BGP Finite State Machine Error | [BGP](#ra_bgp) | deep | none verified in index | 1 | 0 |
| [RFC 6625](#ra_rfc6625) | Wildcards in Multicast VPN Auto-Discovery Routes | [Multicast](#ra_mcast) | deep | checked | 1 | 0 |
| [RFC 6667](#ra_rfc6667) | LDP 'Typed Wildcard' Forwarding Equivalence Class (FEC) for PWid and Generalized PWid FEC  | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 0 | 0 |
| [RFC 6718](#ra_rfc6718) | Pseudowire Redundancy | [PW](#ra_pw) | deep | none verified in index | 1 | 0 |
| [RFC 6720](#ra_rfc6720) | The Generalized TTL Security Mechanism (GTSM) for the Label Distribution Protocol (LDP) | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 1 | 0 |
| [RFC 6790](#ra_rfc6790) | The Use of Entropy Labels in MPLS Forwarding | [MPLS/LDP](#ra_ldp) | deep | checked | 1 | 0 |
| [RFC 6793](#ra_rfc6793) | BGP Support for Four-Octet Autonomous System (AS) Number Space | [BGP](#ra_bgp) | deep | checked | 1 | 0 |
| [RFC 6805](#ra_rfc6805) | The Application of the Path Computation Element Architecture to the Determination of a Seq | [PCEP](#ra_pcep) | read | none verified in index | 0 | 0 |
| [RFC 6826](#ra_rfc6826) | Multipoint LDP In-Band Signaling for Point-to-Multipoint and Multipoint-to-Multipoint Labe | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 0 | 0 |
| [RFC 6870](#ra_rfc6870) | Pseudowire Preferential Forwarding Status Bit | [PW](#ra_pw) | deep | checked | 2 | 0 |
| [RFC 6890](#ra_rfc6890) | Special-Purpose IP Address Registries | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6901](#ra_rfc6901) | JavaScript Object Notation (JSON) Pointer | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6938](#ra_rfc6938) | Deprecation of BGP Path Attributes: DPA, ADVERTISER, and RCID_PATH / CLUSTER_ID | [BGP](#ra_bgp) | light | none verified in index | 0 | 0 |
| [RFC 6979](#ra_rfc6979) | Deterministic Usage of the Digital Signature Algorithm (DSA) and Elliptic Curve Digital Si | [IP](#ra_ip) | light | exist, not read | 0 | 0 |
| [RFC 6980](#ra_rfc6980) | Security Implications of IPv6 Fragmentation with IPv6 Neighbor Discovery | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 6996](#ra_rfc6996) | Autonomous System (AS) Reservation for Private Use | [BGP](#ra_bgp) | light | none verified in index | 0 | 0 |
| [RFC 7032](#ra_rfc7032) | LDP Downstream-on-Demand in Seamless MPLS | [MPLS/LDP](#ra_ldp) | read | none verified in index | 0 | 0 |
| [RFC 7110](#ra_rfc7110) | Return Path Specified Label Switched Path (LSP) Ping | [OAM](#ra_oam) | deep | checked | 2 | 1 |
| [RFC 7112](#ra_rfc7112) | Implications of Oversized IPv6 Header Chains | [IP](#ra_ip) | light | none verified in index | 0 | 0 |
| [RFC 7130](#ra_rfc7130) | Bidirectional Forwarding Detection (BFD) on Link Aggregation Group (LAG) Interfaces | [OAM](#ra_oam) | deep | checked | 2 | 0 |
| [RFC 7140](#ra_rfc7140) | LDP Extensions for Hub and Spoke Multipoint Label Switched Path | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 1 | 0 |
| [RFC 7153](#ra_rfc7153) | IANA Registries for BGP Extended Communities | [BGP](#ra_bgp) | read | none verified in index | 0 | 0 |
| [RFC 7246](#ra_rfc7246) | Multipoint Label Distribution Protocol In-Band Signaling in a Virtual Routing and Forwardi | [MPLS/LDP](#ra_ldp) | read | none verified in index | 0 | 0 |
| [RFC 7267](#ra_rfc7267) | Dynamic Placement of Multi-Segment Pseudowires | [PW](#ra_pw) | read | none verified in index | 0 | 0 |
| [RFC 7274](#ra_rfc7274) | Allocating and Retiring Special-Purpose MPLS Labels | [MPLS/LDP](#ra_ldp) | read | none verified in index | 0 | 0 |
| [RFC 7275](#ra_rfc7275) | Inter-Chassis Communication Protocol for Layer 2 Virtual Private Network (L2VPN) Provider  | [PW](#ra_pw) | deep | none verified in index | 5 | 2 |
| [RFC 7300](#ra_rfc7300) | Reservation of Last Autonomous System (AS) Numbers | [BGP](#ra_bgp) | light | none verified in index | 0 | 0 |
| [RFC 7307](#ra_rfc7307) | LDP Extensions for Multi-Topology | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 3 | 2 |
| [RFC 7308](#ra_rfc7308) | Extended Administrative Groups in MPLS Traffic Engineering (MPLS-TE) | [IS-IS](#ra_isis) | deep | none verified in index | 1 | 1 |
| [RFC 7311](#ra_rfc7311) | The Accumulated IGP Metric Attribute for BGP | [BGP](#ra_bgp) | deep | none verified in index | 2 | 1 |
| [RFC 7313](#ra_rfc7313) | Enhanced Route Refresh Capability for BGP-4 | [BGP](#ra_bgp) | deep | none verified in index | 2 | 0 |
| [RFC 7338](#ra_rfc7338) | Requirements and Framework for Point-to-Multipoint Pseudowires over MPLS Packet Switched N | [PW](#ra_pw) | light | none verified in index | 0 | 0 |
| [RFC 7349](#ra_rfc7349) | LDP Hello Cryptographic Authentication | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 4 | 3 |
| [RFC 7358](#ra_rfc7358) | Label Advertisement Discipline for LDP Forwarding Equivalence Classes (FECs) | [MPLS/LDP](#ra_ldp) | read | none verified in index | 0 | 0 |
| [RFC 7361](#ra_rfc7361) | LDP Extensions for Optimized MAC Address Withdrawal in a Hierarchical Virtual Private LAN  | [PW](#ra_pw) | deep | checked | 2 | 0 |
| [RFC 7385](#ra_rfc7385) | IANA Registry for P-Multicast Service Interface (PMSI) Tunnel Type Code Points | [Multicast](#ra_mcast) | light | none verified in index | 0 | 0 |
| [RFC 7438](#ra_rfc7438) | Multipoint LDP (mLDP) In-Band Signaling with Wildcards | [MPLS/LDP](#ra_ldp) | deep | none verified in index | 0 | 0 |
| [RFC 7442](#ra_rfc7442) | Carrying Protocol Independent Multicast - Sparse Mode (PIM-SM) in Any-Source Multicast (AS | [Multicast](#ra_mcast) | deep | not checked | 1 | 0 |
| [RFC 7447](#ra_rfc7447) | Deprecation of BGP Entropy Label Capability Attribute | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 7473](#ra_rfc7473) | Controlling State Advertisements of Non-negotiated LDP Applications | [MPLS/LDP](#ra_ldp) | deep | not checked | 2 | 2 |
| [RFC 7490](#ra_rfc7490) | Remote Loop-Free Alternate (LFA) Fast Reroute (FRR) | [IS-IS](#ra_isis) | deep | no page found | 2 | 1 |
| [RFC 7506](#ra_rfc7506) | IPv6 Router Alert Option for MPLS Operations, Administration, and Maintenance (OAM) | [OAM](#ra_oam) | deep | not checked | 0 | 0 |
| [RFC 7524](#ra_rfc7524) | Inter-Area Point-to-Multipoint (P2MP) Segmented Label Switched Paths (LSPs) | [Multicast](#ra_mcast) | part | no page found | 1 | 0 |
| [RFC 7525](#ra_rfc7525) | Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport La | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 7552](#ra_rfc7552) | Updates to LDP for IPv6 | [MPLS/LDP](#ra_ldp) | deep | checked | 3 | 1 |
| [RFC 7570](#ra_rfc7570) | Label Switched Path (LSP) Attribute in the Explicit Route Object (ERO) | [RSVP](#ra_rsvp) | deep | not checked | 1 | 1 |
| [RFC 7606](#ra_rfc7606) | Revised Error Handling for BGP UPDATE Messages | [BGP](#ra_bgp) | deep | checked | 4 | 1 |
| [RFC 7607](#ra_rfc7607) | Codification of AS 0 Processing | [BGP](#ra_bgp) | deep | no page found | 2 | 1 |
| [RFC 7611](#ra_rfc7611) | BGP ACCEPT_OWN Community Attribute | [BGP](#ra_bgp) | read | not checked | 1 | 0 |
| [RFC 7679](#ra_rfc7679) | A One-Way Delay Metric for IP Performance Metrics (IPPM) | [OAM](#ra_oam) | light | not checked | 0 | 0 |
| [RFC 7680](#ra_rfc7680) | A One-Way Loss Metric for IP Performance Metrics (IPPM) | [OAM](#ra_oam) | light | not checked | 0 | 0 |
| [RFC 7715](#ra_rfc7715) | Multipoint LDP (mLDP) Node Protection | [MPLS/LDP](#ra_ldp) | deep | not checked | 1 | 0 |
| [RFC 7717](#ra_rfc7717) | IKEv2-Derived Shared Secret Key for the One-Way Active Measurement Protocol (OWAMP) and Tw | [OAM](#ra_oam) | part | not checked | 0 | 0 |
| [RFC 7726](#ra_rfc7726) | Clarifying Procedures for Establishing BFD Sessions for MPLS Label Switched Paths (LSPs) | [OAM](#ra_oam) | deep | no page found | 3 | 2 |
| [RFC 7748](#ra_rfc7748) | Elliptic Curves for Security | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 7750](#ra_rfc7750) | Differentiated Service Code Point and Explicit Congestion Notification Monitoring in the T | [OAM](#ra_oam) | deep | no page found | 1 | 1 |
| [RFC 7761](#ra_rfc7761) | Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised) | [Multicast](#ra_mcast) | deep | checked | 2 | 0 |
| [RFC 7775](#ra_rfc7775) | IS-IS Route Preference for Extended IP and IPv6 Reachability | [IS-IS](#ra_isis) | deep | not checked | 2 | 1 |
| [RFC 7794](#ra_rfc7794) | IS-IS Prefix Attributes for Extended IPv4 and IPv6 Reachability | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 7811](#ra_rfc7811) | An Algorithm for Computing IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) | [IS-IS](#ra_isis) | part | not checked | 0 | 0 |
| [RFC 7812](#ra_rfc7812) | An Architecture for IP/LDP Fast Reroute Using Maximally Redundant Trees (MRT-FRR) | [IS-IS](#ra_isis) | part | not checked | 1 | 0 |
| [RFC 7820](#ra_rfc7820) | UDP Checksum Complement in the One-Way Active Measurement Protocol (OWAMP) and Two-Way Act | [OAM](#ra_oam) | part | not checked | 0 | 0 |
| [RFC 7897](#ra_rfc7897) | Domain Subobjects for the Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | part | not checked | 0 | 0 |
| [RFC 7911](#ra_rfc7911) | Advertisement of Multiple Paths in BGP | [BGP](#ra_bgp) | deep | no page found | 3 | 1 |
| [RFC 7947](#ra_rfc7947) | Internet Exchange BGP Route Server | [BGP](#ra_bgp) | deep | not checked | 1 | 1 |
| [RFC 7948](#ra_rfc7948) | Internet Exchange BGP Route Server Operations | [BGP](#ra_bgp) | light | not checked | 0 | 0 |
| [RFC 7981](#ra_rfc7981) | IS-IS Extensions for Advertising Router Information | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 7999](#ra_rfc7999) | BLACKHOLE Community | [BGP](#ra_bgp) | deep | not checked | 1 | 0 |
| [RFC 8017](#ra_rfc8017) | PKCS #1: RSA Cryptography Specifications Version 2.2 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8029](#ra_rfc8029) | Detecting Multiprotocol Label Switched (MPLS) Data-Plane Failures | [OAM](#ra_oam) | deep | checked | 1 | 0 |
| [RFC 8032](#ra_rfc8032) | Edwards-Curve Digital Signature Algorithm (EdDSA) | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8077](#ra_rfc8077) | Pseudowire Setup and Maintenance Using the Label Distribution Protocol (LDP) | [PW](#ra_pw) | deep | checked | 1 | 0 |
| [RFC 8092](#ra_rfc8092) | BGP Large Communities Attribute | [BGP](#ra_bgp) | deep | checked | 1 | 0 |
| [RFC 8093](#ra_rfc8093) | Deprecation of BGP Path Attribute Values 30, 31, 129, 241, 242, and 243 | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8102](#ra_rfc8102) | Remote-LFA Node Protection and Manageability | [IS-IS](#ra_isis) | deep | not checked | 1 | 0 |
| [RFC 8169](#ra_rfc8169) | Residence Time Measurement in MPLS Networks | [RSVP](#ra_rsvp) | part | no page found | 2 | 2 |
| [RFC 8186](#ra_rfc8186) | Support of the IEEE 1588 Timestamp Format in a Two-Way Active Measurement Protocol (TWAMP) | [OAM](#ra_oam) | deep | not checked | 0 | 0 |
| [RFC 8200](#ra_rfc8200) | Internet Protocol, Version 6 (IPv6) Specification | [IP](#ra_ip) | part | checked | 1 | 0 |
| [RFC 8201](#ra_rfc8201) | Path MTU Discovery for IP version 6 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8202](#ra_rfc8202) | IS-IS Multi-Instance | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 8205](#ra_rfc8205) | BGPsec Protocol Specification | [BGP](#ra_bgp) | light | not checked | 0 | 0 |
| [RFC 8212](#ra_rfc8212) | Default External BGP (EBGP) Route Propagation Behavior without Policies | [BGP](#ra_bgp) | deep | no page found | 1 | 0 |
| [RFC 8223](#ra_rfc8223) | Application-Aware Targeted LDP | [MPLS/LDP](#ra_ldp) | deep | not checked | 1 | 0 |
| [RFC 8231](#ra_rfc8231) | Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE | [PCEP](#ra_pcep) | deep | checked | 5 | 1 |
| [RFC 8232](#ra_rfc8232) | Optimizations of Label Switched Path State Synchronization Procedures for a Stateful PCE | [PCEP](#ra_pcep) | deep | no page found | 5 | 2 |
| [RFC 8233](#ra_rfc8233) | Extensions to the Path Computation Element Communication Protocol (PCEP) to Compute Servic | [PCEP](#ra_pcep) | deep | checked | 5 | 3 |
| [RFC 8253](#ra_rfc8253) | PCEPS: Usage of TLS to Provide a Secure Transport for the Path Computation Element Communi | [PCEP](#ra_pcep) | deep | checked | 1 | 0 |
| [RFC 8259](#ra_rfc8259) | The JavaScript Object Notation (JSON) Data Interchange Format | [IP](#ra_ip) | deep | checked | 1 | 0 |
| [RFC 8271](#ra_rfc8271) | Updates to the Resource Reservation Protocol for Fast Reroute of Traffic Engineering GMPLS | [RSVP](#ra_rsvp) | part | not checked | 1 | 1 |
| [RFC 8277](#ra_rfc8277) | Using BGP to Bind MPLS Labels to Address Prefixes | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8281](#ra_rfc8281) | Path Computation Element Communication Protocol (PCEP) Extensions for PCE-Initiated LSP Se | [PCEP](#ra_pcep) | deep | checked | 1 | 0 |
| [RFC 8287](#ra_rfc8287) | Label Switched Path (LSP) Ping/Traceroute for Segment Routing (SR) IGP-Prefix and IGP-Adja | [OAM](#ra_oam) | deep | checked | 2 | 1 |
| [RFC 8306](#ra_rfc8306) | Extensions to the Path Computation Element Communication Protocol (PCEP) for Point-to-Mult | [PCEP](#ra_pcep) | deep | checked | 6 | 2 |
| [RFC 8320](#ra_rfc8320) | LDP Extensions to Support Maximally Redundant Trees | [MPLS/LDP](#ra_ldp) | deep | no page found | 2 | 1 |
| [RFC 8326](#ra_rfc8326) | Graceful BGP Session Shutdown | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8333](#ra_rfc8333) | Micro-loop Prevention by Introducing a Local Convergence Delay | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 8338](#ra_rfc8338) | Signaling Root-Initiated Point-to-Multipoint Pseudowire Using LDP | [PW](#ra_pw) | deep | not checked | 1 | 1 |
| [RFC 8356](#ra_rfc8356) | Experimental Codepoint Allocation for the Path Computation Element Communication Protocol  | [MPLS/LDP](#ra_ldp) | deep | no page found | 2 | 1 |
| [RFC 8402](#ra_rfc8402) | Segment Routing Architecture | [IS-IS](#ra_isis) | part | checked | 1 | 0 |
| [RFC 8405](#ra_rfc8405) | Shortest Path First (SPF) Back-Off Delay Algorithm for Link-State IGPs | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 8408](#ra_rfc8408) | Conveying Path Setup Type in PCE Communication Protocol (PCEP) Messages | [PCEP](#ra_pcep) | deep | no page found | 2 | 0 |
| [RFC 8439](#ra_rfc8439) | ChaCha20 and Poly1305 for IETF Protocols | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8446](#ra_rfc8446) | The Transport Layer Security (TLS) Protocol Version 1.3 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8448](#ra_rfc8448) | Example Handshake Traces for TLS 1.3 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 8491](#ra_rfc8491) | Signaling Maximum SID Depth (MSD) Using IS-IS | [IS-IS](#ra_isis) | deep | not checked | 1 | 0 |
| [RFC 8538](#ra_rfc8538) | Notification Message Support for BGP Graceful Restart | [BGP](#ra_bgp) | deep | no page found | 2 | 1 |
| [RFC 8545](#ra_rfc8545) | Well-Known Port Assignments for the One-Way Active Measurement Protocol (OWAMP) and the Tw | [OAM](#ra_oam) | read | not checked | 0 | 0 |
| [RFC 8570](#ra_rfc8570) | IS-IS Traffic Engineering (TE) Metric Extensions | [IS-IS](#ra_isis) | deep | checked | 4 | 1 |
| [RFC 8571](#ra_rfc8571) | BGP - Link State (BGP-LS) Advertisement of IGP Traffic Engineering Performance Metric Exte | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8623](#ra_rfc8623) | Stateful Path Computation Element (PCE) Protocol Extensions for Usage with Point-to-Multip | [PCEP](#ra_pcep) | deep | no page found | 7 | 5 |
| [RFC 8654](#ra_rfc8654) | Extended Message Support for BGP | [BGP](#ra_bgp) | deep | no page found | 2 | 1 |
| [RFC 8660](#ra_rfc8660) | Segment Routing with the MPLS Data Plane | [IS-IS](#ra_isis) | deep | not checked | 1 | 0 |
| [RFC 8661](#ra_rfc8661) | Segment Routing MPLS Interworking with LDP | [IS-IS](#ra_isis) | part | no page found | 2 | 1 |
| [RFC 8664](#ra_rfc8664) | Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing | [PCEP](#ra_pcep) | deep | checked | 1 | 1 |
| [RFC 8667](#ra_rfc8667) | IS-IS Extensions for Segment Routing | [IS-IS](#ra_isis) | deep | checked | 1 | 0 |
| [RFC 8668](#ra_rfc8668) | Advertising Layer 2 Bundle Member Link Attributes in IS-IS | [IS-IS](#ra_isis) | deep | checked | 2 | 1 |
| [RFC 8669](#ra_rfc8669) | Segment Routing Prefix Segment Identifier Extensions for BGP | [BGP](#ra_bgp) | deep | checked | 2 | 0 |
| [RFC 8685](#ra_rfc8685) | Path Computation Element Communication Protocol (PCEP) Extensions for the Hierarchical Pat | [PCEP](#ra_pcep) | deep | no page found | 5 | 3 |
| [RFC 8697](#ra_rfc8697) | Path Computation Element Communication Protocol (PCEP) Extensions for Establishing Relatio | [PCEP](#ra_pcep) | deep | no page found | 3 | 1 |
| [RFC 8706](#ra_rfc8706) | Restart Signaling for IS-IS | [IS-IS](#ra_isis) | deep | no page found | 0 | 0 |
| [RFC 8741](#ra_rfc8741) | Ability for a Stateful Path Computation Element (PCE) to Request and Obtain Control of a L | [PCEP](#ra_pcep) | deep | not checked | 1 | 0 |
| [RFC 8745](#ra_rfc8745) | Path Computation Element Communication Protocol (PCEP) Extensions for Associating Working  | [PCEP](#ra_pcep) | deep | no page found | 3 | 1 |
| [RFC 8751](#ra_rfc8751) | Hierarchical Stateful Path Computation Element (PCE) | [PCEP](#ra_pcep) | light | not checked | 0 | 0 |
| [RFC 8754](#ra_rfc8754) | IPv6 Segment Routing Header (SRH) | [IS-IS](#ra_isis) | light | not checked | 0 | 0 |
| [RFC 8762](#ra_rfc8762) | Simple Two-Way Active Measurement Protocol | [OAM](#ra_oam) | deep | checked | 3 | 1 |
| [RFC 8779](#ra_rfc8779) | Path Computation Element Communication Protocol (PCEP) Extensions for GMPLS | [PCEP](#ra_pcep) | part | not checked | 2 | 1 |
| [RFC 8786](#ra_rfc8786) | Updated Rules for Processing Stateful PCE Request Parameters Flags | [PCEP](#ra_pcep) | deep | not checked | 0 | 0 |
| [RFC 8800](#ra_rfc8800) | Path Computation Element Communication Protocol (PCEP) Extension for Label Switched Path ( | [PCEP](#ra_pcep) | deep | no page found | 3 | 2 |
| [RFC 8814](#ra_rfc8814) | Signaling Maximum SID Depth (MSD) Using the Border Gateway Protocol - Link State | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8950](#ra_rfc8950) | Advertising IPv4 Network Layer Reachability Information (NLRI) with an IPv6 Next Hop | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 8972](#ra_rfc8972) | Simple Two-Way Active Measurement Protocol Optional Extensions | [OAM](#ra_oam) | part | checked | 1 | 1 |
| [RFC 8986](#ra_rfc8986) | Segment Routing over IPv6 (SRv6) Network Programming | [IS-IS](#ra_isis) | light | not checked | 0 | 0 |
| [RFC 9000](#ra_rfc9000) | QUIC: A UDP-Based Multiplexed and Secure Transport | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9001](#ra_rfc9001) | Using TLS to Secure QUIC | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9002](#ra_rfc9002) | QUIC Loss Detection and Congestion Control | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9003](#ra_rfc9003) | Extended BGP Administrative Shutdown Communication | [BGP](#ra_bgp) | deep | not checked | 1 | 0 |
| [RFC 9005](#ra_rfc9005) | Path Computation Element Communication Protocol (PCEP) Extension for Associating Policies  | [PCEP](#ra_pcep) | deep | not checked | 0 | 0 |
| [RFC 9012](#ra_rfc9012) | The BGP Tunnel Encapsulation Attribute | [BGP](#ra_bgp) | part | no page found | 0 | 0 |
| [RFC 9015](#ra_rfc9015) | BGP Control Plane for the Network Service Header in Service Function Chaining | [BGP](#ra_bgp) | light | not checked | 0 | 0 |
| [RFC 9026](#ra_rfc9026) | Multicast VPN Fast Upstream Failover | [Multicast](#ra_mcast) | light | not checked | 0 | 0 |
| [RFC 9050](#ra_rfc9050) | Path Computation Element Communication Protocol (PCEP) Procedures and Extensions for Using | [PCEP](#ra_pcep) | deep | no page found | 7 | 3 |
| [RFC 9059](#ra_rfc9059) | Path Computation Element Communication Protocol (PCEP) Extensions for Associated Bidirecti | [PCEP](#ra_pcep) | deep | no page found | 3 | 1 |
| [RFC 9072](#ra_rfc9072) | Extended Optional Parameters Length for BGP OPEN Message | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 9085](#ra_rfc9085) | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing | [BGP](#ra_bgp) | part | not checked | 0 | 0 |
| [RFC 9086](#ra_rfc9086) | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing BGP Egress Pe | [BGP](#ra_bgp) | part | not checked | 0 | 0 |
| [RFC 9088](#ra_rfc9088) | Signaling Entropy Label Capability and Entropy Readable Label Depth Using IS-IS | [BGP](#ra_bgp) | deep | not checked | 0 | 0 |
| [RFC 9104](#ra_rfc9104) | Distribution of Traffic Engineering Extended Administrative Groups Using the Border Gatewa | [BGP](#ra_bgp) | deep | not checked | 1 | 0 |
| [RFC 9110](#ra_rfc9110) | HTTP Semantics | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9112](#ra_rfc9112) | HTTP/1.1 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9114](#ra_rfc9114) | HTTP/3 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9204](#ra_rfc9204) | QPACK: Field Compression for HTTP/3 | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9234](#ra_rfc9234) | Route Leak Prevention and Detection Using Roles in UPDATE and OPEN Messages | [BGP](#ra_bgp) | deep | no page found | 3 | 1 |
| [RFC 9256](#ra_rfc9256) | Segment Routing Policy Architecture | [IS-IS](#ra_isis) | light | not checked | 0 | 0 |
| [RFC 9294](#ra_rfc9294) | Application-Specific Link Attributes Advertisement Using the Border Gateway Protocol - Lin | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 9325](#ra_rfc9325) | Recommendations for Secure Use of Transport Layer Security (TLS) and Datagram Transport La | [IP](#ra_ip) | light | not checked | 0 | 0 |
| [RFC 9346](#ra_rfc9346) | IS-IS Extensions in Support of Inter-Autonomous System (AS) MPLS and GMPLS Traffic Enginee | [IS-IS](#ra_isis) | deep | no page found | 2 | 2 |
| [RFC 9350](#ra_rfc9350) | IGP Flexible Algorithm | [IS-IS](#ra_isis) | deep | checked | 2 | 1 |
| [RFC 9352](#ra_rfc9352) | IS-IS Extensions to Support Segment Routing over the IPv6 Data Plane | [IS-IS](#ra_isis) | deep | no page found | 4 | 1 |
| [RFC 9357](#ra_rfc9357) | Label Switched Path (LSP) Object Flag Extension for Stateful PCE | [PCEP](#ra_pcep) | deep | not checked | 1 | 0 |
| [RFC 9377](#ra_rfc9377) | IS-IS Flood Reflection | [IS-IS](#ra_isis) | deep | no page found | 2 | 1 |
| [RFC 9384](#ra_rfc9384) | A BGP Cease NOTIFICATION Subcode for Bidirectional Forwarding Detection (BFD) | [BGP](#ra_bgp) | deep | not checked | 1 | 0 |
| [RFC 9479](#ra_rfc9479) | IS-IS Application-Specific Link Attributes | [IS-IS](#ra_isis) | deep | no page found | 2 | 0 |
| [RFC 9488](#ra_rfc9488) | Local Protection Enforcement in the Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | deep | not checked | 0 | 0 |
| [RFC 9494](#ra_rfc9494) | Long-Lived Graceful Restart for BGP | [BGP](#ra_bgp) | deep | no page found | 3 | 1 |
| [RFC 9502](#ra_rfc9502) | IGP Flexible Algorithm in IP Networks | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 9514](#ra_rfc9514) | Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing over IPv6 (SR | [BGP](#ra_bgp) | part | not checked | 0 | 0 |
| [RFC 9525](#ra_rfc9525) | Service Identity in TLS | [IP](#ra_ip) | part | not checked | 1 | 0 |
| [RFC 9552](#ra_rfc9552) | Distribution of Link-State and Traffic Engineering Information Using BGP | [BGP](#ra_bgp) | deep | checked | 2 | 0 |
| [RFC 9603](#ra_rfc9603) | Path Computation Element Communication Protocol (PCEP) Extensions for IPv6 Segment Routing | [PCEP](#ra_pcep) | deep | no page found | 4 | 2 |
| [RFC 9604](#ra_rfc9604) | Carrying Binding Label/SID in PCE-Based Networks | [PCEP](#ra_pcep) | deep | not checked | 3 | 2 |
| [RFC 9658](#ra_rfc9658) | Multipoint LDP Extensions for Multi-Topology Routing | [MPLS/LDP](#ra_ldp) | deep | not checked | 1 | 0 |
| [RFC 9687](#ra_rfc9687) | Border Gateway Protocol 4 (BGP-4) Send Hold Timer | [BGP](#ra_bgp) | deep | no page found | 1 | 0 |
| [RFC 9757](#ra_rfc9757) | Path Computation Element Communication Protocol (PCEP) Extensions for Native IP Networks | [PCEP](#ra_pcep) | light | not checked | 0 | 0 |
| [RFC 9774](#ra_rfc9774) | Deprecation of AS_SET and AS_CONFED_SET in BGP | [BGP](#ra_bgp) | deep | no page found | 1 | 1 |
| [RFC 9776](#ra_rfc9776) | Internet Group Management Protocol, Version 3 | [Multicast](#ra_mcast) | deep | not checked | 2 | 1 |
| [RFC 9777](#ra_rfc9777) | Multicast Listener Discovery Version 2 (MLDv2) for IPv6 | [Multicast](#ra_mcast) | deep | not checked | 1 | 1 |
| [RFC 9789](#ra_rfc9789) | MPLS Network Actions (MNAs) Framework | [MPLS/LDP](#ra_ldp) | light | not checked | 0 | 0 |
| [RFC 9793](#ra_rfc9793) | BGP Extensions for Bit Index Explicit Replication (BIER) | [BGP](#ra_bgp) | light | checked | 0 | 0 |
| [RFC 9800](#ra_rfc9800) | Compressed SRv6 Segment List Encoding | [IS-IS](#ra_isis) | part | not checked | 0 | 0 |
| [RFC 9830](#ra_rfc9830) | Advertising Segment Routing Policies in BGP | [BGP](#ra_bgp) | deep | no page found | 2 | 1 |
| [RFC 9831](#ra_rfc9831) | Segment Type Extensions for BGP Segment Routing (SR) Policy | [BGP](#ra_bgp) | light | not checked | 0 | 0 |
| [RFC 9843](#ra_rfc9843) | IGP Flexible Algorithms: Bandwidth, Delay, Metrics, and Constraints | [IS-IS](#ra_isis) | deep | not checked | 3 | 3 |
| [RFC 9855](#ra_rfc9855) | Topology Independent Fast Reroute Using Segment Routing | [IS-IS](#ra_isis) | deep | not checked | 1 | 1 |
| [RFC 9862](#ra_rfc9862) | Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing (SR) | [PCEP](#ra_pcep) | deep | no page found | 6 | 1 |
| [RFC 9885](#ra_rfc9885) | Multi-Part TLVs in IS-IS | [IS-IS](#ra_isis) | deep | no page found | 2 | 1 |
| [RFC 9917](#ra_rfc9917) | IGP Flexible Algorithms Reverse Affinity Constraint | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 9929](#ra_rfc9929) | IGP Unreachable Prefix Announcement | [IS-IS](#ra_isis) | deep | not checked | 0 | 0 |
| [RFC 9933](#ra_rfc9933) | Carrying SR-Algorithm in Path Computation Element Communication Protocol (PCEP) | [PCEP](#ra_pcep) | light | not checked | 0 | 0 |
| [RFC 10039](#ra_rfc10039) | Interconnecting EVPN and IPVPN Domains | [BGP](#ra_bgp) | light | not checked | 0 | 0 |

