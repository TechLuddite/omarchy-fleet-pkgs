# This is a fork

This repository mirrors `omacom/omarchy-pkgs` and will carry the package recipe for the Omarchy Fleet work. It is not a GitHub fork, so `upstream` has to be added by hand:

```bash
git remote add upstream https://github.com/omacom/omarchy-pkgs.git
```

Two branches matter and they have different rules.

- `master` is a pure mirror of upstream. **Never commit to it.** It is only ever fast-forwarded from `upstream/master`, which is what makes `git log master..fleet-main` the exact answer to what this fork has changed.
- `fleet-main` is the default branch and where every change lands. Branch from it, pull request into it.

```bash
git fetch upstream
git push origin upstream/master:master
```

Upstream moves fast here. Within a day of mirroring, `master` was twenty-one commits ahead. Sync before any rebase rather than after.

The runtime repository is the sibling checkout `../omarchy-fleet`, mirroring `omacom/omarchy`. Its `agents/skills/fleet.md` carries the fleet design and is worth reading before changing anything here.

## What this fork has changed

Nothing yet beyond its own governance files. This repository exists because the ISO builder builds each package from `/omarchy-pkgs/pkgbuilds/<name>`, so a fleet package has nowhere to live without it.

## What is coming

A recipe at `pkgbuilds/omarchy-fleet/`, with a `PKGBUILD` and a `.omarchy/package.json` in the shape every other package here uses. It takes its source from the mounted runtime checkout through `OMARCHY_SRC`, the way `omarchy-dev` does.

The ISO side is already prepared for it. `builder/build-iso.sh` in the ISO fork publishes one list of Omarchy packages with an append point, so shipping this one is `OMARCHY_EXTRA_PACKAGES=omarchy-fleet` on the build rather than an edit in four places.

## Repository settings that are deliberate

GitHub Actions is disabled for this repository. Upstream ships four workflows here, three of which are maintainer cron jobs on six-hour schedules that sync AUR, rebuild triggers and upstream releases. On a mirror they would run every six hours, expect credentials and a publishing role this repository does not have, and fail or do something unwanted. Re-enable Actions only after deciding which of those four should exist here, and switch the three cron jobs off individually rather than turning everything on.

Anything committed here has to stand on its own for a reader who has never seen this project's internal notes. No shorthand reference codes, no internal host names, no pointers to private records.
