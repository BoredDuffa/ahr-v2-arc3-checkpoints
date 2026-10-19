# AHR v2 research checkpoints

Public recovery checkpoints for the AHR v2 research project. These artifacts preserve experiments and their failure cases; they are not a validated ARC-AGI model or a standalone inference package.

**Diagnostic archive verified on 19 October 2026.** All four payloads (5,302,800,472 bytes in total), their metadata and the public restore receipt passed full anonymous download/SHA-256 verification. See the [diagnostic release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/diagnostic-archive-20261019).

## Diagnostic archive contents

| Experiment | Snapshot steps | Purpose |
|---|---:|---|
| Grounded-policy repair | 1, 401, 600 | Preserve a preliminary repair attempt that did not establish improved action behavior |
| Original synthetic learning probe | 6,097 | Preserve an early diagnostic snapshot from synthetic puzzle training |

The original backbone contains **329,334,183 parameters**. The repair adds a **131,845-parameter readout**, for **329,466,028 parameters** in total. These counts do not imply that every architectural component participated in every training objective.

These four snapshots are historical diagnostics. The completed human-playthrough continuation is published in its own release below.

## Human step-200 parent checkpoint

**Published and verified on 19 October 2026:** [human step-200 release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/human-parent-20261019). The 1,325,141,985-byte checkpoint has SHA-256 `d9cef168b82d3c06e340af1177a471481a7a23da0f29844a808e106144fbc262`; its full public download, five metadata files and public restore receipt were verified. The local payload remains preserved.

This release contains one pinned terminal step-200 human-imitation checkpoint and five metadata files. It preserves the local checkpoint. Its manifest also references an earlier checkpoint that is not included in this single-parent release. Use the distinct `PUBLISHED_HUMAN_PARENT_TO_GITHUB` receipt and verify every downloaded file.

## Completed human-playthrough continuation

The [longer human-imitation release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/human-long-20261019) preserves final step **10,966** and the best checkpoint by the declared development joint NLL, which remains initial step **200**. It includes the completed machine-readable learning report and terminal checkpoint verification, plus a public restore receipt. Final/best payloads also remain on the training server.

The continuation completed **10,766 additional optimizer updates in 50 minutes 53 seconds**, within its registered one-hour lease on a shared A100. All nine exact checkpoint-recovery smoke checks passed first. It used all 74,122 eligible training examples from 21 game families. The fixed development cohort has 4,096 examples, 1,024 per held-out family, and includes all **44 eligible recordings out of 48 raw recordings**; four raw recordings have no eligible labels. These development families have been reused and are not an untouched test set.

| Metric | Initial step 200 | Final step 10,966 | Train-only comparison |
|---|---:|---:|---|
| Human action agreement | 36.28% | 37.87% | Mask-conditioned action prior: 47.68% |
| Agreement with multiple legal actions | 15.04% | 17.15% | Mask-conditioned action prior: 30.24% |
| Mean click distance, lower is better | 21.95 px | 25.36 px | Global mean coordinate: 23.32 px |
| Joint action/click NLL, lower is better | 4.5785 | 5.7308 | Global action prior × uniform coordinates: 4.4622 |

Final exact click coordinates: **0/1,604**. A paired recording bootstrap supports a small action-imitation improvement on these fixed families, but the final model is 9.81 percentage points below the mask-conditioned action baseline (exploratory 95% interval: 8.10–11.76 points below). Click error and joint likelihood worsened. A pixel-shuffle control changed 4,093/4,096 grids and provided no reliable evidence of useful state-specific pixel dependence. **This run did not beat the baseline or establish grounded reasoning.** No ARC competition score or game completion was measured.

The full human-imitation architecture retains **329,334,183 parameters**; 211,749,274 receive gradients through the current-frame encoder and Queen/Worker/Scout policy paths. Spatial features are mean-pooled, click x/y heads are independent, and the current latent is supplied in nominal history/memory slots. World prediction, energy-based refinement, Lorentz geometry and planning are inactive. These results test that imitation path, not those proposed reasoning mechanisms. Causes of the observed failure require controlled ablations.

## Earlier 200-update human-playthrough check

A separate earlier 200-update, single-frame imitation check used public human replay data. Its 512-row development sample differs from the continuation cohort above, so the two sets of figures should not be mixed:

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
