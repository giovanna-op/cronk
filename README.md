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
- `src/cronk-helper/`: Small C CLI helper that prints the standard 5-field `crontab` syntax banner (`bin/cronk-helper`).
- `tests/`: Unit tests for `cron_to_json` and `json_to_cron`.

## To-do

- Add i18n of periodicity via Babel
