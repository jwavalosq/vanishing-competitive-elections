# Build Report — "How Politicians Choose Their Voters"

Built locally on 2026-11-02. **Nothing was published.** No accounts were used, no sign-ins happened, no `git push` was run, and no remote repository was created. Everything below lives only in this folder until the user provides publishing access.

## What ran successfully

Every notebook was executed end to end with `jupyter nbconvert --execute` and finished with **zero cell errors**. All six charts were generated from the computed data (none hand-drawn, none invented).

| Notebook | Result |
|---|---|
| `00_setup.ipynb` | Environment check passed (Python 3.12, pandas, matplotlib, geopandas). |
| `01_toy_example.ipynb` | 5×5 grid, 13 A / 12 B. Rows: A wins 4–1, efficiency gap +32.0% (favors A). Columns: B wins 3–2, efficiency gap −16.0% (favors B). Chart: `charts/phase1_seats_vs_votes.png`. |
| `02_one_real_state.ipynb` | North Carolina 2016 (13 districts, all contested): Democratic vote 46.7%, seats 3 of 13. Efficiency gap −19.4% (favors R). Mean–median difference +4.8 points. Partisan bias (uniform swing) −26.9 points. Chart: `charts/phase2_nc2016_voteshare.png`. |
| `03_maps_over_time.ipynb` | NC maps plotted for 2016 (115th Congress), 2020 (116th Congress), 2024 (119th Congress): 13, 13, and 14 districts. Verified 11 of 13 districts were redrawn between the 2016 and 2020 maps. Seat counts: 3D–10R (2016), 5D–8R (2020), 4D–10R (2024). Chart: `charts/phase3_nc_maps_2016_2020_2024.png`. |
| `04_vanishing_competitive_elections.ipynb` | Competitive-share series 1976–2024 (25 elections) saved to `data/processed/competitive_share_by_year.csv`. Charts: `charts/phase4_competitive_share.png` and `charts/phase4_seats_votes_gap.png`. |
| `05_gerrychain_ensemble.ipynb` | Nevada, 1,000-map ReCom ensemble in ~30 s. Real map efficiency gap +19.1% (2020 presidential votes); ensemble mean +7.3%, SD 13.7 points, range −36.1% to +21.4%; 14.9% of random maps lean as far or further Democratic. Chart: `charts/phase5_nevada_ensemble.png`. Ensemble values saved to `data/processed/nevada_ensemble_eg.csv`. |

## Every dataset used, with its URL

| File in `data/raw/` | Source | URL |
|---|---|---|
| `congressional_election_results_post1948.csv` (674 KB) | Princeton gerrymetrics, bundled congressional results. File actually covers 1948–2018 (the repo README says 1948–2016). | https://raw.githubusercontent.com/PrincetonUniversity/gerrymandertests/master/election_data/congressional_election_results_post1948.csv |
| `house_tidytuesday_1976_2022.csv` (4.0 MB) | MIT Election Data + Science Lab House returns 1976–2022, via the TidyTuesday mirror (clean CSV, same data). | https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-11-07/house.csv |
| `house_1976_2024.csv` (4.2 MB) | MIT Election Data + Science Lab House returns 1976–2024, Harvard Dataverse DOI 10.7910/DVN/IG0UN2, via a public mirror (see "Failures and approximations"). | Mirror: https://raw.githubusercontent.com/keithpotz/Election-Prediction/main/src/data/polling_data/house_1976_2024.csv — Dataverse page: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/IG0UN2 |
| `cb_2017_us_cd115_20m.zip` (408 KB) | U.S. Census Bureau, cartographic boundary file, 115th Congress, 1:20,000,000. | https://www2.census.gov/geo/tiger/GENZ2017/shp/cb_2017_us_cd115_20m.zip |
| `cb_2020_us_cd116_20m.zip` (405 KB) | U.S. Census Bureau, cartographic boundary file, 116th Congress, 1:20,000,000 (2020 vintage captures the November 2019 NC redraw — verified: 11 of 13 NC districts differ from the 2017 file). | https://www2.census.gov/geo/tiger/GENZ2020/shp/cb_2020_us_cd116_20m.zip |
| `cb_2025_us_cd119_20m.zip` (410 KB) | U.S. Census Bureau, cartographic boundary file, 119th Congress, 1:20,000,000. | https://www2.census.gov/geo/tiger/GENZ2025/shp/cb_2025_us_cd119_20m.zip |
| `nv.json` (2.8 MB) | eveomett-states Nevada precinct file (post-2020, built from Redistricting Data Hub / VEST data with `maup`), CC BY-NC 4.0. Not for litigation (project's own warning, repeated in the notebook). | https://raw.githubusercontent.com/eveomett-states/Nevada/main/nv.json |

## Failures, approximations, and honest corrections

1. **The headline claim did not survive testing — and the notebook says so.** The task's premise (competitive seats "drastically reduced") was tested exactly as specified: margin ≤ 5 points, every House election 1976–2024. The share does **not** decline; it bounces between ~2% and ~11%, spiking in wave years (1994, 2010, 2018) and collapsing in quiet years (2004, 1988, 2016). The notebook reports this plainly instead of claiming a decline, and adds a second, independent lens that *does* show a real break: the seats–votes gap flipped from a persistent Democratic bonus (+5 to +10 points, 1976–1992) to a Republican bonus in 2012–2016 (−4.0, −3.9, −4.7), including the 2012 "wrong-winner" House (Democrats won the vote, lost the chamber 201–234). The literature's "vanishing competition" claim is usually measured by presidential partisanship or expert ratings, which need presidential-by-district data not in these files — the notebook states this.
2. **MIT 1976–2024 Dataverse download is guestbook-blocked.** The Dataverse dataset (DOI 10.7910/DVN/IG0UN2) requires accepting a guestbook form, so it cannot be downloaded unattended. The build uses a public mirror of the same file instead, with a documented quirk: every row is wrapped in quotation marks and 56 of 33,805 rows are malformed (extra commas inside a field). The notebooks skip those rows (0.17%) and cross-check the result: the mirror reproduces NC 2016 (10R/3D) and NC 2020 (8R/5D) exactly as the clean TidyTuesday file does, and yields 435 seats for 2024 (10R/4D in NC, matching the official count).
3. **No Census cartographic file exists for the 117th Congress.** The 2020 election map therefore uses the 116th Congress file, 2020 vintage (`cb_2020_us_cd116_20m.zip`), which captures the November 2019 NC redraw — verified geometrically (11 of 13 NC districts differ from the 2017 file). State-based cartographic district files do not exist under the expected URLs (all returned 404); the national 20m files were used and filtered to NC.
4. **A few years cover fewer than 435 seats in the MIT file** (1992: 427, 1996: 425, 2006: 431). Shares are computed over covered seats; the notebooks note this.
5. **GerryChain 1.0 API differs from older tutorials.** `Graph.nodes` is a property (use `graph.node_data(id)`), `recom` is a factory requiring `pop_col`/`pop_target`/`epsilon`, and `MarkovChain` takes `initial_partition`. The notebook uses the 1.0 API. The ensemble uses a population-balance constraint only (within 10%); a court-grade analysis would add compactness and Voting Rights Act constraints, and the notebook says so. Chain steps are correlated; the notebook notes that a rigorous study would thin the chain and run longer.
6. **Princeton file coverage differs from its README.** The repo README says 1948–2016; the downloaded CSV actually runs 1948–2018. The notebook and README here use the verified range.
7. **Environment note.** The first install attempt failed (disk-full in `/tmp`, a 512 MB tmpfs). The working virtualenv lives outside the repo at `~/.venvs/elections` (geopandas 1.2.0, pandas 3.1.0, jupyter/nbconvert). The repo itself contains no virtualenv and is ready to publish as-is; on Colab, each notebook's first cell installs what it needs.

## What still needs the user

**Nothing except publishing access.** To publish, the user must provide (or approve) a way to create a GitHub repository and push this folder — that step was explicitly excluded from this build and has not been done. Suggested next step when access is provided: create the repo, push, enable GitHub Pages or add a Streamlit app link, and post the headline chart on LinkedIn.
