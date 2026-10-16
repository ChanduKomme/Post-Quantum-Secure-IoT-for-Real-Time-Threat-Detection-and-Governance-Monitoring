# Reviewer quick guide

## 5-minute path

1. Read the root `README.md` for the study framing and headline results.
2. Read `PAPER.md` for the abstract, research questions, contributions, and limitations.
3. Inspect `PRIMARY_RESULTS.csv` and `NETWORK_RESULTS.csv` for machine-readable headline values.
4. Read `ARTIFACT_SCOPE.md` before interpreting PQC-vs-DTLS differences.
5. Read `REPRODUCIBILITY.md` for evidence and replication boundaries.
6. Use the live evidence portal for project presentation and catalogue navigation: https://pqcsecrity.live/evidence

## Central result

The paper's central measurement lesson is that successful-message latency, service continuity, session establishment, complete-cycle delivery, and telemetry completeness are different observables and should not be collapsed into one headline metric.

The 24-hour DTLS run has a 10 ms median established-session RTT yet a 159.184 s maximum observed inter-delivery gap during failed session establishment. The PQC endurance run records 32,790 sender-confirmed deliveries with one missing parsed receiver acceptance. In later PQC loss experiments, structured terminal counters omit some metadata-fetch failures, reducing completed-cycle delivery to 98.71% at 20% targeted loss and 65.63% at 50% targeted loss.

## Interpretation guardrails

- Do not interpret the successful RTT ratio as a primitive-level KEM-versus-ECDHE slowdown.
- Do not treat the two profiles as having identical authentication, persistence, or key-lifecycle contracts.
- Do not treat message samples within one 24-hour run as independent campaign replications.
- Do not interpret matching Kyber-derived parameter sizes or successful round trips as FIPS 203 conformance.
- Do not interpret dashboard/Splunk event totals as application-delivery denominators without verifying event completeness.

## Version 1 status

This is an evidence-bounded conference artifact. The next experimental version is expected to improve source-to-binary provenance, cycle-level instrumentation, independent run replication, and matched-security baseline design without rewriting Version 1 results.
