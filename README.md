# mirage-vault-card-data

This repo hosts nothing but versioned data releases: no source code, no
build tooling, nothing you'd `git clone` and run. It exists purely so
that trading card identity data (name, set, artist, rarity, image, etc.)
can be fetched **publicly and without authentication** by the tools that
consume it.

## Why a separate repo

The tooling that produces this data (backfill scripts, validation,
release packaging, a desktop GUI with a "Check for Updates" flow) lives
in a companion repository that is intentionally private. That tool makes
an unauthenticated request to the GitHub Releases API to check for and
download new data - which only works against a *public* repo. Splitting
the data out here keeps the data openly and reliably fetchable while
keeping the tooling's source private.

## What's here

Nothing but GitHub Releases. Each release is tagged `vX.Y.Z` and carries:

- `cards.json` - the card identity dataset for that version
- `images_part001.tar` ... `images_partNNN.tar` - card images, packed
  into shards
- `manifest.json` - filename -> shard index for the image shards
- `data_release.json` - a small manifest (version, publish timestamp,
  record/image counts, and a sha256 of every other asset) used to verify
  a download completed correctly and to detect whether a newer release
  is available

See the [Releases page](https://github.com/MyKale92/mirage-vault-card-data/releases)
for the current and past versions.

## Licensing & attribution

This data is **not** covered by an open-source code license (there's no
code here). Card names, artwork, and images remain the property of their
original rights holders (e.g., for Pokemon: The Pokémon Company,
Nintendo, Game Freak, Creatures, and Wizards of the Coast). Some fields
are sourced in part from Bulbapedia and are subject to its CC BY-NC-SA
terms. This repo does not grant any rights beyond what those sources
already permit - it's a distribution convenience, not a relicensing.

## Scope

Currently Pokemon TCG only. The naming here is intentionally generic
("card-data" rather than "pokemon-card-data") since this may expand to
cover other trading card games later; each game's data would still ship
as clearly labeled, separately identifiable assets within a release.
