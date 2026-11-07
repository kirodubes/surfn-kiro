# Changelog

## 2026.11.07 — The leave screen in white

### What Changed

- The Plasma leave screen showed Log Out as Surfn's green disc (and Shut Down as its red one) next to a white Cancel.
  Every button there (Log Out, Restart, Shut Down, Sleep, Hibernate) is now Breeze's monochrome line icon, white on
  dark and dark on light, like Cancel.
- The user picture on the leave screen (when no face is set) was Surfn's orange avatar; it is now Breeze's line
  person in the same white.
- Variety's tray icon was the colourful Variety app icon on Plasma; it is now a monochrome line icon (Surfn-Plasma's
  art), white on dark and dark on light.

### Technical Details

- The greeter asks for `iconSizes.huge` (64 px). Two things gave it Surfn's colour art:
  - `actions/32` and `actions/scalable` of `system-log-out` / `system-shutdown`: step 9 only swapped names Surfn drew
    in colour at small sizes. `system-log-out`, `system-reboot`, `system-shutdown`, `system-suspend` and
    `system-suspend-hibernate` are now in `_src/breeze-actions` (Breeze files + `NAMES.txt`): Breeze's 16-32 px.
  - Surfn's app icons of the same names (`apps/scalable`, Size 48) beat Breeze's `actions/32` at 64 px. New step 10
    (`_src/accent/make_leave_screen.py`) moves them to `<name>-surfn.svg`; the icons linking to them keep their art
    (`reboot`, `view-refresh`, `xfpm-suspend`, ...).
- Aliases keep Surfn's art where Breeze has no file of that size (`application-exit`, `gtk-quit`, ... at 16 px and
  scalable) through `system-shutdown-surfn.svg`; `system-logout.svg` (Surfn's own name) stays as it was.
- The avatar is `user-identity` at 64 px, found in `apps/scalable` (a link to Surfn's `user.svg`). Step 10 now
  writes `_src/leave/user-identity.svg` there (Breeze's 24 px line person, SVG so it scales); the other names
  linking to `user.svg` keep Surfn's orange.
- `LICENSE-breeze`: 35 files added (3,320).
- Variety asks `variety-indicator` (`-dark` with the Dark option). Surfn keeps those in `panel/`, and KDE skips
  folders with `Context=Panel`: KIconLoader then drops the last part of the name and shows `variety`. New step 11
  writes `_src/tray/variety-indicator.svg` (`ColorScheme-Text`, fallback `#8c939d`) as both names in
  `status/symbolic`. GTK still sees the `panel/` copies too.

### Files Modified

- `usr/share/icons/Surfn-Kiro/actions/*/system-{log-out,reboot,shutdown,suspend,suspend-hibernate}.svg`
- `usr/share/icons/Surfn-Kiro/{actions,apps}/*/system-*-surfn.svg` (new) and the aliases linking to them
- `usr/share/icons/Surfn-Kiro/status/symbolic/variety-indicator{,-dark}.svg` (new)
- `usr/share/icons/Surfn-Kiro/apps/scalable/user-identity.svg` (link to `user.svg` -> Breeze file)
- `LICENSE-breeze`
- `CHANGELOG.md`

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
  - **The Places sidebar uses Breeze's monochrome line icons** (Home, Desktop, Documents, Downloads, Trash,
    Network, Recent, ...): dark on light, white on dark. The folders in the file view stay Surfn's, in colour.
  - **The panel and system tray use Breeze's monochrome icons too**: a thin up arrow instead of the heavy triangle,
    a line disc for devices, a line desktop for Show Desktop, and Breeze's volume, battery, network, Bluetooth,
    brightness, KDE Connect and Vaults icons.
  - **Buttons, toolbars and menus are monochrome**: the 283 action icons Surfn drew in colour (green Add, coloured
    Install from File and Download, red Remove and Delete, ...) use Breeze's line icons at 16 to 32 px.
    Delete keeps Breeze's red, as Breeze marks destructive actions.
  - The README's licence notes name every source that keeps its own licence: Breeze, Numix and Numix Circle,
    Papirus and Paper. New `LICENSE-third-party` lists 2,411 files by source.
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
  Previews taken in a Plasma VM over the stock wallpaper (Hanabi), with the accent folders.
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
- Places sidebar: Breeze's 16/22/24 px icons for 17 Places names (breeze-icons 6.31.0, LGPL-3.0-or-later, listed
  in `LICENSE-breeze`), GTK fallback colour `#8c939d`. Their bigger sizes became SVG wraps of Surfn's art (the
  PNG-first rule). Same-name SVGs in other contexts (`document-open-recent` in actions/apps, `network-workgroup`
  in apps/devices) moved to private names (`...-surfn-<context>.svg`) so they no longer beat the Places icon;
  the icons that linked to them keep their art.
- Panel and tray: step 8 swaps 270 `-symbolic` names (the tray asks `-symbolic` first; found by tracing
  plasmashell's icon lookups) for Breeze's: arrows, audio, microphone, battery, network (incl. Bluetooth and Wi-Fi
  levels), notifications, brightness, night light, optical media, drives, keyboard indicators, KDE Connect, Vaults,
  updates, camera, printer, clipboard, display. Breeze files kept in `_src/breeze-panel`; Surfn's own copies of
  those names are removed, or kept under `<name>-surfn.svg` where other icons link to them (6 Bluetooth files).
  `LICENSE-breeze` lists all 1,407 Breeze files.
- Buttons/toolbars: step 9 swaps the 283 colourful action names that Breeze has in monochrome (only the actions
  context, so app icons of the same name stay Surfn's; names in `_src/breeze-actions/NAMES.txt`). Aliases follow
  to Breeze in their own folder (`add` -> `list-add`, also Surfn's 24 -> 24@2x links); links from other contexts
  and Breeze-less large sizes keep Surfn's art as `<name>-surfn.svg` (98 files). 375 colourful action names have
  no Breeze counterpart and stay colourful. `LICENSE-breeze` now lists 3,285 files.
- `LICENSE-third-party`: every real file compared with the installed icon themes (byte-identical copies) plus
  Paper's author's export path in the SVGs (`_src/third_party.py`). Recoloured icons no longer match: a minimum.
- The build is deterministic now: when two colours tie for an icon's GTK fallback, the first one in the file wins
  (it was Python's set order, so two `status` icons changed grey once more).
- Known gap: applying the global theme sets the icons for KDE apps, but GTK apps keep the previous icon theme
  until the icons are picked once under Icons (or `plasma-changeicons Surfn-Kiro`). Breeze's own themes do sync.
- Build scripts are kept locally in `_src/` (not published): the build reruns from a Surfn tree.

### Files Modified

- `usr/share/icons/Surfn-Kiro/` (new theme, based on Surfn 26.11.06)
- `usr/share/plasma/look-and-feel/Surfn-Kiro-Dark/`, `Surfn-Kiro-Light/` (new)
- `LICENSE-breeze` (new)
- `README.md`, `CHANGELOG.md`, `LICENSE`, `setup.sh`, `up.sh`, `kiro.jpg`, `.gitignore`
