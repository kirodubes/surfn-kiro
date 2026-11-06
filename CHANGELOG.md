# Changelog

## 2026.11.06 — Surfn Kiro: Surfn tuned for Plasma light and dark

### What Changed

- New icon theme branched from Surfn (tag 26.11.06). Surfn itself stays as it is; the Plasma work goes here.
- A full crawl of System Settings (100 modules, two levels deep), Kickoff, the tray and Dolphin in a Plasma VM,
  in light and dark, found icons that vanish on one of the two. This first release fixes the main ones:
  - Monochrome glyphs (panel, tray, symbolic and small action icons) now follow Plasma's text colour.
  - The Defaults button's white page has a grey outline (about 60 settings pages).
  - Dolphin's Places icons are mid grey instead of dark grey, readable on dark.
  - `edit-none` exists, so empty pages (Bluetooth, Splash Screen "None", ...) no longer show a pencil.
  - The System Sounds play button, the tray disc and show-desktop icons and the panel launcher show on light.

### Technical Details

- Plasma recolours an SVG only with `fill="currentColor"` + `class="ColorScheme-Text"` and a
  `current-color-scheme` style block. Neutral greys in symbolic, panel and monochrome status/action icons were
  switched to that hook. The style block's fallback colour is what GTK desktops draw: the original colour for
  panel icons, mid grey `#8c939d` for small action icons.
- Icons with light and dark greys together (white letters on a grey badge) are left as drawn: one colour would
  erase the detail (718 skipped).
- QtSvg drops any group with a `filter:url(#...)`: Paper's no-op feBlend filter was stripped from 229 icons.
- KDE tries every `.png` size before any `.svg`, so the Places PNGs stay PNG: dark-grey 16/22/24 glyphs are
  lifted to mid grey with their alpha normalised, keeping Surfn's art.
- Page borders: a grey copy of the white page drawn underneath (QtSvg ignores `clipPath`, which drew a black page).
- Full theme, not an overlay: KDE trims a missing name inside the theme (`edit-none` → `edit`) before it asks an
  inherited theme.
- Build scripts are kept locally in `_src/` (not published): the build reruns from a Surfn tree.

### Files Modified

- `usr/share/icons/Surfn-Kiro/` (new theme, based on Surfn 26.11.06)
- `README.md`, `CHANGELOG.md`, `LICENSE`, `setup.sh`, `up.sh`, `kiro.jpg`, `.gitignore`
