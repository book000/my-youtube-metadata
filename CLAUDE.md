# CLAUDE.md

## Purpose

This repository is a **data-only** store. It holds a single file, `tracks.json`,
which maps YouTube video IDs to music track metadata (title, artist, and
optional album information). It contains no application source code, build
system, or tests. The file is maintained by an external automation that pushes
commits titled `Update tracks.json`; manual edits are the exception.

## Repository layout

- `tracks.json` — the entire dataset. A single JSON object keyed by YouTube
  video ID.

There are no other tracked files (no source, no CI workflows, no README).

## Data format (`tracks.json`)

A JSON object. Each key is a YouTube video ID and each value is an object with
exactly these four fields:

```json
{
  "dQw4w9WgXcQ": {
    "track": "Song title",
    "artist": "Artist name",
    "album": null,
    "albumArtist": null
  }
}
```

- `track` (string): song title. Always present.
- `artist` (string or null): performer(s); multiple artists are comma-separated
  (e.g. `"猫又おかゆ,戌神ころね"`). Occasionally null.
- `album` (string or null): album name. Currently null for every entry.
- `albumArtist` (string or null): album artist. Almost always null.

Keep all four fields on every entry even when a value is null, so the schema
stays uniform. Video-ID keys are normally 11 characters (`[A-Za-z0-9_-]`).

## Working conventions

- Preserve the existing formatting: 2-space indentation, keys in their current
  order (the file is **not** sorted, so do not reorder it).
- Do not add or remove fields on entries; only fill in values.
- After any manual edit, verify the file still parses as JSON, e.g.
  `python3 -c "import json; json.load(open('tracks.json'))"`.

## No build / test / lint

There is nothing to build, test, or lint in this repository. "Verification"
means confirming `tracks.json` is valid JSON and each entry keeps the four-field
schema described above.

## Documentation update rules

If the data schema of `tracks.json` changes (new field, key format change),
update the "Data format" section above in the same change.
