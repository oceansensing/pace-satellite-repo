# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-09-30 — Its own repository, set up before its data

NASA's PACE products get a repository of their own (the owner, 2026-09-30), set up with its documents and publish workflow and publishing nothing until its source is chosen.

## D2 — 2026-10-14 — NASA's own archive, by OPeNDAP

The source is NASA's ocean color archive, OB.DAAC: the catalog (CMR) for which days exist and OPeNDAP for
the values, which needs no login. Not NASA Worldview, the candidate named at D1: its PACE layers are
rendered pictures, not values a reader can read back.

## D3 — 2026-10-14 — Each quantity a day and an 8-day mean, one product a NASA suite

Every quantity of the OCI ocean color and atmosphere suites, one map each, at NASA's 4 km grid (0.1 degree
where NASA makes nothing finer, the aerosols): its newest day, and the mean of each cell's clear days over
the eight newest, each day counted once. One product per NASA suite, ten in all, 44 roots. A quantity at
one wavelength names its band in its root (`kd490-pace`) and its header (`wavelength`), so the spectrum's
other bands join without a rename.

## D4 — 2026-10-14 — Published to R2 alone

Every product is `r2_only` (the site pipeline's D13, its note of 2026-10-09): the roots and tiles go to the
second host only, the status to Pages beside the other origins'.
