# smartchargeapp.github.io

Public site of SmartCharge: <https://smartchargeapp.github.io/>

## What is served

- `index.html`, `ca/index.html`, `en/index.html`: the page that states what
  SmartCharge is for the user, in Spanish, Catalan and English. The site root is
  the Spanish page; the other two live under `/ca/` and `/en/`.
- `favicon.png`, `apple-touch-icon.png`: the app icon.
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
page.

## Checks after a change

- <https://smartchargeapp.github.io/> serves the idea page.
- <https://smartchargeapp.github.io/ca/> and `/en/` serve the other two.
- <https://smartchargeapp.github.io/.well-known/appspecific/com.tesla.3p.public-key.pem>
  still serves the key with status 200.
