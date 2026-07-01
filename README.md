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
- Moved neighbor-AS prepending out of the main inline procedure and into a `Neighbor-AS-Augmented Verification` subsection. The text now treats this as a verification mode that should be supported for detached/offline/monitoring use, while inline enforcement is left to local policy.
- Added metadata requirements for centralized or Route Reflector based verification: the verifier needs per-egress ASBR, local AS, neighbor AS, BGP Role/local relationship, and export-policy context.
- Recast "turning off" egress checks as `Deployment Controls` rather than an optimization. The text says controls may be appropriate in narrow cases, but not when the operator still wants egress checks for AS migration, AS_PATH manipulation, ASPA registration omissions, or other export-side operational errors.
- Clarified, after coauthor review, that centralized or Route Reflector based verification is primarily useful for monitoring and operational assurance unless it has accurate per-egress metadata and an enforcement mechanism at the actual egress ASBR.
- Clarified that partial verification is a scoped optimization and not a relaxation of ASPA-based AS_PATH verification.
- Clarified that this draft does not define new BGP Roles or OTC behavior for Complex peering relationships, and instead follows the guidance in RFC 9234.

## Open Points for Coauthor Review

- Whether `Neighbor-AS-Augmented Verification` should be stronger than the current detached/offline/monitoring-oriented wording.
- Whether inline enforcement should remain `SHOULD NOT propagate` for Invalid results, or whether the text should more explicitly describe alert-only and policy-driven deployment modes.
- Whether the restored OTC precedence text is strong enough for complex peering and partial-transit cases.
- Whether the centralized/Route Reflector verification section is acceptable with the added metadata requirements, or should be further narrowed.
- Whether `Deployment Controls` adequately preserves the useful v04 optimization ideas without implying that egress verification is generally unnecessary.

## Handling of Recent Coauthor Comments

- `Neighbor-AS-Augmented Verification`: current text is kept for this revision as a compromise. It supports this verification mode and allows inline enforcement as a matter of local policy, but does not make NAAV part of the mandatory/base egress procedure.
- Invalid handling: current `SHOULD NOT propagate` wording is retained.
- OTC and Complex relationships: no new mutual-transit or Complex-role mechanism is added. The text now makes clear that the draft follows RFC 9234 and does not redefine BGP Roles or OTC behavior.
- Centralized/Route Reflector verification: text is narrowed to emphasize monitoring and operational assurance unless accurate per-egress metadata and an actual enforcement path are available.
- Partial verification: text is clarified so that partial verification cannot be read as skipping necessary ASPA checks without reliable local knowledge.

## Notes on ASPA Monitoring

The latest ASPA verification draft includes monitoring-related recommendations, such as providers monitoring whether their AS number is included in customer ASPA SPAS and logging Invalid causes for diagnostics. It does not appear to define a detailed standalone ASPA monitoring procedure. For this reason, the current v05 working text does not rely on ASPA monitoring as a core premise for the egress draft's positioning.
