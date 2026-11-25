# smartchargeapp.github.io

Public site of SmartCharge: <https://smartchargeapp.github.io/>

## What is served

- `index.html`, `ca/index.html`, `en/index.html`: the page that states what
  SmartCharge is for the user, in Spanish, Catalan and English. The site root is
  the Spanish page; the other two live under `/ca/` and `/en/`.
- `favicon.png`, `apple-touch-icon.png`: the app icon.
- `media/`: the short film of the idea page, wide (16:9) and tall (4:5, reframed for the phone), in
  Spanish, Catalan and English (`corto-<lang>.mp4`, `corto-<lang>-vertical.mp4`),
  with one poster per shape. Only the end card differs between languages. The
  page shows the wide one above 40rem and the tall one below, and fetches the
  video only on play. Also the silent loops of two cards (`loop-<name>.mp4`, with
  a poster each), the same in every language, fetched only when the card is on
  screen.
- `.nojekyll`: serves `.well-known/` and the generated pages as they are.
- `.well-known/appspecific/com.tesla.3p.public-key.pem`: the public key Tesla
  reads when a car is paired with the app. **Do not move, edit or rename it**:
  Tesla looks for that exact path, and a missing file stops new pairings.

## Where the pages come from

The pages are generated from the idea-page fragments in `buca1821/SmartCharge`
(`docs/producto/la-idea-de-smartcharge.html` and its `.ca.html` and `.en.html`
versions) by `scripts/build-site.py` in that repository. The generator lives
there and not here, so the code that runs with the deploy key is reviewed in
SmartCharge.

The workflow `.github/workflows/publish-site.yml` in `buca1821/SmartCharge`
regenerates and commits these pages when `main` changes something under
`docs/producto/`. It pushes here with a write deploy key scoped to this
repository; a regeneration that changes nothing does not commit. Its output is
noindex on purpose.

Do not edit the HTML here: the next publication overwrites it. To regenerate by
hand from a SmartCharge checkout:

    python3 scripts/build-site.py docs/producto /path/to/smartchargeapp.github.io

The two icons are generated once from the app icon and do not change with the
page. The files under `media/` are committed here by hand for the same reason:
`build-site.py` writes only the three pages, so the workflow never touches them.

## Checks after a change

- <https://smartchargeapp.github.io/> serves the idea page.
- <https://smartchargeapp.github.io/ca/> and `/en/` serve the other two.
- <https://smartchargeapp.github.io/.well-known/appspecific/com.tesla.3p.public-key.pem>
  still serves the key with status 200.
