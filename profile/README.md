<p align="center">
  <img src="https://raw.githubusercontent.com/machine-contact-layer/.github/main/profile/banner.png" alt="Machine Contact Layer (MCL) banner: black and white checkerboard with the OJOBIT wordmark" width="100%">
</p>

<h1 align="center">Machine Contact Layer (MCL)</h1>

<p align="center">
  <strong>A transport-independent layer for machines to meet, and to keep talking.</strong>
</p>

<p align="center">
  Open machine-to-machine protocol and portable C99 stack for device discovery,
  contact, transport negotiation and communication continuity across BLE, IP
  and acoustic links.
</p>

<p align="center">
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/LICENSE"><img alt="License: Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-blue"></a>
  <img alt="Release status: Public Candidate" src="https://img.shields.io/badge/status-Public%20Candidate-orange">
  <img alt="Language: freestanding C99" src="https://img.shields.io/badge/C99-freestanding-informational">
</p>

<p align="center">
  <a href="https://github.com/machine-contact-layer/mcl-sdk/blob/main/QUICKSTART.md"><b>Quickstart</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-sdk"><b>SDK</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-sdk/tree/main/examples"><b>Examples</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/SPECIFICATION_INDEX.md"><b>Specifications</b></a> ·
  <a href="https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md"><b>Security</b></a>
</p>

---

MCL lets machines establish contact even when they were built independently, do
not start on the same network, or need to move an existing contact from one
transport to another. It runs on a microcontroller as readily as on a server —
freestanding C99, no heap, no libc — and leaves your application protocol, your
admission policy and your security stack to you.

```text
  your application or domain protocol        MQTT · ROS 2 · DDS · HTTP · your own
                 ▲
                 │  hand off — or keep the contact on MCL
                 │
  MACHINE CONTACT LAYER                      contact · negotiation · migration · refusal
                 │
       ┌─────────┼──────────┬───────────┐
      BLE        IP      acoustic      UWB (experimental)
```

MCL does not replace MQTT, ROS 2, DDS, HTTP or CAN. It is the layer before or
alongside them: establishing contact, agreeing a compatible transport, refusing
incompatible input and keeping the contact while the bearer changes.

## Use it for

- **Robotics** — robots and autonomous machines from different fleets meet,
  exchange presence and transport offers, and move to a shared network or a
  fleet protocol
- **Embedded and IoT devices** — devices from different vendors share one
  contact layer without a common OS, runtime or cloud service
- **Provisioned fleets** — machines that already share a bearer use `MCL Base 1`
  directly, with no discovery step
- **Offline and degraded networking** — contact over BLE or sound where there is
  no infrastructure, then migration when a better bearer appears
- **Cross-transport systems** — one contact that starts on one link and
  continues on another

## Start here

**Build** → [`mcl-sdk/QUICKSTART.md`](https://github.com/machine-contact-layer/mcl-sdk/blob/main/QUICKSTART.md)
takes you from download to two machines in contact. The release ships a
self-contained developer SDK: one CMake project, no sibling checkout.

**Understand** → [`mcl-core`](https://github.com/machine-contact-layer/mcl-core)
explains what MCL is, how it works, and where each specification lives.

**Implement** → the specifications, registries and conformance vectors are the
contract; the reference code is subordinate to them. Start from
[`SPECIFICATION_INDEX.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SPECIFICATION_INDEX.md).

## Repositories

| Repository | What it contains |
|---|---|
| **[mcl-core](https://github.com/machine-contact-layer/mcl-core)** | Machine semantics, protocol specifications, registries, conformance model. **Start here.** |
| **[mcl-sdk](https://github.com/machine-contact-layer/mcl-sdk)** | Portable C99 SDK, examples, porting guide and the developer SDK package |
| **[mcl-wire](https://github.com/machine-contact-layer/mcl-wire)** | Canonical binary encoding and deterministic decoding |
| **[mcl-link](https://github.com/machine-contact-layer/mcl-link)** | Machine contact lifecycle, framing, sessions and transport migration |
| **[mcl-ip](https://github.com/machine-contact-layer/mcl-ip)** | IP transport binding — MCL over UDP |
| **[mcl-ble](https://github.com/machine-contact-layer/mcl-ble)** | Bluetooth Low Energy transport binding — GATT carriage and role derivation |
| **[mcl-ap](https://github.com/machine-contact-layer/mcl-ap)** | Acoustic transport binding — first contact through a speaker and microphone |
| **[mcl-uwb](https://github.com/machine-contact-layer/mcl-uwb)** | Experimental Ultra-Wideband transport binding |

## Transports and maturity

| Transport | Profile | Maturity |
|---|---|---|
| IP (UDP) | IP-DATAGRAM profile 1 | Stable |
| Bluetooth Low Energy | BLE-GATT profile 1 · BLE-ACTIVATE-1 | Stable · Candidate |
| Acoustic | AP-BOOTSTRAP-1 | Candidate |
| Ultra-Wideband | binding draft | Research Draft |

`MCL Base 1` — machines that already share a bearer — is the Stable floor.
`MCL Stranger-Contact 1` adds zero-prior rendezvous and is Candidate. The IP,
BLE and acoustic bindings have run over the air between laptops, ESP32-S3
boards and Android handsets, with raw records kept in each repository's
evidence directories.

## Security

MCL v1.0 provides no confidentiality, no peer authentication and no replay
protection; a completed contact establishes reachability, not identity. MCL is
cryptography-agnostic: run it inside something that authenticates — DTLS, LE
Secure Connections, a controlled network — or hand off to a protocol that does.
[`SECURITY.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/SECURITY.md)
covers each property and how to report a vulnerability.

## Contribute

Found a defect or a specification error? See
[`REPORTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/REPORTING.md).
Changes follow
[`CONTRIBUTING.md`](https://github.com/machine-contact-layer/mcl-core/blob/main/CONTRIBUTING.md).
Everything is Apache-2.0.

## Contact

**[ojobit.com](https://ojobit.com)** · [info@ojobit.com](mailto:info@ojobit.com)

[X](https://x.com/0J0BIT) ·
[LinkedIn](https://www.linkedin.com/company/ojobit) ·
[GitHub](https://github.com/0j0bit) ·
[Hugging Face](https://huggingface.co/0J0BIT)
