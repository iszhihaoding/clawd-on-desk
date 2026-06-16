# Clawd Codex Pet Development Notes

This file summarizes the context from Codex thread
`codex://threads/019eb031-caba-7d73-beed-6eb36c665e0d`.

The deep link originally provided in the new thread missed the last `d`.
The readable thread title is about the pixel crab pet.

## Current Goal

Continue development of a Codex desktop custom pet based on the original
`Clawd on Desk` pixel crab, while keeping only one final pet package.

The user preference from the previous thread:

- Keep one pet, not multiple variants.
- Preserve the original Clawd feel where possible.
- Balance visual quality with the strict Codex pet atlas format.
- Avoid over-busy failure or work animations when a cleaner original animation
  communicates the state well enough.

## Current Installed Pet

Installed path:

```text
C:\Users\hp\.codex\pets\clawd
```

Important files in the installed package:

```text
C:\Users\hp\.codex\pets\clawd\pet.json
C:\Users\hp\.codex\pets\clawd\spritesheet.webp
C:\Users\hp\.codex\pets\clawd\validation.json
C:\Users\hp\.codex\pets\clawd\contact-sheet.png
C:\Users\hp\.codex\pets\clawd\contact-sheet-final-integrated.png
C:\Users\hp\.codex\pets\clawd\ATTRIBUTION.txt
C:\Users\hp\.codex\pets\clawd\LICENSE
```

`pet.json` currently says:

```json
{
  "id": "clawd",
  "displayName": "Clawd",
  "description": "The original flat pixel crab, adapted from Clawd on Desk for Codex pets.",
  "spritesheetPath": "spritesheet.webp"
}
```

## Source And Build Script

Local source/build workspace used in the previous thread:

```text
C:\Users\hp\Downloads\clawd-on-desk-source
```

Current build script:

```text
C:\Users\hp\Downloads\clawd-on-desk-source\tools\build_codex_clawd_pet.py
```

The script was updated in the prior thread to generate the final integrated
single-pet version, then overwrite the installed Codex pet package.

Source attribution in the installed package:

```text
Source: https://github.com/rullerzhou-afk/clawd-on-desk
Source revision: 10f4cd1b619639d9f5a2f97b972a095db84de574
Original theme author: rullerzhou
License: GNU Affero General Public License v3.0
```

Important note: an externally supplied `clawd-codex-pet-v2.zip` claimed MIT in
its attribution, but the checked source repository license was AGPL-3.0. Do not
reuse the MIT claim.

## Codex Pet Format

Codex custom pets use a fixed 8-column by 9-row spritesheet.

Current validated atlas:

```text
file: C:\Users\hp\.codex\pets\clawd\spritesheet.webp
format: WEBP
mode: RGBA
width: 1536
height: 1872
transparent_rgb_residue_pixels: 0
errors: []
warnings: []
```

Each cell is therefore:

```text
192 x 208 px
```

Codex rows are fixed in this order:

```text
0 idle
1 running-right
2 running-left
3 waving
4 jumping
5 failed
6 waiting
7 running
8 review
```

Codex pet packages are static. They can show state animations, but they cannot
render Codex desktop conversation text, task names, or message bubbles. The
message bubble UI belongs to Codex desktop itself, not the pet package.

## Final State Mapping

The previous thread ended with a confirmed "single pet final integrated" mapping:

| Codex state | Original Clawd animation | Reason |
|---|---|---|
| `idle` | `clawd-idle-follow.svg` | Original quiet default idle; avoids constant looking around. |
| `running-right` | `clawd-react-drag.svg` | Best original reaction for drag/move behavior. |
| `running-left` | mirrored `clawd-react-drag.svg` | Codex needs a separate left-moving row. |
| `waving` | `clawd-happy.svg` | Closest available original animation for greeting/positive feedback. |
| `jumping` | `clawd-react-double-jump.svg` | Best match for jump feedback. |
| `failed` | `clawd-react-annoyed.svg` | Cleaner than `clawd-error.svg`; avoids noisy ERROR text/smoke. |
| `waiting` | `clawd-notification.svg` | Notification/light-bulb style wait state. |
| `running` | `clawd-working-typing.svg` | Represents Codex actively working. |
| `review` | `clawd-idle-reading.svg` | Best match for review/reading output. |

Earlier balanced versions used `clawd-idle-look.svg` for `idle` and
`clawd-react-left.svg` for `waiting`. The user later confirmed replacing them
with `clawd-idle-follow.svg` and `clawd-notification.svg`.

## Visual And Behavior Decisions

- `running` in Codex means "agent/task is running", not physical running.
- The crab typing animation is therefore correct for `running`.
- If the pet starts typing and later looks idle, that is a Codex state switch
  from `running` back to `idle`, not a broken `running` row.
- The original Clawd has random/occasional idle animations, but Codex pet format
  has no random idle mechanism. Extra original animations can only be mapped to
  one of the 9 rows or baked into a fixed loop.
- Mini mode assets from Clawd on Desk were intentionally not integrated because
  they do not fit Codex pet semantics well.
- The package keeps an upward placement adjustment from earlier work to avoid
  bottom-heavy frames and awkward bubble spacing.

## Rejected Package

The thread reviewed:

```text
C:\Users\hp\Downloads\clawd-codex-pet-v2.zip
```

It was not recommended for direct installation because:

- `spritesheet.webp` had transparent RGB residue.
- Many frames touched the bottom of the cell.
- The crab was visually too large compared with the preferred balanced version.
- Several state mappings were semantically weaker.
- Attribution incorrectly claimed MIT while the checked source license was
  AGPL-3.0.

## Current Validation Summary

The installed `validation.json` currently reports:

```text
ok: true
transparent_rgb_residue_pixels: 0
errors: []
warnings: []
```

All 9 rows have usable non-transparent frames. Some rows intentionally use fewer
than 8 frames and leave later cells empty.

## Next Development Steps

If development continues in this new workspace, first copy or move the actual
source project into:

```text
D:\dingzhihao\Codex\clawd-on-desk
```

The current workspace was empty when this note was written.

Suggested next actions:

1. Bring over `C:\Users\hp\Downloads\clawd-on-desk-source`.
2. Keep `tools\build_codex_clawd_pet.py` as the source of truth for generation.
3. Preserve the final mapping above unless the user explicitly asks to change a
   specific state.
4. Regenerate `spritesheet.webp`, `contact-sheet.png`, and `validation.json`.
5. Install to `C:\Users\hp\.codex\pets\clawd`.
6. Restart Codex desktop to see the new pet.

## Preview

Current final contact sheet:

```text
C:\Users\hp\.codex\pets\clawd\contact-sheet-final-integrated.png
```
