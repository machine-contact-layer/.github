<p align="center">
  <img src="https://raw.githubusercontent.com/machine-contact-layer/.github/main/profile/banner.png" alt="OJOBIT" width="100%">
</p>

<h1 align="center">Machine Contact Layer</h1>

<p align="center">
  <strong>A transport-independent layer for machines to meet, and to keep talking.</strong>
</p>

<p align="center">
  <a href="https://github.com/machine-contact-layer/mcl-core/actions/workflows/ci.yml">
    <img alt="core CI" src="https://github.com/machine-contact-layer/mcl-core/actions/workflows/ci.yml/badge.svg"></a>
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/LICENSE">
    <img alt="License Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-blue"></a>
  <img alt="Status: Public Candidate" src="https://img.shields.io/badge/status-Public%20Candidate-orange">
  <img alt="freestanding C99" src="https://img.shields.io/badge/C99-freestanding-informational">
  <img alt="8 repositories" src="https://img.shields.io/badge/repositories-8-lightgrey">
</p>

<p align="center">
  <a href="https://github.com/machine-contact-layer/mcl-sdk/blob/main/QUICKSTART.md"><b>Quickstart</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-core"><b>Specifications</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/conformance/ICS.md"><b>What is claimed</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/REPORTING.md"><b>Report a defect</b></a>
</p>

---

Two machines end up in the same place. They may have been built by different
companies and never designed to work together; or they may both be yours, and
simply have no network in common at this moment. Either way there is no shared
bus, no common credential system, and nobody around to introduce them.

**MCL gives them something they can speak first** — a small, deterministic way to
establish, maintain, validate, refuse, migrate and, when useful, hand off a
continuing contact. What happens after that is the deployment's to decide.

```text
ANOTHER MACHINE
      │  acoustic, BLE advertisement, Wi-Fi — whatever medium exists
      ▼
FIRST CONTACT ............ presence, capabilities, hazards
      │
      │  optional: negotiate a different transport
      ▼
CONTINUING CONTACT ....... often richer or more private — or still acoustic
      │
      ├─▶ STAY ON MCL ......... MCL keeps the contact: presence, capability,
      │                         migration and refusal. NOT your payloads
      ├─▶ SECURITY PROFILE .... optional: establish who you are talking to
      └─▶ HAND OFF ............ your own protocol takes over
```

Those three endings are alternatives, not stages.

MCL is infrastructure for builders. It is not a product, a fleet manager, an
autonomy stack, a credential authority, or a modem.

## Two conformance layers

**`MCL Base 1`** is the v1.0 stable floor, and it is the one most deployments
want. It covers the ordinary case of machines that **already share a bearer**:
provisioned fleets, products paired at manufacture, fixed installations, test
harnesses, and libraries embedded in a larger product. No discovery, no
microphone, no cryptography required.

**`MCL Stranger-Contact 1`** extends Base 1 with an optional zero-prior
rendezvous path, for machines that share no bearer at all. It is an **ingress
capability, not the definition of MCL** — and its acoustic and BLE profiles
remain *Candidate*, not Stable.

Most machine communication today is not stranger communication. Building the
layer around the exceptional case would have been the wrong shape.

**On security:** MCL v1.0 carries no cryptography. The design rule is that MCL
defines the interface a security mechanism plugs into and never the mechanism
itself — you bring your own stack or secure element, and MCL never holds a
private key. That interface is not in this release. Plan for your own
authentication and confidentiality above MCL, or hand off to a protocol that
provides them. [`SECURITY.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md)
is specific about what is and is not protected.

## The repositories

Eight peer repositories. None is a subdirectory of another; the split is by
authority over a specification, not by convenience.

| Repository | What it owns |
|---|---|
| **[mcl-core](https://github.com/machine-contact-layer/mcl-core)** | Architecture charter, governance, conformance, registries, release gate. **Start here.** |
| **[mcl-wire](https://github.com/machine-contact-layer/mcl-wire)** | The canonical deterministic byte representation of MCL semantics |
| **[mcl-link](https://github.com/machine-contact-layer/mcl-link)** | Contact establishment, framing, sessions, addressing, migration |
| **[mcl-sdk](https://github.com/machine-contact-layer/mcl-sdk)** | Reference SDK, examples and the developer archive |
| **[mcl-ap](https://github.com/machine-contact-layer/mcl-ap)** | Acoustic Profile — the bootstrap medium that needs no network |
| **[mcl-ip](https://github.com/machine-contact-layer/mcl-ip)** | IP / datagram binding |
| **[mcl-ble](https://github.com/machine-contact-layer/mcl-ble)** | Bluetooth Low Energy binding |
| **[mcl-uwb](https://github.com/machine-contact-layer/mcl-uwb)** | Ultra-Wideband binding *(specification only — no physical qualification)* |

Transports are **bindings**. A `HAZARD` means the same thing whether it arrived
through a loudspeaker, a Bluetooth advertisement or a UDP datagram; a binding
never redefines semantics.

## Start here

**Building a product on it** → [`mcl-sdk/QUICKSTART.md`](https://github.com/machine-contact-layer/mcl-sdk/blob/main/QUICKSTART.md), section 04.
The `base_arranged_bearer` example is Base 1 end to end: two machines on a
bearer that is already there, Wire major 1 inside Link major 1, no rendezvous
and no bearer to open.

**Implementing the specifications** → [`mcl-core`](https://github.com/machine-contact-layer/mcl-core),
then `mcl-wire` and `mcl-link`. The Implementation Contract is normative;
the reference code is not.

**Evaluating whether to trust it** → [`mcl-core/conformance/ICS.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/conformance/ICS.md)
for what is claimed and at what level, and the release evidence index for every
empirical claim bound to a path and a digest.

## What has actually been run

The reference implementation targets **freestanding C99 with caller-owned
memory** — no heap, no libc required — and is exercised across IP, BLE, acoustic
bootstrap, Windows and Android hosts, and ESP32-S3-class hardware.

- **104 physical-medium changes** preserving one logical contact, including 100
  alternating BLE/IP migrations, with **2,989 recorded checks and zero failures**
- **Zero-prior acoustic rendezvous → policy admission → BLE migration**, verified
  in both derived BLE role orientations, on real hardware
- A **three-machine shared-air run** in which a competing third-party proposal
  did not replace the selected transaction
- The full stack running on an embedded target with **no host in the loop**,
  decoding over air
- **803** independent cross-implementation checks and **108** Stable profile
  interoperability checks *(separate campaigns; they are not summed)*

Negative trials and harness failures are retained as evidence rather than
normalised into success. Every recorded digest is verified by a gate in CI.

## Status

**Public Candidate.** The specifications are published and open for external
review. `v1.0.0` is **not** tagged: the Architecture
Charter requires public external review before any Stable promotion, and
readability is not review.

A clean-room implementation — independent of the reference code, but written by
the same author — found three real specification-reading defects. A reader who
is not the author will find more.

**If you find one, that is the contribution we want most.**
See [`REPORTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/REPORTING.md)
and [`errata/`](https://github.com/machine-contact-layer/mcl-core/tree/main/errata).

## Citing this work

<!-- DOI-SLOT: replace this block when the preprint DOI is issued. -->
> The MCL v1.0 paper is not yet public. A DOI and citation block will be added
> here on publication.

## Contact

**[ojobit.com](https://ojobit.com)** · [info@ojobit.com](mailto:info@ojobit.com)

[X](https://x.com/0J0BIT) ·
[LinkedIn](https://www.linkedin.com/company/ojobit) ·
[GitHub](https://github.com/0j0bit) ·
[Hugging Face](https://huggingface.co/0J0BIT)
