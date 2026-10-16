# Version 1 reproducibility guide

## Scope

This guide describes how to inspect the public source snapshot and reproduce the analysis workflow associated with **Beyond the Handshake: A 24-Hour Study of Post-Quantum Messaging and DTLS on BL602**.

The paper is a reanalysis of archived campaigns. No fresh hardware run is implied by this package.

## Integrity checks

Use `conference/v1/SHA256SUMS.txt` to verify the prepared conference PDF and sanitized source package.

## Source package

The prepared public source package is `PQC_IoT_SENTINEL_V1_PUBLIC_SOURCE.zip`.

After unpacking, read in this order:

1. `README.md`
2. `PROJECT_ANALYSIS.md`
3. `RUN_STEPS.md`
4. `docs/PROTOCOL.md`
5. `experiments/dtls_baseline/README.md`
6. `pi1_network_emulator/README.md`
7. validation and analysis scripts referenced by those documents

## Sanitization

The public package intentionally excludes live credentials and the DTLS development server private key. Example `.env` files contain placeholders only. Generate fresh local development credentials before building the DTLS baseline.

## Historical evidence boundary

The manuscript reports results reconstructed from author-supplied experiment archives. The public source snapshot does not by itself prove that every archived firmware image was built from exactly this source revision with identical compiler/configuration inputs. This is a known Version 1 limitation and must remain visible when reproducing or extending the work.

## Recommended reproduction levels

### Level A — paper/artifact integrity

Verify checksums and inspect the manuscript, source, protocol definitions, and analysis scripts.

### Level B — host-side software checks

Create an isolated Python environment and run the host validation/tests documented in the source snapshot. Do not interpret synthetic fixtures as hardware measurements.

### Level C — short hardware reproduction

Using your own BL602 boards and locally generated credentials, rebuild both endpoints, provision a receiver pin/device credentials, and run a short baseline capture. Record the exact source commit, SDK/toolchain version, build flags, configuration, firmware hashes, and board role mapping.

### Level D — independent experiment replication

For a new scientific campaign, use independently restarted runs, frozen source-to-binary provenance, one terminal record per application cycle, full-cycle timing, and a priori stopping rules. Do not merge new results into Version 1 evidence.

## Live evidence portal

Project evidence website: https://pqcsecrity.live/evidence

The website is a dissemination layer. Exact paper reproduction should use the archived records and analysis scripts rather than treating dashboard counters or demonstration streams as primary experimental data.
