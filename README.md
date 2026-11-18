# Dejadot — website

The landing page for **Dejadot**, a one-thumb arcade game for Android. Grab the coin in five seconds,
then do it again while every run you have made replays around you as a shadow. Touch one and it is
over.

The whole site is one file, `index.html`: no build step, no framework, no tracking.

**Download the app:** [latest release](https://github.com/julyamba/dejadot-page/releases/latest)

## What is on the page

| Section | What it shows |
|---|---|
| **Hero** | The pitch, a download button and a **playable demo** of Classic mode inside a phone frame. |
| **How it works** | Grab, Shadow, Survive: the three-step rule of the game. |
| **Shadow Draft** | The second mode: multiplier, coins that do not avoid shadows, curse drafts, and all 13 cards with their danger, multiplier change and rarity. |
| **Features** | Two modes, the daily challenge, 16 themes, stats and 15 achievements, close calls, sound and haptics, privacy, pause, steering and progress backup. |
| **Themes** | All 16 arena themes with their coin targets. Picking one recolours the whole page, demo included. |
| **FAQ** | Internet and accounts, ads, the daily challenge, losing while standing still, Shadow Draft, unlocking themes, backups, iPhone. |
| **Install** | How to download and install the APK. |

## The playable demo

The demo in the hero is a small JavaScript copy of the app's Classic mode, using the same rules and
numbers:

- a 100 × 150 arena, a 5-second round (300 steps at 60 Hz) and a short grace period at the start of each round;
- the same speed, collision distance and steering leash as the app;
- the same coin look: a spinning face that pops in with two rings.

With a mouse, the dot follows the cursor. On touch screens it steers relatively, like the app. The demo
pauses when it scrolls out of view or the tab is hidden, and it respects "reduce motion".

Shadow Draft is not playable on the page; its cards are described in their own section.

## Download button

The **Download the APK** button points to the
[latest release](https://github.com/julyamba/dejadot-page/releases/latest) of this repository. When the
page loads, it asks the GitHub API for that release and, if the release has an `.apk` file attached,
turns the button into a direct download link. If the API cannot be reached, the button still opens the
releases page.

### Publishing a new version

1. Build the release APK in the app project (`./gradlew :androidApp:assembleRelease`). It is written
   to `androidApp/build/outputs/apk/release/dejadot-<version>-release.apk`.
2. In this repository on GitHub, create a new release (for example tag `v1.0.14`).
3. Attach the `.apk` file to the release and publish it.

The page picks up the new APK on its own; nothing in `index.html` needs to change.

## Running it locally

Open `index.html` in a browser. Everything works from the file, except the download button's lookup
of the latest release, which needs an internet connection.

## Keeping the page in sync with the app

Some details are copied from the app by hand. When they change in the app, update them here too:

| On the page | In the app |
|---|---|
| `THEMES` list in the script (names, unlock coins, colours) | `Theme` in `core/.../Catalog.kt` |
| Demo constants (`W`, `H`, `R`, `SPEED`, `FRAMES`, `GRACE`, `LEASH`, ...) | `core/.../Rules.kt` |
| Shadow Draft cards (text, danger, multiplier, rarity) | `Card` in `core/.../Draft.kt` |
| Counts in the text: 16 themes, 15 achievements, 13 cards, Android 7.0+ | `Theme`, `Achievement`, `Card`, `minSdk` |

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole site: markup, styles and script. |
| `app-icon.png` | The app icon, used for the favicon, the share preview and the install section. |

## Notes

- **Fonts:** Bricolage Grotesque and JetBrains Mono, loaded from Google Fonts. Without them the page
  falls back to system fonts.
- **Saved in the visitor's browser:** the chosen theme (`dejadot-page-theme`) and the demo's best
  score (`echo-page-best`, an older name kept so returning visitors keep their best). Nothing else is
  stored and nothing is sent anywhere.
- **Accessibility:** keyboard focus outlines, `prefers-reduced-motion` support, and labels on the
  demo canvas and the theme buttons.
