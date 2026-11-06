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
  - Two **Plasma global themes**, **Surfn Kiro Dark** and **Surfn Kiro Light**: Breeze Dark / Breeze Light with
    the Surfn Kiro icons, the light / dark Breeze cursor, the accent colour from the wallpaper and Plasma's stock
    wallpaper.
  - **Folders follow Plasma's accent colour.** With the accent taken from the wallpaper they match every
    wallpaper; GTK desktops keep Surfn's blue.
  - **Public** shows its share glyph in Dolphin, and **Projects** has a new `</>` folder (GTK file managers).
  - Dolphin's **Recent Locations** has its own icon, a folder with a clock, instead of a plain blue folder.

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
- `folder-open-recent` did not exist in Surfn. At 16/22/24 px a new glyph is drawn in the Places style (folder +
  clock); `folder-recent` cannot be reused there because at those sizes it is the bare clock of Recent Files.
  32 px and up link to `folder-recent`, which already is a folder with a clock. Checked in Dolphin, light and dark.
- Global themes in `usr/share/plasma/look-and-feel/Surfn-Kiro-{Dark,Light}`: only `metadata.json`, a `defaults`
  file and previews. Everything they do not define (panel layout, lock screen, splash) comes from Breeze, so they
  follow Plasma updates. `[Wallpaper] Image=Next` is Plasma's own default wallpaper package, replaced each release.
  Previews taken in a Plasma VM over the stock wallpaper.
- Accent folders: every raster folder (13 names, 9 sizes) became an SVG per size, pixel-exact. The folder body is one
  vector path with `class="ColorScheme-Accent"` (style fallback `#6ba4e7`, Surfn's blue, what GTK draws); glyph,
  paper and outline sit on top as an embedded PNG, the darker blues turned into black at the matching strength so
  they darken any accent. KDE takes any `.png` size before any `.svg`, so a converted name is SVG at every size: the
  small Places glyphs are wrapped unchanged, otherwise Dolphin scaled the 16 px glyph up instead of the folder.
- With places/ in SVG, a same-name SVG in another scalable dir ties and can win. `document-open`,
  `document-open-recent`, `folder-new`, `system-file-manager` and `org.gnome.Nautilus` stay real PNGs in places/ so
  they look as before; the app alias `apps/scalable/folder-templates.svg` is removed (it hid the Templates folder).
- `folder-public` added (the name KIO asks for, Surfn only had GTK's `folder-publicshare`); `folder-projects` drawn
  new. KIO has no icon name for XDG Projects, so Dolphin still shows a plain folder there.
- The build is deterministic now: when two colours tie for an icon's GTK fallback, the first one in the file wins
  (it was Python's set order, so two `status` icons changed grey once more).
- Known gap: applying the global theme sets the icons for KDE apps, but GTK apps keep the previous icon theme
  until the icons are picked once under Icons (or `plasma-changeicons Surfn-Kiro`). Breeze's own themes do sync.
- Build scripts are kept locally in `_src/` (not published): the build reruns from a Surfn tree.

### Files Modified

- `usr/share/icons/Surfn-Kiro/` (new theme, based on Surfn 26.11.06)
- `usr/share/plasma/look-and-feel/Surfn-Kiro-Dark/`, `Surfn-Kiro-Light/` (new)
- `README.md`, `CHANGELOG.md`, `LICENSE`, `setup.sh`, `up.sh`, `kiro.jpg`, `.gitignore`
