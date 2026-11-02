# How Politicians Choose Their Voters: The Vanishing Competitive Election in America

**In America, voters are supposed to choose their politicians. In many districts, it's the other way around.**

This is a data story told in five chapters, written for anyone — no background in politics, statistics, or code needed. Every concept is explained in plain words before it is used, and every chart can be traced back to a public, free dataset.

> **Testing the famous claim, honestly.** This project started from the popular claim that competitive seats are vanishing. When we tested it exactly — every House election 1976–2024, "competitive" defined as a margin of 5 points or less — the share did *not* decline: it bounces between ~2% and ~11%, spiking in wave years and collapsing in quiet ones. What the data *does* show, clearly, is gerrymandering's fingerprints elsewhere: North Carolina 2016 turned 46.7% of the vote into 3 of 13 seats, and the national seats–votes gap flipped from a Democratic bonus (1976–1992) to a Republican bonus in 2012–2016, including the 2012 "wrong-winner" House. This project shows the tricks, tests the claim, and reports what survived — including the result that surprised us.

## The story in one paragraph

Every ten years, after the Census, each state redraws the boundaries of its congressional districts. Whoever draws the lines can decide who wins — without changing a single vote. Two tricks do most of the work: **packing** (stuffing your opponent's voters into one district they win by a landslide, wasting their votes) and **cracking** (spreading them thinly across many districts they all lose narrowly). This project shows how the tricks work, proves them with real maps and real numbers from North Carolina and Nevada, tests the famous "vanishing competition" claim against 25 elections of data, and ends with a statistical test of whether one state's map is an outlier.

## The five chapters

| Notebook | Chapter | What you will learn |
|---|---|---|
| `notebooks/00_setup.ipynb` | Setup | Project structure, tools, and where every dataset comes from |
| `notebooks/01_toy_example.ipynb` | The toy example | Packing, cracking, and the efficiency gap — with 25 voters on a 5×5 grid |
| `notebooks/02_one_real_state.ipynb` | One real state | Real metrics for North Carolina: efficiency gap, mean–median difference, partisan bias |
| `notebooks/03_maps_over_time.ipynb` | Maps over time | How district boundaries moved in 2016, 2020, and 2024 |
| `notebooks/04_vanishing_competitive_elections.ipynb` | The original finding | Testing whether competitive seats are vanishing (1976–2024) — plus the seats–votes gap flip the data actually shows |
| `notebooks/05_gerrychain_ensemble.ipynb` | The advanced proof | Is the real map an outlier? A 1,000-map GerryChain ensemble test for Nevada |

## How to run it

**Option A — Google Colab (recommended, free, nothing to install on your computer):**
1. Open any notebook in [Google Colab](https://colab.research.google.com/).
2. Run the first cell — it installs everything the notebook needs.
3. Run the rest of the cells top to bottom.

**Option B — On your own computer:**
```bash
pip install -r requirements.txt
jupyter notebook notebooks/
```

## Data sources (all public and free)

- **Princeton gerrymetrics** — bundled congressional election results 1948–2018 and metric code: https://github.com/PrincetonUniversity/gerrymandertests
- **MIT Election Data + Science Lab / Harvard Dataverse** — U.S. House results 1976–2022 (TidyTuesday mirror) and 1976–2024 (Dataverse DOI 10.7910/DVN/IG0UN2, via a public mirror — see `BUILD_REPORT.md` for why and how it was cross-checked)
- **U.S. Census Bureau, TIGER/Line** — congressional district boundary shapefiles (1:20,000,000 cartographic boundary files, chosen to keep downloads small): https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2020.html
- **GerryChain** (Phase 5 only) — https://github.com/mggg/GerryChain — docs: https://gerrychain.readthedocs.io/en/v1.0.0/
- **OpenElections** — precinct-level results index: https://github.com/orgs/openelections/repositories

See `BUILD_REPORT.md` for exactly which files were used, what ran, and what (if anything) failed or was approximated.

## What "competitive" means here

A district is called **competitive** in this project when the winner's margin of victory is **5 percentage points or less** — close enough that either party could plausibly win it. That threshold is a choice, not a law of nature, and the notebooks say so wherever it matters.

## License and honesty note

All data used here is public. No numbers in this project are invented: every chart is computed from the datasets above, and anything that could not be reproduced is documented in `BUILD_REPORT.md`.
