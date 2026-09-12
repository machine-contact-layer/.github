# Security policy

This is the organization-wide default. It applies to every Machine Contact
Layer repository that does not carry its own `SECURITY.md`.

**The authoritative policy is
[`mcl-core/SECURITY.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md).**
Read it before reporting anything. It is the version that governs, and where
that document and this one differ, that one wins.

## Read this first: most of what looks like a vulnerability is documented

**MCL v1.0 provides no confidentiality, no peer authentication, no message
integrity in the security sense, and no replay protection.** No cryptography is
implemented in any repository.

These are stated design properties, not defects. Reports that MCL traffic can
be read, forged, replayed, downgraded or flooded describe the specification
working as written, and `mcl-core/SECURITY.md` lists each one explicitly.

Two consequences worth stating plainly:

- `frame_check` is a CRC-32. It detects accidental corruption. Anyone who can
  write to the medium can recompute it. It is **not** an integrity mechanism.
- `session_ref` is correlation, **not** authentication. It says two frames
  belong to one conversation; it does not say the peer is the machine the
  contact began with.

## What is worth reporting

- A frame or state sequence that violates the specification's own stated
  guarantees — a refusal that does not fire, a version rule accepted when it
  should be rejected, a reserved bit honoured instead of dropped
- A defect in the reference implementation that a conforming peer could trigger:
  a buffer overrun, an out-of-bounds read, an unbounded allocation
- A discrepancy between a specification and the code that claims to implement it
- A claim in any repository that the evidence does not actually support

That last one is a security report in this project. A protocol that overstates
what it protects is the failure mode this policy exists to prevent.

## How to report

Follow the process in
[`mcl-core/SECURITY.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md).
For specification defects that are not security-sensitive, use
[`REPORTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/REPORTING.md)
instead — those are tracked as errata and handled in the open.

Contact: [info@ojobit.com](mailto:info@ojobit.com)
