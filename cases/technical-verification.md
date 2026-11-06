# Portfolio verification record — 2026-11-06

This record distinguishes executed checks from incomplete audits. Tests use synthetic data and no private CRM, Telegram or organization credentials. Commits and workflow URLs are fixed references so a reviewer can reproduce the evidence.

## Scope

| Public project | Verified main commit | Executed verification | Evidence |
| --- | --- | --- | --- |
| [RentGram](https://github.com/AlenaYashkina/rent_gram) | [`10477ef`](https://github.com/AlenaYashkina/rent_gram/commit/10477efb5c628ebd4750f7e8d7621a694bca9f2c) | React/Vite build; Node classification/dedupe regression tests; Python extraction normalization tests | [PR #6](https://github.com/AlenaYashkina/rent_gram/pull/6), [PR #8](https://github.com/AlenaYashkina/rent_gram/pull/8) |
| [Cluster Forge](https://github.com/AlenaYashkina/cluster-forge) | [`fe7dd2e`](https://github.com/AlenaYashkina/cluster-forge/commit/fe7dd2ecf98ad54e025163460aa5c43f485fe478) | Python tests for unsafe paths, symlink escape, undo collision and workspace boundaries; compilation smoke checks | [PR #5](https://github.com/AlenaYashkina/cluster-forge/pull/5), [preview PR #7](https://github.com/AlenaYashkina/cluster-forge/pull/7) |
| [Photo Report Generator](https://github.com/AlenaYashkina/photo-report-generator) | [`408da79`](https://github.com/AlenaYashkina/photo-report-generator/commit/408da799c7d5c9ac148783a4d811cc2eb99f43ae) | Windows Python 3.11 dependency install/compile, synthetic PPTX with two embedded photos, unchanged input hashes | [PR #3](https://github.com/AlenaYashkina/photo-report-generator/pull/3), [PDF preview PR #6](https://github.com/AlenaYashkina/photo-report-generator/pull/6) |
| [Telegram Media Loader](https://github.com/AlenaYashkina/tg_media_loader) | [`aa3c078`](https://github.com/AlenaYashkina/tg_media_loader/commit/aa3c078156cba01d05ac73bea18425590ed19fa6) | Python 3.11 offline example; UTC date boundary, album grouping and two-pass deduplication | [PR #5](https://github.com/AlenaYashkina/tg_media_loader/pull/5) |

Check the latest project workflow runs if the default branch moved after this record; pinned commits describe the checks as of 2026-11-06.

## Secret scanning

`Gitleaks v8.30.1` ran with `git --redact --log-opts="--all"` and a full-ref checkout on **five featured portfolio repositories**. All returned `no leaks found` (known-token-pattern scan, not an independent privacy certification).

| Repo | Git commits scanned | Executed run |
| --- | ---: | --- |
| Profile | 31 | [History scan](https://github.com/AlenaYashkina/AlenaYashkina/actions/runs/42192775178) |
| RentGram | 30 | [History scan](https://github.com/AlenaYashkina/rent_gram/actions/runs/42192797284) |
| Cluster Forge | 22 | [History scan](https://github.com/AlenaYashkina/cluster-forge/actions/runs/42192817542) |
| Photo Report Generator | 20 | [History scan](https://github.com/AlenaYashkina/photo-report-generator/actions/runs/42192834132) |
| Telegram Media Loader | 15 | [History scan](https://github.com/AlenaYashkina/tg_media_loader/actions/runs/42192850858) |

Total: **118 scanned commits**, as reported by GitHub Actions. Results may change if new commits are added or secret patterns evolve. Scan outputs do not prove that historic third-party phone numbers and posts are absent.

## Sample-media metadata inventory

A separate non-destructive script enumerated **1,558 images** and **6 Office documents** in the report-generator `examples` directory. It found **0** images with GPS or detected owner/serial EXIF, **0** Office XML documents with email-like strings, and **0** unreadable assets in those categories. [Execution record](https://github.com/AlenaYashkina/photo-report-generator/actions/runs/42193907684). The script deliberately does not emit any values or individual file contents.

**Not verified:** people/faces/addresses visible in pixels, intellectual-property rights, all XML metadata fields, archive history, private URLs, and every historic Git blob. Human review of sample media remains required before representing it as fully privacy-cleared.

## Technical constraints and known limits

- **Demo vs integration:** public RentGram examples and the small report/Telegram samples are synthetic. Their outputs are not proof of rental availability, work completion or production uptime.
- **CLIP evaluation:** filesystem safety and undo were tested; end-to-end CLIP quality on a separately labeled validation image dataset has **not** been measured. Similarity thresholds are not classification accuracy.
- **Report reproducibility:** the small photo-slide component was verified on Windows, but the entire multi-month worksite-report workflow was **not** executed end-to-end from a clean dataset.
- **Third-party services:** availability of public Netlify/Vercel deployments was **not** visually confirmed during this record. A passing CI build does not replace a browser check.
- **Historic data:** current demonstration datasets no longer include original Telegram contacts/exports, but removing current files does not erase previous Git commits.

## Reviewer quick checks

1. **RentGram:** `cd frontend && npm ci && npm test && npm run build`; open the synthetic demo; verify sales and daily offers do not appear as monthly rent.
2. **Cluster Forge:** `python -m pip install pytest && python -m pytest -q tests/test_safe_cluster_names.py tests/test_undo_safety.py`. Run any filesystem UI experiment only inside a configured disposable `CLUSTER_FORGE_WORKSPACE`.
3. **Photo reports:** `python -m pip install -r requirements.txt && python examples/tiny_demo.py`; inspect the generated PPTX, the two source images, and CI proof.
4. **Telegram loader:** `python -m pip install -e . && python examples/offline_layout_demo.py`; no Telegram account required.

This document records actual automated results, not fabricated productivity metrics or proof of live services. It is deliberately separate from the concise recruiter-oriented front page.
