# Artifact scope and claim boundaries

## Included claims

Version 1 supports an implementation-level systems study of two BL602 security profiles and a secondary PQC network-resilience study. It supports statements about the recorded application behavior, measured timing boundaries, packet-capture observations, persistence ordering in inspected source, and telemetry/accounting discrepancies described in the paper.

## Not claimed

This artifact does not establish:

- FIPS 203 / ML-KEM conformance;
- cryptographic-module certification;
- a formal security proof of the composed custom protocol;
- side-channel resistance;
- target entropy quality;
- fault resistance;
- secure boot or hardware anti-rollback guarantees;
- exactly-once physical actuation;
- fleet-scale behavior;
- energy efficiency;
- universal PQC-vs-DTLS performance superiority.

## Comparison boundary

The PQC and DTLS profiles perform different work. Authentication, persistence, key reuse, acknowledgement semantics, and timing endpoints differ. Results characterize the complete recorded implementations; they do not isolate the causal cost of replacing ECDHE with a post-quantum KEM.

## Measurement boundary

Successful-message RTT is not the same as complete application-cycle latency. Setup/recovery errors, inter-delivery gaps, and telemetry completeness are reported separately. Thousands of message samples from one 24-hour campaign are not treated as thousands of independent experimental replications.

## Sanitization

The public source package excludes real local credentials, provisioned per-device authentication keys, Splunk tokens/passwords, and DTLS private-key material. Placeholders are supplied where necessary for readers to understand the build/configuration path.

## Versioning

Future matched-security baselines, conformance work, repeated 24-hour campaigns, energy measurements, or redesigned instrumentation should be released as Version 2 or a later artifact rather than rewriting Version 1 evidence.
