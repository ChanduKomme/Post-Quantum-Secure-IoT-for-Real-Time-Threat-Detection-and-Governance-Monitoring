# Beyond the Handshake — PQC-IoT Sentinel Conference Version 1

[![Status](https://img.shields.io/badge/status-conference%20v1-blue)](#artifact-status)
[![Platform](https://img.shields.io/badge/platform-BL602%20%2F%20RISC--V-informational)](#system)
[![Transport](https://img.shields.io/badge/transport-CoAP%20%2F%20UDP-lightgrey)](#system)
[![PQC](https://img.shields.io/badge/PQC-Kyber--derived%20512--parameter-orange)](#cryptographic-scope)
[![Classical baseline](https://img.shields.io/badge/baseline-DTLS%201.2-green)](#dtls-baseline)
[![Evidence](https://img.shields.io/badge/evidence-24h%20%2B%20network%20resilience-purple)](#headline-results)

## Conference manuscript

**Beyond the Handshake: A 24-Hour Study of Post-Quantum Messaging and DTLS on BL602**

This branch is the public **Version 1 conference artifact** for the PQC-IoT Sentinel research project. It organizes the conference study, reproducibility notes, artifact scope, checksums, source-package information, and the live evidence website.

> **Live research website:** https://pqcsecrity.live/evidence
>
> The live website is a presentation/evidence portal. The paper's quantitative claims are grounded in archived experiment records and the reconstruction described in the manuscript, not in animated/live dashboard counters alone.

## Paper at a glance

The study compares two separate 24-hour BL602 campaigns:

- **PQC-IoT Sentinel:** application-layer protected CoAP messaging using a Kyber-derived 512-parameter KEM, HKDF-SHA-256, AES-256-CCM, a provisioned device HMAC, persistent freshness state, and request-bound authenticated acknowledgements.
- **Classical baseline:** DTLS 1.2 using ECDHE P-256, ECDSA P-256 server authentication, and AES-256-CCM with session reuse.

The systems intentionally have different authentication, persistence, key-lifecycle, and timing semantics. The comparison is therefore an **implementation-level systems study**, not a primitive-only KEM-versus-ECDHE benchmark.

## Headline results

| Metric | PQC-IoT Sentinel | DTLS 1.2 baseline |
|---|---:|---:|
| Host capture duration | 86,400.172 s | 86,400.820 s |
| Successful sender messages | 32,790 | 42,346 |
| Failed sender message outcomes | 0 | 2 |
| Observed message success | 100.0000% | 99.9953% |
| Parsed/recorded receiver successes | 32,789 | 42,346 |
| Successful RTT median / P95 | 152 / 503 ms | 10 / 18 ms |
| Successful RTT P99 / maximum | 566 / 6,810 ms | 29.55 / 2,458 ms |
| Longest observed inter-delivery gap | 15.747 s | 159.184 s |
| Successful handshakes | N/A | 143 sender / 143 receiver |
| Raw handshake-call errors | N/A | 29 sender / 2 receiver |

A low steady-state RTT does not guarantee uninterrupted delivery. Raw-log reconstruction found DTLS establishment errors that were absent from structured failure counters, while the PQC run retained one missing parsed receiver-acceptance event. The work therefore reports message outcomes, setup/recovery, continuity, and telemetry completeness separately.

## Secondary network-resilience study

Later PQC runs evaluated ordinary forwarding, +200 ms forward delay, 10% broad random loss, and targeted 20% / 50% receiver-bound loss.

| Profile | Structured delivery | Completed-cycle delivery | RTT median | RTT P95 |
|---|---:|---:|---:|---:|
| Network baseline | 100.0% | 100.00% | 130.0 ms | 548.00 ms |
| +200 ms delay | 100.0% | 100.00% | 337.0 ms | 748.00 ms |
| 10% random loss | 100.0% | 100.00% | 129.5 ms | 6,535.35 ms |
| 20% targeted loss | 99.1% | 98.71% | 132.0 ms | 6,912.00 ms |
| 50% targeted loss | 73.9% | 65.63% | 546.0 ms | 13,300.40 ms |

The raw-cycle audit found metadata-fetch failures that were absent from structured terminal telemetry. At 50% loss, public-key and metadata acquisition accounted for 288 of 387 failed completed cycles. Packet-capture checks observed forward missing fractions of approximately 9.55%, 19.95%, and 50.54% for the loss profiles.

## System

The evaluated platform uses BL602/PineCone-compatible RISC-V nodes running application firmware over FreeRTOS/lwIP. The PQC workflow uses:

1. receiver public-key retrieval and SHA-256 fingerprint pinning;
2. metadata retrieval and cross-checking;
3. fresh KEM encapsulation per send cycle;
4. HKDF-SHA-256 key derivation;
5. AES-256-CCM payload protection;
6. a separate provisioned device HMAC over the protected request;
7. persistent sender sequence and receiver freshness state;
8. persistence-before-ACK receiver semantics;
9. request-bound authenticated positive acknowledgements;
10. raw serial + structured event collection for independent analysis.

For the recorded 22-byte demonstration message, the protected application payload is 874 bytes. A minimal `/pqkem-data` CoAP wrapper produces an 890-byte UDP payload before IP/link-layer overhead.

## DTLS baseline

The classical baseline uses DTLS 1.2 with ECDHE P-256, ECDSA P-256 server authentication, and AES-256-CCM. Sessions request 300 messages and reuse the established channel. Development certificate fixtures are used for the laboratory baseline; private key material is not part of the public conference artifact.

The DTLS profile does **not** implement the same application credential, durable acceptance rule, or key lifecycle as the PQC profile. The paper keeps these differences explicit and does not interpret the observed latency ratio as the causal cost of post-quantum cryptography.

## Cryptographic scope

The bundled post-quantum core is described conservatively as **Kyber-derived, 512-parameter** code. The project has matching parameter sizes and successful round-trip behavior, but this Version 1 artifact does **not** claim:

- FIPS 203 / ML-KEM conformance;
- a FIPS-validated cryptographic module;
- a formal proof of the composed custom protocol;
- receiver-key forward secrecy after later compromise of the long-lived decapsulation key;
- side-channel, fault-injection, entropy-quality, or physical-tamper resistance.

These limits are intentional and part of the paper's evidence-bounded interpretation.

## Conference artifact

See [`conference/v1/README.md`](conference/v1/README.md) for the frozen Version 1 artifact index, [`conference/v1/REPRODUCIBILITY.md`](conference/v1/REPRODUCIBILITY.md) for reproduction guidance, and [`conference/v1/ARTIFACT_SCOPE.md`](conference/v1/ARTIFACT_SCOPE.md) for claim boundaries.

The prepared sanitized source snapshot is identified by SHA-256 in the artifact manifest. Real Wi-Fi credentials, Splunk tokens/passwords, provisioned per-device secrets, and the DTLS development server private key are excluded from the public package.

## Artifact status

This branch is a frozen **conference Version 1** snapshot. It should not be silently rewritten to incorporate future matched-baseline or repeated-campaign results. Later experiments should be published as a new version/branch so that the evidence underlying this manuscript remains identifiable.

## Citation

If you use this artifact, cite the conference manuscript:

> *Beyond the Handshake: A 24-Hour Study of Post-Quantum Messaging and DTLS on BL602*, 2026, conference manuscript / Version 1 artifact.

Author metadata should be restored according to the target venue's double-blind or camera-ready policy.

## Responsible use

This repository is a controlled research testbed. Do not deploy development credentials or experimental configurations as production security. Review third-party notices in the included source before redistribution.
