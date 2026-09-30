# pace-satellite-repo

NASA's **PACE** satellite products: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Nothing to publish yet**: its upstream is not live (see PLAN). `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

Nothing yet. Set up on 2026-09-30, ahead of a layer from NASA's PACE mission; what it publishes follows when its source is chosen.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

To be chosen. NASA Worldview (`https://worldview.earthdata.nasa.gov`) is among the candidates named on 2026-09-30.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `orb-satellite-pace-repo` (the ORB lab's PACE products) and `viirs-satellite-repo`, set up the same day.

**Which document gets what, and what "update docs" means across all
twenty-four repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all twenty-four, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
