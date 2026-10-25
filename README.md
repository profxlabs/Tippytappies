# Tippy Taps

A one-page static site. Each page load shows a random dog tippy taps GIF, except about 1 time in 1,000, when it shows a hand tap dancing GIF instead.

## Files

- `index.html` is the whole site. No build step, no dependencies.
- `candidates.html` is a picker page for choosing GIFs. Don't upload it (or do, it's harmless).

## The odds

About 1 in 345 US children have cerebral palsy, and 33.3% of them have limited or no walking ability ([CDC](https://archive.cdc.gov/www_cdc_gov/ncbddd/cp/data.html)). That works out to about 0.097%, rounded to 1 in 1,000. CP is the most common cause of being unable to walk from birth; adding rarer causes like spina bifida would nudge it a little higher.

The rare outcome is the hand tap dance, since it's dancing without using your legs. To change the odds, edit `HAND_ODDS` near the bottom of `index.html`.

## A fresh GIF every load

Each load picks a random GIF from the chosen category and avoids ones that browser has seen recently.

- **With a GIPHY key (recommended):** the site searches GIPHY live (`dog tippy taps` / `finger tap dance`), so the dog side has hundreds of options. Get a free key at https://developers.giphy.com/dashboard/ (Create an App → API), then paste it into `GIPHY_KEY` in `index.html`. A new key is rate-limited to about 100 searches an hour, which is plenty for a few friends. The key is visible in the page source, which is normal for GIPHY keys.
- **Without a key:** it rotates through the built-in `ids` lists (8 dog, 4 hand) in `index.html`.

To tune it, edit `search` (the GIPHY search words) or `ids` (fallback GIFs) on `DOG` and `HAND`. A GIF's id is the last chunk of its link, e.g. `giphy.com/gifs/happy-dog-WOZsizbEUWoxCSQLAM` → `WOZsizbEUWoxCSQLAM`. `candidates.html` previews some ids.

Add `?hand` or `?dog` to the URL to force a category while checking.

GIFs are hotlinked from GIPHY's CDN, which GIPHY allows, with a small "via GIPHY" credit in the footer.

## Hosting (pick one)

### Netlify (easiest, no account setup beyond sign-in)

1. Go to https://app.netlify.com/drop and drag the `tippytappies` folder onto the page.
2. You get a `something.netlify.app` URL immediately.
3. To update later, open the site in Netlify → Deploys → drag the folder in again.

### GitHub Pages

1. Create a public repo on GitHub and upload `index.html`.
2. Repo → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The site appears at `https://<username>.github.io/<repo>/`.

## Pointing your domain at it

Do this at your domain registrar's DNS settings.

**Netlify:** Site → Domain management → Add a domain → enter your domain. Then at your registrar:
- For `www.yourdomain.com` (or any subdomain): add a `CNAME` record pointing to `<your-site>.netlify.app`.
- For the bare `yourdomain.com`: add an `A` record pointing to `75.2.60.5`, or move your DNS to Netlify as it offers.

**GitHub Pages:** Repo → Settings → Pages → Custom domain → enter your domain and save. Then at your registrar:
- For a subdomain like `taps.yourdomain.com`: `CNAME` → `<username>.github.io`.
- For the bare domain: four `A` records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
- Tick "Enforce HTTPS" once it becomes available.

DNS changes usually take minutes, occasionally up to a day. Both hosts issue a free HTTPS certificate automatically.
