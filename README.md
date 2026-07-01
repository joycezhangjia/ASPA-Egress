# ASPA-Egress

ASPA-based AS_PATH Verification for BGP Export.

## Draft Files

- `draft-zhang-sidrops-aspa-egress-04.xml`: preserved copy of the public IETF v04 XML from the IETF archive.
- `draft-zhang-sidrops-aspa-egress-04.pdf`: existing v04 PDF artifact.
- `draft-zhang-sidrops-aspa-egress-05.xml`: current local working text for the next revision.
- `draft-zhang-sidrops-aspa-egress-05.pdf`: rendered PDF for the current v05 working text.

The previous GitHub working file named `[draft]draft-zhang-sidrops-aspa-egress-04.xml` had already moved beyond the public v04 text. It has therefore been renamed to `draft-zhang-sidrops-aspa-egress-05.xml`, and the public v04 XML has been restored separately.

## v05 Working Notes

The current v05 working text starts from Maria's post-v04 restructuring and incorporates Sriram's March 2026 review concerns where they did not conflict with the intended egress-verification scope.

Changes made in this working update:

- Reframed the Introduction to say that this draft does not question the adequacy of ingress ASPA verification and does not change the ASPA verification procedures.
- Kept both partial deployment and operational assurance as motivations, without ranking one as the only or primary motivation.
- Expanded the partial-deployment scenario and moved it before the missing-provider scenario in Section 3.
- Preserved Maria's operational assurance cases, including missing provider ASPA records, AS migration/renumbering, and AS_PATH manipulation/export-policy mistakes.
- Restored the v04-style egress/ingress figure context and added explicit OTC precedence: OTC or an equivalent intra-AS leak-prevention signal must not be overridden by egress ASPA verification.
- Restored the v04 operational note that egress verification needs reliable information about the local relationship with the egress neighbor AS, which may come from BGP Roles, ASPA objects, or local BGP peering and export-policy configuration.
- Clarified that ASPA objects can represent mutual provider authorization at the AS level, while OTC and BGP Roles are session oriented and may require segregating Complex or mutual-transit relationships into non-Complex sessions where feasible. The draft does not define new BGP Roles or OTC behavior.
- Split the procedure section into `Basic Egress Verification` and `Neighbor-AS-Augmented Verification` so that the basic egress procedure is explicit and NAAV is presented as an additional verification mode.
- Moved neighbor-AS prepending out of the main inline procedure and into a `Neighbor-AS-Augmented Verification` subsection. The text keeps this as a supported verification mode and allows inline enforcement as a matter of local policy, but does not make it part of the mandatory/base egress procedure.
- Added metadata requirements for centralized or Route Reflector based verification: the verifier needs per-egress ASBR, local AS, neighbor AS, BGP Role/local relationship, and export-policy context. The text also clarifies that centralized or Route Reflector based verification is primarily useful for monitoring and operational assurance unless it has accurate per-egress metadata and an enforcement mechanism at the actual egress ASBR.
- Recast "turning off" egress checks as `Deployment Controls` rather than an optimization. The text says controls may be appropriate in narrow cases, but not when the operator still wants egress checks for AS migration, AS_PATH manipulation, ASPA registration omissions, or other export-side operational errors.
- Clarified that partial verification is a scoped optimization and not a relaxation of ASPA-based AS_PATH verification. If the verifier does not have reliable local state about the already verified part of the AS_PATH, full AS_PATH verification should be performed.

## Open Points for Coauthor Review

- Whether `Neighbor-AS-Augmented Verification` should be stronger than the current detached/offline/monitoring-oriented wording.
- Whether the current `SHOULD NOT propagate` handling for Invalid results needs any additional policy-mode text, while keeping `SHOULD NOT propagate` as the default behavior.
- Whether `Deployment Controls` adequately preserves the useful v04 optimization ideas without implying that egress verification is generally unnecessary.

## Notes on ASPA Monitoring

The latest ASPA verification draft includes monitoring-related recommendations, such as providers monitoring whether their AS number is included in customer ASPA SPAS and logging Invalid causes for diagnostics. It does not appear to define a detailed standalone ASPA monitoring procedure. For this reason, the current v05 working text does not rely on ASPA monitoring as a core premise for the egress draft's positioning.
