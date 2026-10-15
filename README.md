# pace-satellite-repo

NASA's **PACE** satellite products: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and no code of its own.

`PLAN.md` is the founding plan and running record; `CLAUDE.md` carries what must not be got wrong and the
shared doc doctrine.

## What it publishes

The ocean color and atmosphere suites of PACE's Ocean Color Instrument (OCI), **each quantity as its newest
day and as the mean of each cell's clear days over the eight newest days**, on NASA's 4 km grid (0.1 degree
for the aerosols, the finest NASA maps them at). Twenty-two quantities, 44 roots, each a coarse overview
pointing at its tiles at full resolution:

| Product | Quantities (root stems) | Grid |
| --- | --- | --- |
| `pace-bgc` | chlorophyll-a (`chl`), phytoplankton carbon (`phytoc`), particulate organic and inorganic carbon (`poc`, `pic`) | 4 km |
| `pace-moana` | Prochlorococcus, Synechococcus and picoeukaryote counts (`pro`, `syn`, `peuk`) | 4 km, the Atlantic |
| `pace-npp` | net primary production, CAFE (`npp`) | 4 km |
| `pace-aop` | normalized fluorescence line height (`nflh`) | 4 km |
| `pace-kd` | diffuse attenuation at 490 nm (`kd490`) | 4 km |
| `pace-par` | photosynthetically available radiation (`par`) | 4 km |
| `pace-iop` | CDOM and detritus absorption, phytoplankton absorption, particle backscatter at 442 nm (`adg442`, `aph442`, `bbp442`) | 4 km |
| `pace-aer` | aerosol optical depth at 550 nm, UV aerosol index (`aod550`, `uvai`) | 0.1 degree |
| `pace-trgas` | total ozone, total nitrogen dioxide (`o3`, `no2`) | 4 km |
| `pace-cloud` | cloud cover, top height, optical thickness, particle size (`cloud`, `cth`, `cot`, `cer`) | 4 km |

Each stem is two roots: `<stem>-pace.json`, the day, and `<stem>-pace-8d.json`, the 8-day mean, each with
its tiles in `tiles-<root>/`. A quantity read at one wavelength names its band in its stem and in its
header (`wavelength`, nanometers).

**Published to Cloudflare R2 alone** (`r2_only` in `pipeline/products.toml`): the roots and tiles go to the
second host, and Pages carries this repository's `status/status.json`. Nothing here is drawn on the website's
map; the map's status line still reports these products when they fall behind.

## Where the data comes from

NASA's Ocean Biology Distributed Active Archive Center (OB.DAAC): its catalog (CMR) says which daily
near-real-time files exist, and its OPeNDAP server answers a subset of each file without a login. Only daily
near-real-time files exist, so the 8-day mean is made here. NASA's data use guidance places mission data
under CC0 and asks that it be cited: NASA OB.DAAC, PACE OCI, near-real-time, at the version each header's
`stream` names.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetcher (`scripts/fetch-pace.py`) and the
published-file contract all come from `oceansensing.github.io`, checked out at run time. This repository
carries `pipeline/products.toml`, its publish workflow and a daily cache sweep, and nothing else executable.
Related repositories: `orb-satellite-pace-repo` (the ORB lab's PACE products) and `viirs-satellite-repo`,
set up the same day.

**Which document gets what, and what "update docs" means across all
twenty-five repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all twenty-five, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow and the daily cache sweep
```
