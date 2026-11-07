<h1 align="center">
  <img src="kiro.jpg" alt="Kiro" width="220" />
  <br />
  Surfn Kiro
</h1>

![Last-Commit](https://img.shields.io/github/last-commit/kirodubes/surfn-kiro?style=for-the-badge)

<img alt="GitHub followers" src="https://img.shields.io/github/followers/erikdubois?style=flat">&nbsp;&nbsp;<img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/kirodubes/surfn-kiro">&nbsp;&nbsp;<img alt="GitHub forks" src="https://img.shields.io/github/forks/kirodubes/surfn-kiro">

<img alt="YouTube Channel Subscribers" src="https://img.shields.io/youtube/channel/subscribers/UCJdmdUp5BrsWsYVQUylCMLg">&nbsp;&nbsp;<img alt="YouTube Channel Views" src="https://img.shields.io/youtube/channel/views/UCJdmdUp5BrsWsYVQUylCMLg">

---

**Surfn Kiro** is [Surfn](https://github.com/erikdubois/surfn) tuned to read well on every desktop, light and
dark, with KDE Plasma as the hardest case. It keeps Surfn's colourful look: same folders, same apps, same
categories. What changes is the small stuff Plasma draws on its own:

- Monochrome glyphs (panel, tray, symbolic and small action icons) follow Plasma's text colour, so they
  stay visible on light and dark. GTK desktops get a neutral mid grey that reads on both.
- White pages (the Defaults button and friends) have a thin grey outline, so they do not vanish on light.
- The sidebar Places icons (Home, Documents, Downloads, ...) are lifted from dark grey to mid grey.
- Icons that Plasma could not find (and silently replaced with a pencil) now exist.
- Paper's blend filter, which made 42 device icons blank in Plasma, is gone.

Unlike the other Surfn variants, Surfn Kiro is a **full** theme: it does not inherit from Surfn and does not
need `surfn-icons-git`. KDE shortens a missing icon name inside the theme before it asks an inherited theme,
so a thin overlay would show wrong icons.

## Plasma global themes

The package also ships two Plasma global themes (System Settings → Colours & Themes → Global Theme):

- **Surfn Kiro Dark**: Breeze Dark with the Surfn Kiro icons and the light Breeze cursor.
- **Surfn Kiro Light**: Breeze Light with the Surfn Kiro icons and the dark Breeze cursor.

Both keep Breeze for everything else, take the accent colour from the wallpaper and use Plasma's stock
wallpaper, whichever one the installed Plasma ships.

## Installation (Arch / Kiro — nemesis_repo)

```bash
sudo pacman -S surfn-kiro-icons-git
```

## Manual

Copy `usr/share/icons/Surfn-Kiro` into `~/.icons` (or `~/.local/share/icons` on Plasma),
then select **Surfn Kiro** in your appearance settings.

## Credits

Built on Surfn by Erik Dubois, which itself blends Ultra Flat, Super Flat Remix, Yltra Flat, Numix (Circle)
and Paper icons. All credit to the original artists.

The 16, 22 and 24 px Places sidebar icons (Home, Desktop, Documents, Downloads, Trash, Network, Recent, ...) and
the panel and system tray icons (arrows, volume, battery, network, Bluetooth, brightness, devices, notifications,
KDE Connect, Vaults, ...) and the small button, toolbar and menu icons that were in colour (Add, Remove, Delete,
Install from File, Download, ...) are [Breeze icons](https://invent.kde.org/frameworks/breeze-icons) by the KDE Visual
Design Group, taken from breeze-icons 6.31.0; only their colour outside Plasma was changed to a mid grey.

## License

[LICENSE](./LICENSE) — Attribution-NonCommercial-ShareAlike 4.0 International, the same as Surfn.
Parts made by others keep their own licence. [LICENSE-breeze](./LICENSE-breeze) lists the Breeze icons Surfn Kiro
added; [LICENSE-third-party](./LICENSE-third-party) lists every other file that is identical to another icon theme:

- [Breeze](https://invent.kde.org/frameworks/breeze-icons) by the KDE Visual Design Group: LGPL-3.0-or-later.
- [Numix](https://github.com/numixproject/numix-icon-theme) and
  [Numix Circle](https://github.com/numixproject/numix-icon-theme-circle) by the Numix Project: GPL-3.0.
  Numix is also the first theme Surfn Kiro falls back to for an icon it does not have.
- [Papirus](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme): GPL-3.0.
- [Paper](https://github.com/snwh/paper-icon-theme) by Sam Hewitt: CC BY-SA 4.0.
- [Ultra Flat](https://github.com/Ultra-Flat-Icons/Ultra-Flat-Icons) by Steftrikia: CC BY-NC-SA 4.0.
- [Flattr](https://github.com/NitruxSA/flattr-icons) by Uri Herrera: CC BY-NC-SA 4.0.
- [Super Flat Remix](https://github.com/daniruiz/Super-Flat-Remix) by Daniel Ruiz de Alegría: CC BY-NC-SA 4.0
  (one icon).
- [Flat Remix](https://github.com/daniruiz/flat-remix) by Daniel Ruiz de Alegría: GPL-3.0 (one icon).

Recoloured or edited icons no longer match a source byte for byte, so the list is a minimum.
