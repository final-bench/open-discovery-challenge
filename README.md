# Open Discovery Challenge (ODC)

An open drug discovery competition. Anyone submits a molecule as SMILES. Every entry is scored
by the same automated pipeline and placed on a public leaderboard.

**Participate:** https://huggingface.co/spaces/FINAL-Bench/open-discovery-challenge
**Submission and result ledger:** `FINAL-Bench/odc-submissions` (Hugging Face dataset)

Run by [VIDRAFT](https://vidraft.net). A Hugging Face login is required to submit.

## Seasons

Each season is a different disease and a different protein target. A counter target is scored
alongside the target, so an entry that binds both does not win on potency alone.

| Season | Topic | Organism | Target | Counter target | Closes | Prize | Status |
|---|---|---|---|---|---|---|---|
| 1 | Malaria | *Plasmodium falciparum* | PfDHODH | human DHODH | 2026-09-30 | USD 1,000 | closed |
| 2 | Tuberculosis | *Mycobacterium tuberculosis* | InhA | human FASN (ER domain) | 2026-10-31 | USD 2,000 | open |
| 3 | Chagas disease | *Trypanosoma cruzi* | T. cruzi CYP51 | human CYP51A1 | 2026-11-30 | USD 1,000 | open |
| 4 | Non-opioid analgesia | *Homo sapiens* | Nav1.7 (VSD4) | hERG (pore tetramer) | 2027-01-31 | USD 1,000 | open |

Season 1 no longer accepts submissions. The other seasons accept entries until their closing date.
The live values are served at `/api/seasons` on the Space.

## Scoring

Six axes. The weights differ per season because the biology differs.

| Axis | S1 | S2 | S3 | S4 |
|---|---|---|---|---|
| Activity | 30 | 20 | 10 | 10 |
| Binding | 20 | 25 | 30 | 30 |
| Selectivity | 20 | 25 | **30** | 30 |
| **Total** | **100** | **100** | **100** | **100** |
| ADMET | 15 | 15 | 15 | 15 |
| Novelty | 10 | 10 | 10 | 10 |
| Synthesis | 5 | 5 | 5 | 5 |

Binding and selectivity come from structure prediction against the target and the counter target.
Every entry is docked repeatedly and the repeats are reported with the score, so a single lucky
pose does not decide a rank.

**These are computational predictions, not experimental measurements.** A high score is a
hypothesis worth testing in a laboratory. It is not evidence of activity in cells or in animals.

## Entry limits

| Season | Max molecular weight | Max heavy atoms |
|---|---|---|
| 1 | 550 | 45 |
| 2 | 550 | 45 |
| 3 | 750 | 55 |
| 4 | 600 | 45 |

Entries outside these limits are rejected at submission time with the reason shown.

## How a measurement failure is handled

If any axis cannot be computed, no result is written. A missing axis is a state, not a score of
zero. An entry whose score is absent has not been graded yet, and an entry that fails repeatedly
for environment reasons such as a full GPU is kept in the queue rather than discarded.

## What is in this repository

Public competition facts: seasons, targets, scoring weights, entry limits and the links above.

The scoring implementation, the gate thresholds beyond the published entry limits, and the
reference sets used for novelty are not published. Publishing them would let an entry be shaped
against the grader rather than against the biology.

## Related

| | |
|---|---|
| Open Materials Challenge | https://github.com/final-bench/open-materials-challenge |
| Open Quantum Challenge | https://huggingface.co/spaces/FINAL-Bench/open-quantum-challenge |
| Hugging Face organisation | https://huggingface.co/FINAL-Bench |

## Contact

vidraft@mail.vidraft.net · [vidraft.net](https://vidraft.net) · X [@VIDRAFT_ai](https://x.com/VIDRAFT_ai) · Threads [@vidraft_lab](https://www.threads.com/@vidraft_lab)
