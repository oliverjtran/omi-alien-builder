# Omi Alien Builder

A single-file web app for designing your own alien hero. Pick a body plan, assemble the parts, style it, grant it powers, then export a trading-card style specimen sheet.

The look is a dark, gritty comic style: heavy ink outlines, halftone and hatched shadows, angular anatomy, and Kirby-style energy crackle. Everything is drawn procedurally as SVG, so there are no image assets.

This is an unofficial fan project inspired by Saturday-morning alien-hero cartoons. It is not affiliated with or endorsed by any studio or franchise.

## Features

The builder has five steps:

1. **Form.** Eleven base body plans: Humanoid, Amorphous, Insectoid, Reptilian, Crystalline, Elemental, Aquatic, Technorganic, Botanical, Minikin (tiny, huge-brained) and Beast (quadruped). Then set size, arm count, leg count, eye count (including none), and wings or a tail.
2. **Parts.** A grid of heads, eyes, torsos, arms, legs, wings and tails, each with a live thumbnail. Only parts that fit the chosen form and limb counts are shown.
3. **Style.** Four hide colors with palette presets, six marking patterns, clothing, accessories, body alterations and enhancements.
4. **Powers.** Choose up to four from 33 powers in six categories. Powers natural to the species are badged and give a bonus.
5. **Profile.** Name, species and home world with random rollers, an auto-written dossier, and the hangar, card archive and share code tools below.

Other features:

- **Stat ratings.** Strength, Speed, Defense, Intellect and Energy update live from form, size, limbs, powers and enhancements.
- **Scramble.** Generates a complete random alien.
- **Hangar.** Save up to 12 aliens in the browser and reload them later.
- **Share codes.** Copy a code to send an alien to someone else, or paste one to load it.
- **Specimen card export.** Renders a PNG card with the art, stats and powers.
- **Card archive.** Every exported card is also saved to `localStorage` as a JPEG (about 75 KB each) and listed on the Profile step. If storage fills up, the oldest cards are dropped to make room.

## Run it

Open `index.html` in any modern browser. No build step or dependencies are needed. Fonts load from Google Fonts and fall back to system fonts when offline.

To serve it locally instead:

```bash
python3 -m http.server 8765
```

Then visit http://localhost:8765/index.html.

## GitHub Pages

A copy of the app lives in `docs/index.html` so it can be served with GitHub Pages: in the repository settings, set Pages to deploy from the `main` branch and the `/docs` folder. The page uses no relative asset paths, so it works under a project subpath such as `/omi-alien-builder/`.

`docs/index.html` is a plain copy of `index.html`. After editing the root file, refresh the copy:

```bash
cp index.html docs/index.html
```

## How it works

Everything lives in `index.html` as three scripts:

| Script | Contents |
| --- | --- |
| Data catalog | Forms, part catalogs per slot, palettes, clothing, accessories, alterations, enhancements, powers, and the name generators. Each part lists the forms and leg counts it fits. |
| Renderer | Procedural SVG drawing. `shaded()` builds the halftone and hatched shadows, `limbs()` draws outlined stroked limbs, and `kirby()` draws energy crackle. A grain filter is applied to the main preview and exported card. |
| App | State, stat calculation, the five step panels, persistence, share codes and card export. |

### Adding a part

1. Add an entry to the matching catalog (for example `HEADS`) with a `forms` list saying which forms may use it.
2. Add the drawing for it (for example an entry in `HEADDRAW`). Heads and torsos return a path plus optional `back` and `front` overlay functions.
3. Reload. The part appears in the Parts step for every listed form, and the random generator can pick it.

### Adding a form

Add an entry to `FORMS` with its allowed arm, leg and eye counts, defaults, base stats and colors. A form with `layout: 'beast'` uses the horizontal quadruped body.

## Storage

Nothing is sent to a server. The current alien, the hangar and the card archive are stored in the browser's `localStorage`, so they stay on one browser and one device and are lost if site data is cleared. Share codes are the way to move an alien elsewhere.

## License

No license has been chosen yet.
