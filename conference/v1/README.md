# Conference Version 1 artifact index

## Manuscript

**Beyond the Handshake: A 24-Hour Study of Post-Quantum Messaging and DTLS on BL602**

This directory defines the frozen public artifact for Conference Version 1 of PQC-IoT Sentinel.

## Live website

https://pqcsecrity.live/evidence

The website is a dissemination and evidence-catalogue layer. Quantitative paper results should be reproduced from the archived experimental records and analysis workflow rather than from live/demo counters alone.

## Included artifact records

- `REPRODUCIBILITY.md` — reproduction levels, integrity checks, and experimental-boundary guidance.
- `ARTIFACT_SCOPE.md` — supported claims, non-claims, and comparison limitations.
- `SHA256SUMS.txt` — SHA-256 identifiers for the Version 1 conference PDF and prepared sanitized source package.
- `SOURCE_PACKAGE.md` — sanitization notes and source-package identity.
- `PAPER.md` — manuscript metadata, abstract, core research questions, and headline findings.

## Prepared binary artifacts

The Version 1 artifacts prepared for this branch are:

- `Beyond_the_Handshake_Conference_Paper.pdf`
  - SHA-256: `9b6b7862cacc96f0b14a8b6789b6c08d5eebcf1344fd9680ce2b195cc35ccaf9`
- `PQC_IoT_SENTINEL_V1_PUBLIC_SOURCE.zip`
  - SHA-256: `3335e0706a920db0a282023b07e0db95b464c8d979ad793b0f4953fad693e272`

The public source package is sanitized: real local credentials, provisioned device secrets, and the DTLS development server private key are excluded.

## Versioning rule

Do not silently replace Version 1 evidence with future experiments. Matched-security baselines, repeated 24-hour campaigns, conformance testing, power-cut persistence experiments, energy measurements, or redesigned cycle instrumentation should be released as Version 2 or later.
