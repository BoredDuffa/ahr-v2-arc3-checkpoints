# AHR v2 research checkpoints

Public recovery checkpoints for the AHR v2 research project. These artifacts preserve experiments and their failure cases; they are not a validated ARC-AGI model or a standalone inference package.

**Diagnostic archive verified on 19 October 2026.** All four payloads (5,302,800,472 bytes in total), their metadata and the public restore receipt passed full anonymous download/SHA-256 verification. See the [diagnostic release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/diagnostic-archive-20261019).

## Diagnostic archive contents

| Experiment | Snapshot steps | Purpose |
|---|---:|---|
| Grounded-policy repair | 1, 401, 600 | Preserve a preliminary repair attempt that did not establish improved action behavior |
| Original synthetic learning probe | 6,097 | Preserve an early diagnostic snapshot from synthetic puzzle training |

The original backbone contains **329,334,183 parameters**. The repair adds a **131,845-parameter readout**, for **329,466,028 parameters** in total. These counts do not imply that every architectural component participated in every training objective.

These four snapshots are **not checkpoints from the longer human-playthrough training run**. No results from that longer run are available here.

## Human step-200 parent checkpoint

**Published and verified on 19 October 2026:** [human step-200 release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/human-parent-20261019). The 1,325,141,985-byte checkpoint has SHA-256 `d9cef168b82d3c06e340af1177a471481a7a23da0f29844a808e106144fbc262`; its full public download, five metadata files and public restore receipt were verified. The local payload remains preserved.

This release contains one pinned terminal step-200 human-imitation checkpoint and five metadata files. It preserves the local checkpoint. Its manifest also references an earlier checkpoint that is not included in this single-parent release. Use the distinct `PUBLISHED_HUMAN_PARENT_TO_GITHUB` receipt and verify every downloaded file.

## Preliminary human-playthrough check

A separate 200-update, single-frame imitation check used public human replay data. On its 512-row development sample:

| Measurement | Before | After | Comparison |
|---|---:|---:|---|
| Human action agreement | 42.58% | 40.04% | Train-fitted masked global action prior: 48.05% |
| Mean click distance | 40.26 px | 20.20 px | Human ACTION6 targets on a 64 × 64 grid |
| Exact click coordinates | 0/207 | 0/207 | Both coordinates must match |

Click distance improved, while action agreement declined and remained below the simple baseline. This is preliminary development evidence, not an ARC score, game-solving result, or proof of general reasoning.

## Recovery and use

The payloads are PyTorch recovery dictionaries containing training state, not Transformers-format models. Restoring an experiment requires its matching notebooks, configuration, runtime and data identities; those executable notebooks are not published in this repository. Do not assume that loading a state dictionary alone reproduces the experiment.

For the diagnostic archive, use the `ARCHIVED_TO_GITHUB` restore receipt to map each asset to its original checkpoint path and expected SHA-256 hash. Verify downloaded bytes before restoration. Release assets can be replaced, so the recorded hash identifies the snapshot more precisely than its release tag. PyTorch recovery files can contain pickle data: load only files whose provenance you trust.

Human replay data remain upstream and are not republished here. See the [human replay dataset](https://huggingface.co/datasets/magic-sword/arc_agi_3_public_demo_human_testing), [Hugging Face project metadata](https://huggingface.co/CafeClope/ahr-v2-arc3-research), and the [checkpoint repository](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints).
