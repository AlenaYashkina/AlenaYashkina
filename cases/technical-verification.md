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
- **Report reproducibility:** a complete single-day workflow was executed on Windows from two generated photos with actual parsing and PPTX output; the much larger multi-month archival dataset and every production configuration are **not** fully covered.
- **Third-party services:** the published RentGram Netlify demo was tested in real Chromium and displayed nonempty synthetic listing cards with no NDJSON parsing errors. This does not establish future uptime. The retired CRM's Vercel site is still outside the featured portfolio and should be disabled separately.
- **Historic data:** current demonstration datasets no longer include original Telegram contacts/exports, but removing current files does not erase previous Git commits.

## Reviewer quick checks

1. **RentGram:** `cd frontend && npm ci && npm test && npm run build`; open the synthetic demo; verify sales and daily offers do not appear as monthly rent.
2. **Cluster Forge:** `python -m pip install pytest && python -m pytest -q tests/test_safe_cluster_names.py tests/test_undo_safety.py`. Run any filesystem UI experiment only inside a configured disposable `CLUSTER_FORGE_WORKSPACE`.
3. **Photo reports:** `python -m pip install -r requirements.txt && python examples/tiny_demo.py`; inspect the generated PPTX, the two source images, and CI proof.
4. **Telegram loader:** `python -m pip install -e . && python examples/offline_layout_demo.py`; no Telegram account required.

This document records actual automated results, not fabricated productivity metrics or proof of live services. It is deliberately separate from the concise recruiter-oriented front page.


## Follow-up verification — 2026-11-06

Subsequent fixes were exercised, not inferred from code inspection alone:

| Project | Regression check | Evidence |
| --- | --- | --- |
| RentGram | Correctly parse static NDJSON and fallback JSON API; reject malformed data; frontend tests and build passed | [Parser fix PR #12](https://github.com/AlenaYashkina/rent_gram/pull/12) |
| RentGram published website | Chromium visited `https://rent-gram.netlify.app/`; asserted the listing count was above zero, at least one card rendered, and no parser exceptions. Screenshot was recorded as a CI artifact | [Live browser test run](https://github.com/AlenaYashkina/rent_gram/actions/runs/42235311644) · [PR #14](https://github.com/AlenaYashkina/rent_gram/pull/14) |
| Cluster Forge | Failed automatic moves leave images in manual queue; successful move removes only its source; Python 3.11 clean install (including real CLIP module imports) and React build all passed | [Backend install/build](https://github.com/AlenaYashkina/cluster-forge/actions/runs/42233808001) · [Queue regression tests](https://github.com/AlenaYashkina/cluster-forge/actions/runs/42233807900) · [PR #9](https://github.com/AlenaYashkina/cluster-forge/pull/9) |
| Photo Report Generator | Actual `main.py` orchestration on a small synthetic folder, real PPTX with embedded photos, source hashes unchanged | [Full pipeline Windows run](https://github.com/AlenaYashkina/photo-report-generator/actions/runs/42234447855) · [PR #9](https://github.com/AlenaYashkina/photo-report-generator/pull/9) |
| Telegram Media Loader | Real downloader workflow with injected fictional Telegram messages, including SQLite and NDJSON, UTC date boundaries and rerun deduplication | [Fake-client CI](https://github.com/AlenaYashkina/tg_media_loader/actions/runs/42234139045) · [PR #8](https://github.com/AlenaYashkina/tg_media_loader/pull/8) |

The tests do not substitute for testing actual Telegram account authentication, all production reporting configurations, CLIP classification quality, or permission controls on the user's hosted CRM environment.

### Visible portfolio case evidence

The [property-management case](property-management-automation.md) explains the connected Supabase ↔ ChatGPT ↔ Jira workflow using verified integration documentation and **two** synthetic UI reconstructions (expenses/reimbursements and owner reports). The separate invented guest-support screen was removed: ChatGPT retrieval and human-reviewed replies are described in text, because no standalone support dashboard is deployed. These are not captures of production records.

### Access and privacy actions not verifiable from CI

- The CRM technical-assignment repository `AlenaYashkina/testing` must be set to **Private** in GitHub settings and the Vercel site `project-tgn4y` disabled or protected, including older deployment URLs; removing its profile link and scheduled sync does not close access.
- The public GitHub profile sidebar contact should use the same verified Telegram handle as README: `@alena_yashkina`. The repository's About description for Cluster Forge should be clarified; repo text edits cannot update either account-level setting.
- Existing photo and presentation pixels still require a **human visual and publication-rights review**. Automated token-pattern, EXIF and Office metadata checks do not clear faces, addresses, signage or copyrighted content. A local-only contact-sheet/checklist generator exists in the photo-report repository; its output should stay private.
