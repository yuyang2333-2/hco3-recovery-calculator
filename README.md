# Bicarbonate recovery failure calculator

A static site hosting a clinical prediction calculator and its methods page. No build step, no dependencies, no server-side code.

Accompanies the manuscript *Discordance between anion gap load and bicarbonate recovery in sepsis: a four-database cohort study with a 12-hour prediction tool*.

## Pages

| File | Purpose |
|---|---|
| `index.html` | The calculator. Self-contained: the fitted model is embedded, so it works offline and with JavaScript alone. |
| `about.html` | Development cohorts, predictor encoding, performance, verification instructions and limitations. |
| `404.html` | Not-found page. |

## Deploying

The site is plain static files. Any static host will serve it unchanged.

**GitHub Pages, no command line required**

Create an empty public repository, choose *Add file &rarr; Upload files*, drag the contents of this folder in, and commit. Then skip to the Pages settings below.

**GitHub Pages, from a terminal**

```
git init
git add .
git commit -m "Calculator v1.0"
git branch -M main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

Then: repository Settings &rarr; Pages &rarr; Source `Deploy from a branch`, Branch `main`, folder `/ (root)`. The site appears at `https://<user>.github.io/<repo>/` within a minute or two. The `.nojekyll` file stops Jekyll from reprocessing the HTML.

**Netlify / Cloudflare Pages**

Drag the folder onto the dashboard, or point the service at the repository. `netlify.toml` already sets the publish directory to the repository root.

## Before going live

- The footer links to the archive inside this repository. Once the Zenodo record exists, add its DOI to the footer of `index.html` and to the "Archived record" line of `about.html`.
- Add the journal DOI to the citation block once the article is published.

## Verification

The calculator's arithmetic can be checked independently. The archived source package contains `model.json` (XGBoost booster, 310 trees), `ref_pred.csv` (60 reference predictions) and `t_check.js`:

```
node t_check.js
# n 60  max abs diff 6.246e-7
```

## Licence

Content and code released under CC BY 4.0. No patient-level data are included; the model is derived from MIMIC-IV, eICU-CRD, SICdb and NWICU under their respective data use agreements.

## Not a medical device

This is a research tool. It is not validated for individual patient care and must not be used as the sole basis for a clinical decision.
