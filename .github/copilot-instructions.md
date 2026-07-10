# Copilot code review instructions

This repository is a data-only store. Its single tracked file, `tracks.json`,
maps YouTube video IDs to music track metadata. There is no application source
code, so reviews concern the data file itself.

## What to check in `tracks.json`

- The file must remain valid JSON (a single top-level object).
- Every value object must keep exactly these four fields: `track`, `artist`,
  `album`, `albumArtist`. Flag added or removed fields.
- `track` should be a non-empty string. `artist`, `album`, and `albumArtist`
  may be a string or `null`.
- Keys should be YouTube video IDs: normally 11 characters from
  `[A-Za-z0-9_-]`. Flag keys that clearly deviate from this shape.
- Watch for duplicate keys within the object.
- Preserve the existing 2-space indentation and formatting.

## What NOT to flag

- Existing entries whose `album` / `albumArtist` are `null` — this is the norm,
  not a defect.
- The current key ordering. The file is not sorted; do not request
  reordering entries.
- Non-ASCII values (Japanese titles/artist names are expected and correct).
- Comma-separated `artist` values (e.g. `"A,B"`) — this is the intended way to
  list multiple performers.
