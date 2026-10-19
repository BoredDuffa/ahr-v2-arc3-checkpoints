# AHR v2 research checkpoints

<!-- AHR_ACTION_DELTA_RESULTS_BEGIN -->
## Action balancing and corrected world gradients: no baseline win (19 October 2026)

The complete **329,350,583-parameter AHR v2** remains intact: Queen transformer, Worker and Scout EBMs, literal Lorentz geometry, observed memory, learned spatial world model and bounded two-step planning. Informative actions are sampled uniformly, with one forced action per eight examples. Conditional coordinate supervision is separated from branch action weights; world heads use different successor bootstraps and changed-cell supervision.

A first action-balanced trial completed **3,446 updates / 55,136 sampled examples**. Its calibrated policy recovered **34/68** optional clicks, but its raw policy recovered **0/68**. It also exposed a concrete implementation error: subtracting a detached current state from a forecast containing that same identity base created an unwanted encoder gradient. The corrected loss differentiates both terms. Identity-limit and nonzero-residual finite-difference tests verify the correction; initial forward predictions remain bitwise identical.

The corrected trial completed **2,516 updates / 40,256 sampled examples in 26.64 minutes**, including **1,812** joint updates. All three actual stage recovery gates passed. It used the same parent, seed, data, sampler and learning rates, with a separately registered shorter allowance. This makes terminal cross-trial comparisons descriptive; matched TRAIN updates are an additional mechanism diagnostic.

| Same 512 development observations | Action agreement | Joint NLL, lower is better | Mean click distance |
|---|---:|---:|---:|
| TRAIN-fitted baseline | 43.75% | 4.4300 |23.19px|
| Parent 4,385 |35.16%|4.9727|23.67px|
| First action-balanced 3,446 |40.43%|4.9127|22.93px|
| Corrected terminal 2,516 |35.74%|4.9493|23.26px|
| Preregistered TRAIN-selected 704 |36.52%|4.9797|23.61px|

Baseline cells use metric-specific references: mask-table action probabilities with uniform legal coordinate density for joint NLL, and the TRAIN-fitted coordinate median for click distance. They are not one predictor yielding every cell.

**Neither corrected endpoint beats the unchanged baseline criterion.** Optional clicks remain **0/68**, raw and calibrated. The terminal raw joint NLL worsens from 5.0000 to 5.1244; TRAIN-fitted calibration lowers it to 4.9493. Loss reduction after calibration does not demonstrate that the raw policy learned useful click decisions.

Grounding is more stable: corrected world forecast MSE is **0.08603**, versus 0.21326 in the first action-balanced trial and 0.08911 at initialization. Encoder alignment is 0.06875, versus 0.19342 and 0.07334 respectively. At matched TRAIN update 2,204, world MSE is 0.08472 versus 0.12296. However, the corrected terminal forecast still loses to neural-current persistence **0.08382** and fixed-descriptor persistence **0.02211**. Useful action-dependent dynamics beyond persistence are not established. Distinct world heads alone do not prove calibrated epistemic uncertainty.

[Corrected final/best weights and benchmark/restore metadata](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/delta-gradient-20261019) · [First diagnostic trial](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/action-balanced-20261019).

**Checkpoint preservation verified:** both corrected final/best payloads total **2,653,937,277 bytes**. All 22 payload/metadata assets and the separate [restore receipt](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/download/delta-gradient-20261019/archive_receipts__PUBLISHED_TO_GITHUB.json) passed complete anonymous byte-count/SHA256 verification at **2026-10-19T22:33:44.406082+00:00**. Latest two resumable checkpoints plus best remain on the training server. The temporary upload credential has been removed. GitHub releases remain mutable; verify full hashes on restore.

These are **offline human-playthrough imitation and one-step descriptor diagnostics**, using the same 512 observations from 44 recordings in four reused development families. This is not an ARC-AGI-3 gameplay score, game-completion result or new-game generalization test. The TRAIN-family selector has only four optional-click labels; ancestors were exposed to its families. One seed, reused development data and recording-bootstrap intervals conditional on these families limit conclusions. Inference controls establish component activity, not a causal architecture advantage.

<!-- AHR_ACTION_DELTA_RESULTS_END -->

## Spatial world repair: no baseline win (19 October 2026)

The separate repair keeps the entire **329,334,183-parameter core**, adds a learned **16,400-parameter spatial readout**, and retains the Queen, both EBMs, literal Lorentz event geometry, observed memory and bounded two-step planning: **329,350,583 parameters total**. It corrects the previous input/target coordinate mismatch using grounded neural spatial states, identity-initialized simplex residual forecasts, an existing-head spatial click pointer and train-only calibrated outcome/availability/error heads. The observed semantic context remains fixed during imagination.

All three actual stage-boundary exact-recovery gates passed, including full policy-only component gradients, inference effects and teacher-target isolation. The run completed **4,385 updates / 70,160 examples in 46 minutes 30 seconds**, including **3,617 full joint updates / 57,872 examples**, within the original one-hour allowance. No historical weights were deleted. GPU0 was shared; the other experiments were untouched.

The fixed cohort is the **same 512 observations, 44 eligible recordings and four reused development families** as the full pilot below. Both old and repaired point errors now use floating conditional means, registered before this repair's outcomes. Exact joint NLL remains the proper two-dimensional branch-mixture likelihood.

| Fixed development measurement | Old full model | Repair initial | Repair final | Baseline |
|---|---:|---:|---:|---:|
| Human action agreement | 41.60% | 43.75% | **35.16%** | 43.75% |
| Agreement, 384 multi-legal observations | 22.14% | 25.00% | **13.54%** | 25.00% |
| Exact joint NLL, lower is better | 5.2245 | 4.4616 | **4.9727** | 4.4300 |
| Mean click distance, 196 clicks | 24.37 px | 24.24 px | **23.67 px** | 23.19 px |
| Common fixed-descriptor world MSE | 0.46159 | 0.75462 | **0.08911** | 0.02211 |

**The final model does not beat the combined baseline criterion.** Joint NLL improves over the old model by **0.2517 nats** (paired recording 95% interval **0.1959–0.3074**), but deteriorates against the repaired initialization by **0.5111 nats** (**0.3879–0.6185**). Action agreement is **8.59 percentage points below** the mask baseline (**5.66–11.70 pp below**). The comparison algorithms are a training-fitted mask action prior, its product with uniform coordinates, a training-fitted constant median click, and exact current-descriptor persistence. Exact clicks remain **0/196**. The historical 31.15-pixel result below used marginal modes; it is not the matched old mean-decoder result in this table.

Grounding improves substantially (old encoder alignment MSE **0.43259 → 0.07334**), but world prediction still loses to copying its own neural state (**0.08911 versus 0.08810**) and to raw-descriptor persistence (**0.02211**). In learned successor coordinates, forecast MSE is **0.016300**, versus persistence **0.016046**. Wrong-action alignment and state-shuffle intervals do not establish useful state-specific generalization. Planning now helps same-weight joint NLL by only **0.00382** (**0.00225–0.00548**), without changing action agreement. Removing EBM refinement improves NLL by **0.01545**; the Lorentz-versus-Euclidean interval crosses zero. These are inference interventions, not separately trained causal architecture comparisons.

The most concrete remaining shortcut is click-action suppression: on **68 target-click observations with other legal actions**, agreement falls from **68/68 initially to 0/68 finally**. The final policy selects action 2 on 28 and action 4 on 40 of these rows; the 128 forced-click rows remain correct. This is an exploratory post-run slice of the fixed cohort, not a new independent test.

The new repair excludes 21 complete TRAIN recordings (**7,289 rows**) from all new gradient phases, leaving **66,833 optimizer rows**. The inherited parent used the earlier full pool, so this is a current-run holdout rather than globally unseen data. Calibration and checkpoint selection use only these reserved TRAIN recordings; the unchanged benchmark priors retain all **74,122** original training rows. Fixed TRAIN-selection NLL improves **4.4533 → 3.9472**, while development NLL worsens **4.4616 → 4.9727**, indicating poor transfer/overfitting. The final checkpoint is also best by the registered TRAIN-selection metric; this does not turn the development failure into a win.

Three successor heads are retained, but equal initialization and their shared objective preserve symmetry. Independent ensemble diversity is unestablished; uncertainty is a learned conditional error scale with TRAIN-only calibration, not demonstrated epistemic or out-of-distribution uncertainty. One seed, correlated recordings, reused development families and uncorrected multiple comparisons limit inference. **No ARC gameplay, game completion, competition score, or new-game generalization is measured.**

**Public final/best storage verified:** the [world-repair release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/world-repair-20261019) contains one deduplicated final/best step-4,385 payload (**1,326,910,741 bytes**), 14 metadata files and a [public restore receipt](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/download/world-repair-20261019/archive_receipts__PUBLISHED_TO_GITHUB.json). Every complete anonymous payload/metadata download and the restore receipt passed byte-count/SHA256 checks at **2026-10-19T20:34:38.438244+00:00**. The checkpoint remains on the training server; the temporary upload credential was removed.


## Full AHR pilot: no baseline win (19 October 2026)

The new full-path run retained **329,334,183 parameters** and activated differentiable Worker/Scout EBM refinement, literal 1+3 Minkowski/Lorentz event calculations, observed two-frame memory and eight-root/two-step learned-world planning. All **17 exact-recovery and activation checks passed** before training. This is a new initialization: the world and geometry modules were freshly initialized, all LayerNorm affine parameters reset, and the verified parent encoder/Queen/Worker/Scout tensors outside LayerNorm preserved. Exact continuation applies within this new run.

It completed **5,500 updates / 22,000 examples in 47 minutes 1 second**, including smoke checks and evaluation, within the original one-hour allowance on shared GPU0. This is less than one pass through the 74,122-example pool. The frozen development cohort has **512 observations, 384 multi-legal rows and 196 click rows**, balanced across four reused families and covering all 44 eligible recordings. It differs from the historical 4,096-row cohort below.

| Fixed development metric | New-run initial | Final step 5,500 | Baseline |
|---|---:|---:|---:|
| Human action agreement | 38.67% | 41.60% | 43.75% |
| Agreement with multiple legal actions | 18.23% | 22.14% | 25.00% |
| Proper joint action/click NLL, lower is better | 12.9404 | 5.2245 | 4.4300 |
| Mean click distance, lower is better | 28.42 px | 31.15 px | 23.19 px |
| Fixed-descriptor world MSE, lower is better | 1.8328 | 0.4616 | 0.0221 |

The action baseline is a training-fitted legal-mask prior; joint NLL uses that prior with uniform coordinates; click distance uses a training-fitted constant median; world MSE uses the fixed current-frame descriptor as its successor prediction. Final exact clicks were **0/196**. The final action difference from the mask baseline is **-2.15 percentage points** (exploratory 95% interval **-5.46 to +0.98 pp**), so superiority is not established. The best checkpoint by development joint NLL is step **2,500**, also below the baseline criterion.

Real observations outperform shuffled observation bundles on multi-legal action agreement by **3.13 pp** (95% interval **+0.52 to +5.80 pp**), but not on joint NLL. This is limited evidence of useful observation dependence. Disabling planning slightly improves joint NLL by **0.0069 nats** (paired interval **0.0044 to 0.0093**); the Lorentz-versus-Euclidean difference includes zero. These are same-checkpoint inference controls, not separately trained architecture ablations. Intervals resample recordings within fixed reused families, with one training seed and no multiple-comparison correction.

World prediction and encoder anchoring improve from their new-run initial states, but final world MSE remains **20.9 times** the copy-current error (19.7 times on descriptor-changed rows). The coarse fixed auxiliary target is 16-colour occupancy in 8x8 spatial cells; it is not a direct policy input or full visual reconstruction. The planner uses approximate future transitions and unverified future masks. Computation stays at fixed depth two; persistent event DAG/pheromone memory and useful adaptive halting are not demonstrated. **No ARC gameplay, completion rate or competition score was measured.**

**Public final/best storage verified:** the [full-path release](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/tag/full-path-20261019) contains final step 5,500, best step 2,500, 11 selected metadata files and a [public restore receipt](https://github.com/BoredDuffa/ahr-v2-arc3-checkpoints/releases/download/full-path-20261019/archive_receipts__PUBLISHED_TO_GITHUB.json). Both payloads total **2,652,910,016 bytes**. Every complete anonymous payload download and the restore receipt passed byte-count/SHA256 checks. The weights also remain on the training server; the temporary upload credential was removed.

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
