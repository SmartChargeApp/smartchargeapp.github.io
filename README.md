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

The pages are generated, not edited here. Their source is `buca1821/SmartCharge`,
`docs/producto/la-idea-de-smartcharge.html` and its `.ca.html` and `.en.html`
versions, which are artifact fragments (no doctype, no `<html>`, no viewport).
`build-site.py` turns them into the full documents served here: doctype,
`html lang`, viewport, title, description, social tags and the language links
pointing at `/`, `/ca/` and `/en/`.

To regenerate after the source pages change, from a checkout of
`buca1821/SmartCharge` (private):

    python3 /path/to/smartchargeapp.github.io/build-site.py docs/producto /path/to/smartchargeapp.github.io

Then commit the three generated `index.html` files. The two icons are generated
once from the app icon and do not change with the page.

The pages carry `noindex, nofollow`. Remove that tag in `build-site.py` if the
site should appear in search engines.

## Checks after a change

- <https://smartchargeapp.github.io/> serves the idea page.
- <https://smartchargeapp.github.io/ca/> and `/en/` serve the other two.
- <https://smartchargeapp.github.io/.well-known/appspecific/com.tesla.3p.public-key.pem>
  still serves the key with status 200.
