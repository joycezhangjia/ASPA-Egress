# ASPA-Egress
ASPA-based AS_PATH Verification for BGP Export

**draft-zhang-sidrops-aspa-egress-04**: the latest version proposed to IETF sidrops WG

1. Key Updates in Version 04
- Authorship Update: K. Sriram and Nan Geng have been officially added as co-authors.
- Procedure Refinement (Section 3):
    - Add Section 3.1 (Utility of OTC Attribute): Clarifies why egress verification alone may yield incorrect results in complex peering scenarios and how OTC complements it.
    - Add Section 3.2 (Consideration of Complex BGP Sessions): Provides guidance on handling complex relationships.
- New Optimization Section (Section 4): Introduced strategies to minimize processing overhead, such as centralized processing for full tables and operational switches to disable egress verification when ingress ASPA + OTC is fully deployed.
- Editorial Cleanup: Extensive improvements to the Abstract, Introduction, and overall readability.

2. Plan for Version 05 (Target: Before IETF 125, March 2)
- Out-of-Band Verification (Maria):
- "Prepend Neighbor AS" Option (Yangyang & Maria):
Add an "Implementation Note" or similar subsection describing an optional/command-line feature for prepending the neighbor AS. This will be presented as a strict mode for diagnostics/debugging.
- BGP Roles for Self-Check (Nan):
Refine the "Operational Considerations" to explicitly mention using negotiated BGP Roles to detect local ASPA registration errors (early detection).