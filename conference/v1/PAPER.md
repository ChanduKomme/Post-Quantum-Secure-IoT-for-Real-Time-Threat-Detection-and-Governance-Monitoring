# Beyond the Handshake: A 24-Hour Study of Post-Quantum Messaging and DTLS on BL602

## Version

Conference Version 1, 2026.

## Abstract

Embedded post-quantum benchmarks usually expose computation and handshake costs; sustained applications also depend on key reuse, durable acceptance, and recovery. This study examines those costs through two separate 24-hour BL602 campaigns: PQC-IoT Sentinel, an application-layer Kyber-derived messaging system, and a classical DTLS 1.2 baseline. Sentinel combines fresh per-message encapsulation with device authentication and persistence before acknowledgement. It records 32,790 successful sender deliveries with no observed terminal failures and one missing parsed receiver event. DTLS records 42,346 successes from 42,348 message attempts. Successful-message RTT median/P95 is 152/503 ms for Sentinel and 10/18 ms for DTLS, while the longest observed intervals between successful deliveries are 15.75 and 159.18 s. Raw-log reconstruction identifies 29 sender and two receiver handshake errors omitted from structured DTLS failure totals; 143 successful handshakes per role remain verified. The sender's successful handshake intervals sum to 6.51 ms per delivered DTLS message under the observed reuse policy. Archived PQC images are about one-third smaller, while their static BSS allocation is larger. The contribution is a sustained implementation comparison that separates message outcomes, session establishment, temporal variation, and evidence completeness. A secondary PQC delay/loss study examines recovery beyond baseline conditions. Differing authentication, persistence, timing, and key lifecycles preclude attributing the observed gap to cryptography alone.

## Research questions

1. **RQ1 — Delivery continuity and recovery:** What delivery continuity and recovery are observed throughout each 24-hour campaign?
2. **RQ2 — Latency and lifecycle:** How do successful-message latency, within-run variation, and key-establishment policy interact?
3. **RQ3 — Resources and comparability:** What footprint and runtime evidence support deployment on BL602, and what remains incomparable?

## Contributions

- An explicit account of both profiles' acceptance and timing boundaries.
- Raw reconstruction of message, session, and temporal outcomes, including omitted handshake failures and successful-setup amortisation.
- Resource analysis tied to identifiable archived files and reproducible analysis scripts.
- Secondary robustness evidence from controlled PQC delay/loss campaigns.

## Primary 24-hour results

| Metric | PQC baseline | DTLS baseline |
|---|---:|---:|
| Host capture duration (s) | 86,400.172 | 86,400.820 |
| Successful / failed sender messages | 32,790 / 0 | 42,346 / 2 |
| Observed message success | 100.0000% | 99.9953% |
| Parsed/recorded receiver successes | 32,789 | 42,346 |
| Successful messages per capture hour | 1,366.25 | 1,764.40 |
| Successful RTT mean (ms) | 213.830 | 11.979 |
| Successful RTT median / P95 (ms) | 152 / 503 | 10 / 18 |
| Successful RTT P99 / maximum (ms) | 566 / 6,810 | 29.55 / 2,458 |
| Longest observed inter-delivery gap (s) | 15.747 | 159.184 |
| Hourly median RTT range (ms) | 105–170 | 9–11 |
| Successful handshakes, sender / receiver | N/A | 143 / 143 |
| Raw handshake-call errors, sender / receiver | N/A | 29 / 2 |

## Key interpretation

The established DTLS exchange is faster in this configuration, but the ratio between successful-message RTTs is **not** a measured KEM-versus-ECDHE penalty. Sender encapsulation occurs outside the PQC RTT timer, DTLS handshake establishment occurs outside steady-state message RTT, and the two profiles have different authentication, persistence, acknowledgement, and key-reuse semantics.

The endurance analysis also shows why successful-message latency and service continuity are different metrics. DTLS maintains a low typical established-session RTT while exhibiting a much longer recovery interruption during failed session establishment. PQC shows a higher steady-state application RTT but a smaller maximum observed inter-delivery gap in these separate campaigns. Because the runs were recorded on different dates and were not matched fault trials, no intrinsic recovery superiority is claimed.

## Secondary PQC network study

| Profile | Delivered | Structured delivery | Completed cycles | Cycle delivery | RTT median (ms) | RTT P95 (ms) |
|---|---:|---:|---:|---:|---:|---:|
| Network baseline | 1,000 | 100.0% | 1,000 | 100.00% | 130.0 | 548.00 |
| 200-ms delay | 1,000 | 100.0% | 1,000 | 100.00% | 337.0 | 748.00 |
| 10% random loss | 1,000 | 100.0% | 1,000 | 100.00% | 129.5 | 6,535.35 |
| 20% targeted loss | 991 | 99.1% | 1,004 | 98.71% | 132.0 | 6,912.00 |
| 50% targeted loss | 739 | 73.9% | 1,126 | 65.63% | 546.0 | 13,300.40 |

The raw-cycle reconstruction found four and 126 metadata-fetch failures omitted from structured terminal telemetry at 20% and 50% loss, respectively. At 50% loss, key/metadata acquisition accounted for 288 of 387 failed completed cycles. This is both an availability finding and an instrumentation finding.

## Resource observations

Archived PQC sender/receiver binaries are 398,384 / 401,872 bytes; corresponding DTLS files are 591,064 / 602,236 bytes. Static BSS moves in the opposite direction: 103,652 / 107,324 bytes for PQC versus 94,102 bytes for each DTLS role. These are complete application-build characteristics, not isolated cryptographic primitive footprints.

The PQC receiver has full-day runtime heap/stack observations. DTLS runtime-memory values come from a shorter separate characterization note, so the manuscript does not present them as equal-duration peak-memory measurements.

## Limitations

Version 1 deliberately leaves the following open:

- FIPS 203 / ML-KEM conformance of the Kyber-derived implementation;
- a matched-security classical/PQC protocol experiment;
- repeated independent 24-hour campaigns;
- fully locked historical source-to-flashed-binary provenance;
- energy and flash-lifetime measurements;
- arbitrary power-cut persistence testing;
- side-channel, fault, entropy-quality, and physical-identity validation;
- multi-device contention, mobility, and payload scaling.

## Live evidence portal

https://pqcsecrity.live/evidence

The portal is a companion presentation layer; exact quantitative reproduction should use the archived evidence and analysis workflow described by the artifact.
