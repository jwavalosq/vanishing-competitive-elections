# How Politicians Choose Their Voters: The Vanishing Competitive Election in America

**Read the story site:** https://jwavalosq.github.io/vanishing-competitive-elections/

I started with a simple question. In America, voters are supposed to choose their politicians. So why do so many elections feel decided before anyone votes? I had heard the famous claim that competitive seats are vanishing. I wanted to test it myself, with real data, instead of repeating it.

## The question I started with

Every ten years, after the Census, each state redraws the boundaries of its congressional districts. Whoever draws the lines can decide who wins, without changing a single vote. I wanted to know how that works, whether it really shows up in the results, and whether competition in House elections is actually disappearing.

## Why it matters

If the lines decide the winner, then the election that matters is the map drawing, not the vote. That affects who gets heard, which issues get attention, and whether a representative has any reason to listen to voters who disagree with them. You do not need a background in politics, statistics, or code to follow this project. I explain every concept in plain words before I use it, and every chart traces back to a public, free dataset.

## What I did

I built this in five steps, one notebook per step, and I ran every notebook end to end with zero cell errors.

1. **I started small, with 25 voters.** I drew a 5 by 5 grid, 13 voters for Party A and 12 for Party B, and I drew the districts two different ways. Same voters, same votes. Drawn by rows, Party A wins 4 to 1. Drawn by columns, Party B wins 3 to 2. Nothing changed except the lines. That is the whole trick, and it fits on one page.
2. **I measured one real state.** I took North Carolina in 2016 and computed the standard fairness metrics: the efficiency gap, the mean-median difference, and partisan bias. Real votes, real map, real numbers.
3. **I watched the maps move.** I plotted North Carolina's districts in 2016, 2020, and 2024, and I checked how many districts were redrawn between maps.
4. **I tested the famous claim.** I took every House election from 1976 to 2024, 25 elections, and I measured the share of seats decided by 5 points or less. I also measured the national gap between seat share and vote share over the same period.
5. **I ran the statistical test.** I generated 1,000 legal alternative maps of Nevada with GerryChain and asked whether the real map looks like a typical map drawn without partisan intent.

## What I found

First, the honest surprise. The famous claim did not survive my test.

**Competitive seats are not vanishing.** Tested exactly, every House election from 1976 to 2024, with "competitive" defined as a margin of 5 points or less, the competitive share does not decline. It bounces between about 2% and 11%, spiking in wave years and collapsing in quiet ones. In 1976 it was 8.3%. In 2022 it was 8.7%. In 2024 it was 8.3%. I started this project expecting a decline, and the data said otherwise. A good analyst reports that, even when it breaks the story they started with.

But something real did break, and it is the story this project actually tells.

**North Carolina, 2016.** Democrats won 46.7% of the vote and 3 of 13 seats. The efficiency gap was minus 19.4%, favoring Republicans, one of the largest in the country that year. The mean-median difference was plus 4.8 points. Partisan bias, under a uniform swing, was minus 26.9 points. Nearly half the votes, less than a quarter of the seats.

**The maps kept moving while the voters barely did.** Between the 2016 and 2020 maps alone, 11 of 13 North Carolina districts were redrawn. Seat counts went 3D to 10R in 2016, then 5D to 8R in 2020, then 4D to 10R in 2024.

**The national seats-votes gap flipped.** From 1976 to 1992, the gap was a persistent Democratic bonus of plus 5 to plus 10 points. In 2012 to 2016, it became a Republican bonus: minus 4.0, minus 3.9, minus 4.7. That includes 2012, the "wrong-winner" House, where Democrats won the national vote and lost the chamber 201 to 234.

**Nevada: a lean, not a smoking gun.** Nevada's real map sits at an efficiency gap of plus 19.1%. The 1,000 random maps averaged plus 7.3%, and 14.9% of them lean as far or further in the same direction. So the map leans, but it is not a proven outlier. Saying so is the point. Not every suspicious-looking map is a proven gerrymander.

## What it means, and who it helps

Gerrymandering is real, and I can show you exactly how it works and where it shows up in the numbers. But the most repeated claim about it, that competitive seats are vanishing, does not hold up when you test it the way I tested it. That distinction matters. If you are a voter, a student, a journalist, or a hiring manager reading this, you now have a tested answer instead of a slogan, and you can check my work yourself. Every number here is computed from public data, and the one result that surprised me is reported right next to the ones that confirmed what I expected.

## The six chapters

| Notebook | Chapter | What you will learn |
|---|---|---|
| `notebooks/00_setup.ipynb` | Setup | Project structure, tools, and where every dataset comes from |
| `notebooks/01_toy_example.ipynb` | The toy example | Packing, cracking, and the efficiency gap, with 25 voters on a 5 by 5 grid |
| `notebooks/02_one_real_state.ipynb` | One real state | Real metrics for North Carolina: efficiency gap, mean-median difference, partisan bias |
| `notebooks/03_maps_over_time.ipynb` | Maps over time | How district boundaries moved in 2016, 2020, and 2024 |
| `notebooks/04_vanishing_competitive_elections.ipynb` | The original finding | Testing whether competitive seats are vanishing (1976 to 2024), plus the seats-votes gap flip the data actually shows |
| `notebooks/05_gerrychain_ensemble.ipynb` | The advanced proof | Is the real map an outlier? A 1,000-map GerryChain ensemble test for Nevada |

## How to run it yourself

**Option A, Google Colab (recommended, free, nothing to install on your computer):**
1. Open any notebook in [Google Colab](https://colab.research.google.com/).
2. Run the first cell. It installs everything the notebook needs.
3. Run the rest of the cells top to bottom.

**Option B, on your own computer:**
```bash
pip install -r requirements.txt
jupyter notebook notebooks/
```

## What the limits are, stated honestly

A district counts as **competitive** here when the winner's margin is **5 percentage points or less**. That threshold is a choice, not a law of nature, and I say so in the notebooks wherever it matters.

A few more limits I want you to know. The MIT House file for 1976 to 2024 comes from a public mirror, because the Harvard Dataverse download requires a guestbook form. That mirror has 56 malformed rows out of 33,805, and I skip those rows (0.17%). I cross-checked the result: the mirror reproduces North Carolina 2016 (10R, 3D) and 2020 (8R, 5D) exactly, and it gives 435 seats for 2024. A few years cover fewer than 435 seats in the MIT file (1992: 427, 1996: 425, 2006: 431). I compute shares over covered seats and I note that. There is no Census cartographic file for the 117th Congress, so the 2020 election map uses the 116th Congress file, 2020 vintage, which captures the November 2019 North Carolina redraw. I verified that geometrically: 11 of 13 North Carolina districts differ from the 2017 file. The Nevada ensemble uses a population-balance constraint only (within 10%). A court-grade analysis would add compactness and Voting Rights Act constraints, and the notebook says so. The literature's "vanishing competition" claim is usually measured by presidential partisanship or expert ratings, which need presidential-by-district data that is not in these files. The notebook states that too.

## Data sources (all public and free)

- **Princeton gerrymetrics**, bundled congressional election results 1948 to 2018 and metric code: https://github.com/PrincetonUniversity/gerrymandertests
- **MIT Election Data + Science Lab / Harvard Dataverse**, U.S. House results 1976 to 2022 (TidyTuesday mirror) and 1976 to 2024 (Dataverse DOI 10.7910/DVN/IG0UN2, via a public mirror, see `BUILD_REPORT.md` for why and how it was cross-checked)
- **U.S. Census Bureau, TIGER/Line**, congressional district boundary shapefiles (1:20,000,000 cartographic boundary files, chosen to keep downloads small): https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2020.html
- **GerryChain**, for the ensemble test only: https://github.com/mggg/GerryChain, docs: https://gerrychain.readthedocs.io/en/v1.0.0/
- **OpenElections**, precinct-level results index: https://github.com/orgs/openelections/repositories

See `BUILD_REPORT.md` for exactly which files I used, what ran, and what (if anything) failed or was approximated.

## License and honesty note

All data used here is public. No numbers in this project are invented. Every chart is computed from the datasets above, and anything that could not be reproduced is documented in `BUILD_REPORT.md`.
