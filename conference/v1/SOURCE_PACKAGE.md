# Sanitized source package

Prepared public source archive:

`PQC_IoT_SENTINEL_V1_PUBLIC_SOURCE.zip`

SHA-256:

`3335e0706a920db0a282023b07e0db95b464c8d979ad793b0f4953fad693e272`

## Contents

The prepared archive contains the updated PQC-IoT Sentinel source project, including:

- BL602 sender and receiver firmware;
- shared protocol/state helpers;
- dashboard frontend/backend;
- Splunk integration and governance tooling;
- DTLS baseline source;
- Raspberry Pi network-emulation helpers;
- host provisioning/capture tools;
- validation and analysis scripts;
- project analysis, protocol, measurement, and run documentation.

## Publication sanitization

The public package deliberately removes or replaces:

- real Wi-Fi credentials;
- Splunk passwords and HEC tokens;
- provisioned per-device authentication secrets;
- local private configuration;
- the laboratory DTLS server private key.

The DTLS credential headers are replaced by a public placeholder that requires the reproducer to generate fresh local credentials. This avoids publishing reusable private-key material.

## Historical provenance limitation

The source snapshot supports inspection of the implemented design and reproducible host-side analysis, but the Version 1 historical archive does not provide a complete source/SDK/compiler/configuration-to-flashed-binary lock for every campaign. The manuscript therefore distinguishes source-level behavior, recorded runtime evidence, and binary characteristics rather than claiming exact historical binary reconstruction.

## Distribution

The live evidence portal is:

https://pqcsecrity.live/evidence

The repository branch records the source-package checksum so copies obtained through the project evidence channel can be verified against the artifact identity used for Conference Version 1.
