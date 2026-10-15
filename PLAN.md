# pace-satellite-repo: the founding plan and running record

NASA's **PACE** satellite products. Created on GitHub by the owner on 2026-09-30 and given its documents by
the site's `pipeline/scaffold/new-origin.py`; its source and products chosen on 2026-10-14.

## What it is for

PACE's Ocean Color Instrument suites, ocean color and atmosphere, each quantity as its newest day and as an
8-day mean of each cell's clear days (`README.md` has the table). Published to R2 alone.

## Where the data comes from, measured 2026-10-14

- **NASA's ocean color archive (OB.DAAC), by OPeNDAP, no login.** A whole-globe 4 km grid of one variable
  answers in 4.7 s (chlorophyll, 13.9 MB) to 8.1 s (cloud fraction, 44 MB, out of a 2.9 GB file). The
  whole-file downloads ask for an Earthdata account; the subsets do not.
- **Which days exist comes from NASA's catalog (CMR)**, which is public: 133 PACE collections, of which the
  near-real-time `_NRT` level-3 and level-4 daily files are what this repository reads.
- **Only daily near-real-time files.** No 8-day or monthly near-real-time product exists; the
  science-quality versions lag about a month (the newest on 2026-10-14 was 2026-08-31's, posted
  2026-09-30). So the 8-day mean is computed here, from the eight newest days the catalog lists.
- **When a day arrives**, from the catalog's own `updated` times, 2026-10-08 to 14: BGC, KD, IOP, AOP,
  AER_UAA and CLOUD post day D at D+1 13:18-16:24 UTC; MOANA 15:18-18:18; TRGAS 21:37-21:54; PAR at D+2
  13:25-13:34; NPP at D+2 16:00 to D+3 00:27. The budgets in `products.toml` are these, plus the
  schedule's two hours and a missed day.
- **Coverage.** One day held a value in 9.7% of the 4 km grid's cells (2026-10-13, chlorophyll: clouds and
  the gaps between swaths); eight days in 36%.
- **Size.** A quantity is about 280 MB (its day and its 8-day mean, tiles and overview), 30 MB for the
  0.1 degree aerosols; about 5.5 GB for all 22 (measured by a full local build, 2026-10-14). A day's build
  of every product took about six minutes of fetching locally.

## The traps, each found by a request

The fetcher's docstring has them with their measurements: the constraint's brackets percent-encoded; a
subset's coordinate variables come back as zeros, so the axes are read by their own request; packed
integers are scaled by the fetcher; MOANA's counts carry -2147483648 beside a declared fill of -32767;
retrievals outside NASA's own valid range are in the files and are dropped.

## The spectrum, kept open

The 172-band remote-sensing reflectance is not published. One band by OPeNDAP took 45 s (wavelength is the
file's fastest axis), so the spectrum would come from the whole files (843 MB a day, an Earthdata login), and
172 maps of the kind published here would be about 70 GB: a spectrum needs a packed file per tile holding
every band, a new kind in the contract. A quantity at one wavelength already names its band, so other bands
of Kd, absorption and backscatter join as roots of their own.

## 2026-10-15: the first run, and the schedule

The secrets set (the deploy key and the two R2 secrets shared), then the dispatched run 38680413668:
green, every product `fresh` — day 2026-10-13 (PAR and NPP 10-12), all 44 roots. The build job took 12
minutes, its fetch-and-assemble step 9 (the cloud suite the longest, 3), the ten tile caches saved; the
R2 job uploaded 18,315 files in 15 minutes, the bucket then equal to the build. Pages carries the status
alone, its products R2's (`products: {}` there, as every product is `r2_only`). **Scheduled since**,
every two hours at 41 past.

## Open

1. A week of scheduled runs, read: the budgets against NASA's real posting times, the caches' size.
