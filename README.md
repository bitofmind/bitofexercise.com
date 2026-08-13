# bitofexercise.com

Landing page for **Bit of Exercise**, the iPhone app by Bit of Mind.
Static site hosted on GitHub Pages.

Migrated 2026-08-13 from the "OurWay" website builder (ourwayapp.com on AWS), which
served the domain over plain HTTP only — its TLS certificate was issued for
`ourwayapp.com`, so `https://bitofexercise.com` failed hostname verification.
GitHub Pages provides a proper auto-renewing certificate.

## Contents

- `index.html` — the page. Plain HTML/CSS; the old builder loaded Bootstrap 3 and
  jQuery but used neither. Same copy, same images, responsive feature grid.
- `icon.png`, `screens.png`, `appstore.png` — now **self-hosted**. They previously
  loaded from the builder's S3 bucket (`justl-imgrep2.s3.amazonaws.com`), which would
  have disappeared along with the old host.
- `.nojekyll` — keeps GitHub Pages from running Jekyll (which ignores dot-directories).

Two small corrections while transcribing: the App Store link was updated from the
legacy `itunes.apple.com` to `apps.apple.com`, and "Strave" was corrected to "Strava".

## Going live

⚠️ **Do not delete the `MX` records.** The zone carries Loopia mail
(`mailcluster.loopia.se`, `mail2.loopia.se`) serving `info@bitofexercise.com`.
Changing `A`/`CNAME` records does not affect mail, but deleting `MX` rows would break
it. Leave the `NS` records alone too. Loopia's **"Återställ DNS-backup"** is the
safety net.

1. In Loopia DNS for `bitofexercise.com`:
   - **remove** the `A` record `35.167.226.66` (the OurWay host) under `@` and `www`
   - add four `A` records on `@`:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - add `www` as `CNAME` to `bitofmind.github.io.`
2. Repo Settings → Pages → Custom domain → `bitofexercise.com` → **Enforce HTTPS**
3. The certificate is issued within a few minutes.
