# Style guide: "Stone & Gold"

The Fluffy Moose theme is a nod to the old-school fantasy MMOs our group grew
up on: stone panels, gold accents and a pixel font on the menus. It's
deliberately toned down, with soft colours, thin bevels and no text shadows, so
it stays easy on the eyes through a whole film. It also makes the site cleaner
and easier to get around than stock Jellyfin.

The full visual handbook, with every option side by side, is here (the link
expires about February 2027):
<https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/mockups/f4e733f43f27fd6fc7fcdf2444b36959.html>

## Decisions

| Area | Choice | Status |
|---|---|---|
| Overall look | **A: Stone & Gold** | ✅ chosen |
| Navigation | **Side panel** with labelled icons. It becomes a bottom tab bar on phones, and replaces the hamburger menu and the top tabs. | ✅ chosen |
| Home page | **Big Resume card + 3 rows**. Empty rows are hidden, and each row gets "See all ›". | ✅ chosen |
| Poster cards | Bevelled frame with a gold focus glow | default (recommended) |
| Buttons | Stone panel with a thin top highlight, Noto Sans label | default (recommended) |
| Progress bar | Slim moss-green bar, with the label underneath it | default (recommended) |
| Extras | Level-up pop-up · right-click menu · loading screen · friends online | ⏳ choosing from screenshots |

## Palette

| Token | Hex | Use |
|---|---|---|
| Dungeon | `#1a1713` | Page background |
| Stone | `#2d2720` | Panels, top bar, side panel |
| Stone lit | `#3a3229` | Active and hover surfaces, buttons |
| Edge | `#4a4035` | Thin bevels and borders |
| Deep | `#13100c` | Inset fields (search box) |
| Gold | `#e2b65a` | Accent, active nav marker, focus glow |
| Ember | `#d99a5b` | Section and item titles |
| Bone | `#e9e1d0` | Body text |
| Muted | `#a99d87` | Secondary text |
| Moss | `#6aa05a` | Progress fill |
| Rust | `#b5473a` | Errors, delete |

Measured contrast: gold on stone 7.8:1, bone on dungeon 13.7:1, muted on stone
5.5:1 (4.7:1 on stone lit), ember on dungeon 7.4:1. All pass WCAG AA.
**Text never sits on the progress bar.**

## Type

| Role | Font | Rules |
|---|---|---|
| Headings, titles | Cinzel 700 | Headings only |
| Menu items, section labels, badges, pop-ups | Pixelify Sans 400/600 | 12px minimum. Never in paragraphs or on buttons. |
| Numbers | Noto Sans (automatic) | The pixel font's **5 looks like S and its 2 like 8**, so its `@font-face` leaves out digits (`unicode-range` skips U+0030–0039) and they fall back to Noto Sans. |
| Body, descriptions, settings, buttons | Noto Sans | Already bundled with Jellyfin, and covers every language |

All three fonts are under the SIL Open Font License and come from
`@fontsource` packages, so they're bundled with the app, not loaded from Google.

## Ground rules

- **Inspired by, never copied.** No logos, sprites, icons, sounds, fonts or
  names from any real game. This repo is public.
- **Readable first.** The pixel font is for short labels only.
- **Easy on the eyes.** No text shadows, no heavy black outlines, nothing
  brighter than the posters.
- **Works with a TV remote, a thumb and a mouse.** Every focusable thing gets
  the gold focus glow. Tap targets are at least 44px.
- **Easy to merge.** The theme lives in `src/themes/fluffymoose/`. Layout
  changes stay small and in as few Jellyfin files as possible (see
  [development.md](development.md)).

## Screenshots

Titles and episodes are real shows. Poster artwork is a colour placeholder,
because the real artwork is copyrighted and these images are public. On the
server, Jellyfin shows the real posters from its own metadata.

### Today (stock Jellyfin 12.4)

![Stock Jellyfin home screen](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/deb587865a086421d88d.png)

### Stone & Gold, desktop and phone

![Stone & Gold home screen](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/1b0e13a8713440c187d9.png)

![Stone & Gold on a phone](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/2d39445f829207b87295.png)

### Extras, without and with

![Level-up pop-up](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/4307e85117b19c1bfd10.png)

![Right-click menu](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/ec0f24246a1862fe19c8.png)

![Loading screen](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/e39ee2e9501b1df34801.png)

![Friends online](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/8f861963fba6b18289f0.png)

### Components

![Poster card options](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/014cb1b06c105ac0f098.png)

![Button options](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/ce03850015bd37180a04.png)

![Progress bar options](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/e45379d6a9fefbbeca36.png)
