# Skill benchmark

**Run date:** 2026-10-01 UTC. **Scope:** one OpenSpec implementation task, one trial per condition.

The no-test-skill control used the fewest tokens, lowest calculated API-equivalent cost, and least observed generation time. All three outputs passed the frozen acceptance suite. A deeper review found a shared pathological-input bug, stronger capacity performance in the Astra orchestration output, and no material overengineering. These are results for this task, not a general ranking of skills or models.

## 1. Test procedure

1. **Freeze the inputs.** Test this repository at [5abeb9b](https://github.com/starpia-forge/skills/tree/5abeb9bca887f7d8bdb2c9a4aae3fc64d0f6b05a), with Codex CLI `0.159.0-alpha.7` and OpenSpec `1.14.0`, on one cloud Linux computer. Use a Python standard-library reservation-ledger fixture with six baseline tests. Freeze the task, fixture, installed skills, and independent 32-case acceptance suite before any run.
2. **Give every root the same substantive task.** Implement atomic multi-resource reservations, half-open interval capacity accounting, canonical persistent idempotency, deterministic waitlist promotion on cancellation, no-op/error nonmutation, detached reads, atomic persistence, and compatible JSON CLI commands. Add regression tests and README documentation. Complete **explore → propose → apply → archive**. The exact task bytes were identical, with SHA-256 `0c8d2e9f45e75949b6529f01d0f392889dedb359020faadcffe34e6d32d2317e`.
3. **Fix the caller, vary skill selection.** Every root used `gpt-6-astra` with `medium` effort. The two skill arms received byte-identical project copies, both test skills, the same custom-agent definitions, the same common driver, and only a different explicit skill attachment. Preserve each selected skill's intended downstream models and responsibilities. Generic delegation limits were six threads and depth two, with fresh-context briefs.
4. **Add an isolated control.** Copy the same fixture but omit the two test-skill directories and their two custom-agent TOMLs: six files removed, 15 retained files unchanged. Keep the standard OpenSpec skills and common tools/settings. Remove the skill attachment, four custom-agent configuration overrides, and exactly three skill-selection/selected-role sentences from the driver. Keep all other driver text, including fresh-context delegation guidance. Runtime skill discovery confirmed neither test skill was available and no custom-agent mappings were inherited. The control could delegate normally but chose to use only its root.
5. **Run and account for the whole tree.** Run `luna-implement` and `astra-orchestration` in parallel; run the control later, alone. Start timing immediately before root `turn/start`; stop after the root and required descendants finish. Capture unique `rawResponse/completed` IDs and numeric usage, then join actual model, effort, role, and parent metadata before ephemeral threads close. Do not provide other arms' results or the external tests to any arm. Audit completed tool paths for unintended access. Exclude setup, preflights, and independent review from generation timing and token totals.
6. **Review the outputs independently.** After completion, the supervising reviewer directly reran acceptance and project tests, read the library/CLI and archived artifacts, and checked strict OpenSpec validation and an empty active-change list. Then perform oracle, fault-injection, edge-input, and performance probes without changing any implementation. Preserve the original results; no original trial was rerun when adding the control or recalculating costs.

Observed trees were Astra → two Luna workers for `luna-implement`; Astra → a named Sol manager → four named Luna workers for `astra-orchestration`; and one Astra root for the control. The archive workflow was completed in all cases. The control synced and verified the main specification before moving the change directory to the archive, which the installed archive skill permits; it did not invoke the archive CLI command. Its archive directory uses local date `2026-10-02`, while the run's UTC date is `2026-10-01`.

Whole-tree generation duration was **779.353 s (12m 59.35s)** for `luna-implement`, **1,368.705 s (22m 48.71s)** for `astra-orchestration`, and **412.261 s (6m 52.26s)** for the control. The scheduling difference means these durations are not fully controlled. Per-agent turn durations include tools and waiting, overlap, and must not be summed to obtain whole-tree wall time.

## 2. Per-agent usage and calculated API cost

All ten agents are included below. Labels L0–L2, A0–A5, and C0 identify agents within this report; parent labels show the actual tree. A1 used the named `astra_orchestration_manager` role, and A2–A5 used `astra_orchestration_worker`.

**Responses** counts distinct completed provider response IDs. **Uncached input = input − cached input. Output already includes Reasoning; Total = uncached input + cached input + output.** Reasoning must not be added again. There were no missing usage records, unassigned agents, or model reroutes. All agent, case, and global sums reconcile.

| Case | Agent role and parent | Model / effort | Responses | Uncached input | Cached input | Output | Reasoning | Total | API-equivalent USD |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|
| `luna-implement` | L0 root | `gpt-6-astra` / `medium` | 53 | 110,478 | 3,428,224 | 12,410 | 1,265 | 3,551,112 | 5.15350400 |
| `luna-implement` | L1 worker; parent L0 | `gpt-6-luna` / `max` | 12 | 47,247 | 364,800 | 8,222 | 3,890 | 420,269 | 0.01248370 |
| `luna-implement` | L2 worker; parent L0 | `gpt-6-luna` / `max` | 18 | 40,352 | 745,984 | 17,735 | 6,903 | 804,071 | 0.02036254 |
| **luna-implement subtotal** | **3 agents** |  | **83** | **198,077** | **4,539,008** | **38,367** | **12,058** | **4,775,452** | **5.18635024** |
| `astra-orchestration` | A0 root | `gpt-6-astra` / `medium` | 64 | 125,721 | 2,509,440 | 4,441 | 288 | 2,639,602 | 3.98870000 |
| `astra-orchestration` | A1 manager; parent A0 | `gpt-6.1-sol` / `xhigh` | 71 | 119,094 | 4,750,080 | 16,518 | 4,512 | 4,885,692 | 0.87837600 |
| `astra-orchestration` | A2 worker; parent A1 | `gpt-6-luna` / `max` | 20 | 63,841 | 782,592 | 10,120 | 3,241 | 856,553 | 0.01927002 |
| `astra-orchestration` | A3 worker; parent A1 | `gpt-6-luna` / `max` | 16 | 35,897 | 518,144 | 9,839 | 5,453 | 563,880 | 0.01369064 |
| `astra-orchestration` | A4 worker; parent A1 | `gpt-6-luna` / `max` | 19 | 40,844 | 728,320 | 14,515 | 6,798 | 783,679 | 0.01862510 |
| `astra-orchestration` | A5 worker; parent A1 | `gpt-6-luna` / `max` | 14 | 38,098 | 505,344 | 16,891 | 7,153 | 560,333 | 0.01730874 |
| **astra-orchestration subtotal** | **6 agents** |  | **204** | **423,495** | **9,793,920** | **72,324** | **27,445** | **10,289,739** | **4.93597050** |
| `no-test-skill` | C0 root | `gpt-6-astra` / `medium` | 20 | 78,819 | 846,976 | 10,760 | 133 | 936,555 | 2.17316600 |
| **no-test-skill subtotal** | **1 agent** |  | **20** | **78,819** | **846,976** | **10,760** | **133** | **936,555** | **2.17316600** |
| **All cases** | **10 agents** | | **307** | **700,391** | **15,179,904** | **121,451** | **39,636** | **16,001,746** | **12.29548674** |

### Price basis

Costs are **Standard API token-price equivalents in USD**, using official prices verified on **2026-10-01**, calculated with `Decimal` separately for each response. They are not actual ChatGPT charges or a conversion of subscription credits. Rates per million tokens, in the order **ordinary input / cached read / cache write / inclusive output**, were:

- `gpt-6-astra`: **$10 / $1 / $12.50 / $50** ([model](https://developers.openai.com/api/docs/models/gpt-6-astra))
- `gpt-6.1-sol`: **$2 / $0.10 / $2.50 / $10** ([model](https://developers.openai.com/api/docs/models/gpt-6.1-sol))
- `gpt-6-luna`: **$0.10 / $0.01 / $0.125 / $0.50** ([model](https://developers.openai.com/api/docs/models/gpt-6-luna))

Ordinary input excludes both cached reads and cache writes. Cost per response is `(ordinary input × input rate + cached read × cached rate + cache write × write rate + output × output rate) / 1,000,000`. A prompt with **more than 272,000 input tokens** doubles input/cache rates and multiplies output rates by 1.5 for the full request. Across all **307 responses**, maximum input was **118,594 tokens**; no long-context multiplier applied. Every response explicitly reported cache-write usage, totaling **zero**. Reasoning is charged within output, not separately. See [official pricing](https://developers.openai.com/api/docs/pricing), [prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching), and [reasoning usage](https://developers.openai.com/api/docs/guides/reasoning).

Other service tiers, regional surcharges, taxes, non-token fees, setup, and review are excluded. The control's API-equivalent cost was 58.10% below `luna-implement` and 55.97% below `astra-orchestration` in this experiment. Token totals alone do not determine cost: the orchestration arm used more total tokens than the Luna arm but had lower calculated cost because of its model mix.

## 3. Result quality

The frozen acceptance suite passed **32/32 for every case**, and all six original baseline tests remained intact. The deeper review compared **7,200 operations** with an independent oracle (24 seeded sequences × 100 operations × three implementations) and tested no-op behavior, detached values, validation-before-idempotency, and injected write/replace failures. All ordinary-input comparisons and fault probes passed. Passing those tests does not establish correctness for every possible input.

| Case | Completeness | Implementation performance | Preventive coverage and design | Overengineering |
|---|---|---|---|---|
| `luna-implement` | 32/32 acceptance; 30/30 project tests; all four phases and strict spec validation complete | Builds and sorts events for unrelated resources. Full cancellation with 150 blocked waiters: **761.808 ms** | Tests atomic rollback/cleanup, one-snapshot promotion, randomized admission, and parser `ValueError` handling | No material overengineering. Straightforward code, but unnecessary all-resource work; +61 core lines over baseline |
| `astra-orchestration` | 32/32 acceptance; 26/26 project tests; all four phases and strict spec validation complete | Filters candidate resources and aggregates timestamp deltas. Same cancellation: **235.924 ms** | Useful validation/canonicalization separation and compact event representation. No matching project replace-failure injection test found; independent fault probes passed | No material overengineering. Extra separation and representation are largely justified; +84 core lines |
| No-test-skill control | 32/32 acceptance; 18/18 project tests; all four phases and strict spec validation complete | Filters candidate resources; keeps endpoint tuples. Same cancellation: **272.830 ms** | Compact shared admission helper, atomic replace-failure regression, and a 100-operation admission/cancellation oracle | No material overengineering. Smallest production-code change; +49 core lines |

**Performance context.** The cancellation workload had 8,000 confirmed items on 100 unrelated resources plus 150 blocked waiters. Values above are the supervising reviewer's independent repeat: medians of seven samples after two warmups, randomized interleaving, warm filesystem cache, reset excluded, no CLI startup. Environment: Python 3.12.14, Linux x86_64, AMD EPYC 9V74, nine CPUs in process affinity, shared cloud host. These are implementation-operation timings, not model generation duration or service guarantees. A full reservation on the unrelated-resource state was much closer: Astra **112.322 ms**, control **114.176 ms**, Luna **121.788 ms**, because common JSON I/O dominates. All three still rebuild capacity state during promotion, leaving a shared repeated-scan scalability limit.

**Shared defect, not hidden by the pass counts.** A `batch --items` value of `'[' * 10000 + '0' + ']' * 10000` causes all three CLIs to exit 1 with a `RecursionError` traceback, rather than exit 2 with the required JSON validation error. This low-frequency pathological-input gap in the new batch parser was independently reproduced. Deeply nested malformed database input has an analogous inherited reader defect. Other weak validation of manually corrupted saved schemas largely comes from the baseline and was not scored as a new feature regression; malformed JSON and malformed internal schemas are distinct concerns.

All outputs preserved the single-file version-1 JSON format and standard-library-only scope. None introduced an unrequested framework, dependency, migration layer, concurrency mechanism, or feature. Atomic replacement, fresh reads, and deep-copy returns were baseline primitives; the feature work correctly reused them rather than inventing them. Raw test counts should not be treated as quality scores.

## Limits and conclusion

This is one task and one trial per condition. The original pair shared machine/provider capacity; the later control did not share that concurrent workload. Provider load, prompt-cache warmth, and possible cache reuse were not reset. The control deliberately lacks the two test skills and their agent definitions, so its configuration is not byte-identical to the treatment workspaces. The common task is identical; the exact driver/configuration differences are described above. Experimental app-server usage telemetry was verified on the installed version and is not a portability guarantee.

For this task, the control was the least expensive generation path and produced compact, well-tested code. The Astra orchestration output had the best measured capacity representation and promotion performance. Luna's output was functionally complete on ordinary tested inputs but did avoidable unrelated-resource work. All three share the disclosed edge-input gap, and none showed material overengineering. These observations do not establish model-level superiority or predict results on a different workload.

The fixture, full task text, acceptance runner, sanitized per-response capture, source hashes, and detailed review evidence were retained separately. This documentation-only commit publishes the procedure and results, not a self-contained rerunnable benchmark harness. Accounting/pricing checks (40) and independent-capture merger checks (9) passed; they validate reporting, not application correctness.
