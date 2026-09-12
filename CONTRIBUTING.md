# Contributing to MCL

This is the organization-wide default. It applies to every Machine Contact
Layer repository that does not carry its own `CONTRIBUTING.md`.

**The full guide is
[`mcl-core/CONTRIBUTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/CONTRIBUTING.md).**
Read it before opening a pull request. Everything below is a summary of it.

## Before anything else: run both gate halves

```sh
mcl-core/tools/local-gates.sh        # GCC, Clang, ASan/UBSan, ARM-M0, RV32IM,
                                     # C++ headers, API surface, registries,
                                     # spec index, traceability
mcl-core/tools/local-gates-msvc.ps1  # MSVC /W4 /WX
```

**Neither run alone is "the gates."** A change that passes one and breaks the
other has broken the build. Say the result in your pull request.

Run them locally even though CI will run them too. A red CI run after the fact
is a slower and more public way to learn what one local command would have told
you.

The scripts are authoritative. CI invokes them; it does not reimplement them.
If CI disagrees with your laptop, the script is what both are wrong about.

## The eight repositories are peers

None is a subdirectory of another. The split is by **authority over a
specification**, not by convenience, so a change usually belongs in exactly one
of them:

| If you are changing | It belongs in |
|---|---|
| byte representation of an object | `mcl-wire` |
| framing, sessions, addressing, migration | `mcl-link` |
| a transport binding | `mcl-ip`, `mcl-ble`, `mcl-ap`, `mcl-uwb` |
| the reference implementation or examples | `mcl-sdk` |
| governance, conformance, registries, charter | `mcl-core` |

A change that has to touch several at once is usually a design question first.
Open an issue before the pull request.

## What this project asks for most

**Specification defects.** A clean-room implementation — independent of the
reference code, but written by the same author — found three real
specification-reading defects. A reader who is not the author will find more,
and finding one is the most valuable contribution available right now.

Report those through
[`REPORTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/REPORTING.md).
They are tracked as [errata](https://github.com/machine-contact-layer/mcl-core/tree/main/errata),
in the open.

## Two rules that are not negotiable

**Raw evidence is immutable.** Measurements, capture logs and their recorded
digests are never edited to make something agree. If a digest and a file
disagree, find out which is wrong and say so; a failed measurement stays in the
record with an explanation.

**Never report simulated or fitted results as physical evidence.** The
conformance levels (C0–C6) and evidence levels (E0–E6) are separate axes and
mean different things. `mcl-core/conformance/` defines both.

## Security

See [`SECURITY.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md)
first — MCL v1.0 deliberately provides no confidentiality, authentication,
integrity or replay protection, and those are documented properties rather than
defects.
