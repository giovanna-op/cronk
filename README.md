# Cronk: a cron-json translator

---

_This repository is an educational project for learning software supply-chain security with OpenSSF Scorecard and SLSA. It is meant for demonstrative purposes and should not be used in production!_

_All project backstory beyond this point is fictional!_

---

- **Student:** Giovanna de O. Pinheiro, 2026.2
- **Course:** MAC0696 - Cibersegurança e Privacidade @ University of São Paulo (USP)

Cronk allows developers to convert files between the `crontab` and `json` formats.

## Project Structure

- `src/cronk/`: Python package for converting between `crontab` and `json` schedules.
- `src/cronk-helper/`: Small C CLI helper that prints the standard 5-field `crontab` syntax banner (`bin/cronk-helper`). The binary is not versioned; build it with `./src/cronk-helper/compile.sh`.
- `tests/`: Unit tests for `cron_to_json` and `json_to_cron`.

- 
## Supply-chain security

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/giovanna-op/cronk/badge)](https://scorecard.dev/viewer/?uri=github.com/giovanna-op/cronk)

Final [OpenSSF Scorecard](https://scorecard.dev/viewer/?uri=github.com/giovanna-op/cronk) score: **7.1 / 10** (baseline: ~1.8).

| Checkpoint | What changed | Why it matters |
| --- | --- | --- |
| 2 | Removed the committed binary and the `pull_request_target` workflow; added `LICENSE` and `SECURITY.md` | Opaque binaries and shell injection in workflows are classic supply-chain entry points; a license and a security policy make the project usable and reportable |
| 3 | Added CI tests and CodeQL; created a ruleset on `main` (PRs and passing checks required, no force-push or deletion) | Nothing reaches `main` without tests and static analysis |
| 4 | Fixed the CodeQL alert, enabled Dependabot, upgraded vulnerable dependencies, hash-pinned all `pip` installs | Known CVEs are gone and tampered packages fail the install |
| 5 | Release workflow with OIDC trusted publishing and hash-pinned build tools | No long-lived publishing token that could leak |
| 6 | SLSA Level 3 provenance attached to the GitHub Release (`v0.0.1`) | Anyone can verify the artifact came from this repository's CI |

Score progression: 6.7 (before the first Release run), 6.8 (`Packaging` at 10), 7.1 (`Signed-Releases` at 10).

### Issue found and fixed: invalid action SHAs in `release.yml`

When pushing the `v0.0.1` tag, the *Publish to TestPyPI* and *Upload distributions to GitHub Release* jobs failed at *Set up job* with `unable to find version <sha>`. The `actions/download-artifact` and `softprops/action-gh-release` actions were pinned to commit SHAs that do not exist in their repositories, so hash-pinning was in the right format but pointed at nothing. I replaced both with SHAs of real release commits (`download-artifact` v8.0.2, `action-gh-release` v3.0.4) through a pull request, then recreated the `v0.0.1` tag on `main` to re-trigger the workflow. The Release run turned green and `Signed-Releases` went to 10.

### Checks that remain low, and why

- `Maintained`: the repository is less than 90 days old.
- `Contributors`: a single contributor.
- `Code-Review`: the ruleset requires 0 approvals so a solo developer can merge.
- `Fuzzing` and `CII-Best-Practices`: out of scope for this exercise.
