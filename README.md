# Dose – supplements, lab results and check-ups

Dose is a private web app for your health routine:

- **Today** – your daily supplement plan by time of day, notes on amounts, timing and interactions, and what's due next.
- **Supplements** – every product with brand, ingredients, dose, timing, start date and planned duration. When you add one, you instantly see how it fits with your other supplements, medication and results.
- **Results** – lab reports (with history and trends) and examinations. Dose interprets your values, suggests what to take or change, and builds a schedule of follow-up tests, supplement monitoring and age-appropriate screenings.
- **Advisor** – optional AI (Claude) that knows your full picture: ask a question, review your results or check your whole plan.

Your data stays in your browser. Optional sync stores it **encrypted** in a private GitHub repository.

---

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest`, `icon-*.png`, `icon.svg` | Icon and “Add to Home Screen” |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are (hidden file – fine if it's missing) |
| `README.md` | This guide |

---

## 1. Put the app online (about 10 minutes)

1. Create a free account at [github.com](https://github.com).
2. Click **+** (top right) → **New repository**.
   - Name: `dose`
   - Visibility: **Public** (free GitHub Pages needs a public repository – the app itself contains no personal data)
   - Click **Create repository**.
3. On the next page click **uploading an existing file**. Unzip the download and drag all files into the browser window. Click **Commit changes**.
4. Go to **Settings → Pages**. Under *Build and deployment* choose **Deploy from a branch**, branch **main**, folder **/ (root)** → **Save**.
5. After 1–2 minutes the app is live at `https://YOUR-USERNAME.github.io/dose/`.

## 2. Add it to your phone

- **iPhone (Safari):** open the address → Share button → **Add to Home Screen**.
- **Android (Chrome):** open the address → ⋮ menu → **Add to Home screen** or **Install app**.

Each device keeps its own data until you set up sync (step 4).

## 3. Set up the AI advisor (optional)

1. Sign in to the Claude Console at [console.anthropic.com](https://console.anthropic.com) and add credit under **Billing**. You can set a monthly spending limit there.
2. Go to **API keys → Create key** and copy the key (starts with `sk-ant-`).
3. In Dose: **Settings → AI advisor** → paste the key → **Test connection**.
4. Repeat on each device – the key is stored only on the device and is never synced.

**Costs:** you pay per request. With the recommended Sonnet model, a report usually costs a few cents; current prices are on Anthropic's pricing page.

**Privacy:** only when you press an AI button are your profile, supplements and results sent to Anthropic's API. The key lives in your browser, so don't enter it on shared computers.

## 4. Sync between phone and computer (optional)

**a) Create a private data repository**
**+** → **New repository** → name `dose-data` → **Private** → tick **Add a README file** → **Create repository**.

**b) Create an access token that can only reach this repository**
Profile picture → **Settings** → **Developer settings** (bottom left) → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**:
- Token name: `Dose sync`
- Expiration: e.g. 1 year (create a new one when it runs out)
- Repository access: **Only select repositories** → `dose-data`
- Permissions → Repository permissions → **Contents: Read and write**
- **Generate token** and copy it (starts with `github_pat_`). It is shown only once.

**c) Connect each device**
In Dose: **Settings → Sync** → GitHub username, `dose-data`, the token, and an **encryption password** (at least 8 characters) → **Connect and sync**.
Use the **same password on every device** and write it down. Without it, the data on GitHub can't be opened.

How it works: your data is encrypted in the browser (AES-256) before upload, so GitHub only stores unreadable text. Dose syncs automatically after changes and when you open the app. If both devices changed something in the meantime, it asks which version to keep.

---

## Tips

- **Supplements:** for minerals, enter the elemental amount (“of which magnesium”), not the compound. For omega-3, enter EPA and DHA separately. With an API key you can photograph the label instead of typing.
- **Lab results:** add one report per blood test date. Enter your lab's reference range when it's printed – it takes priority over the app's general ranges. With an API key you can scan the report (photo or PDF); Chinese and German reports work too.
- **Units:** pick the unit for each value from the list (e.g. mmol/L or mg/dL, µmol/L or mg/dL, g/L or g/dL). New values start with SI units, as used in China and Europe – switch to conventional US units under **Profile → Lab units**. Values from different countries are converted, so trends and ratings still work. If your report uses a unit the app doesn't know, choose *Other unit…* and enter the lab's reference range – the value is then rated with that range.
- **Chinese test names** such as 铁蛋白, 低密度脂蛋白胆固醇, 谷丙转氨酶 or 25-羟基维生素D are recognized, as are common check-up (体检) values like urea, bilirubin, albumin, MCH/MCHC, ApoB and cystatin C.
- **Examinations:** if your doctor gives you a date for the next check, enter it as *Next appointment* – it overrides the standard interval.
- **Year of birth and sex** in your profile decide which screenings appear.
- **Calendar:** each due item has a button that downloads a calendar entry (.ics).

## Backups

**Settings → Data → Download backup** saves everything as a JSON file. Do this now and then – especially if you don't use sync. Clearing your browser's website data deletes the local copy.

## Updating the app

Upload the new `index.html` to the `dose` repository (**Add file → Upload files** → **Commit changes**). Your data isn't affected.

## Troubleshooting

| Message | What to do |
|---|---|
| Token rejected | The token expired or was copied incorrectly – create a new one (step 4b). |
| Repository not found | Check the username and repository name, and that the token has access to `dose-data`. |
| The token can't write | Token permissions: Contents must be *Read and write*. |
| Password doesn't match | Use the same encryption password on all devices. |
| Repository is public | Make `dose-data` private (Settings → General → Danger Zone). |
| API key rejected / credit used up | Check the key or top up credit in the Claude Console. |
| Model not available | Choose another model under Settings → AI advisor. |

## Important

Dose does not replace medical or pharmaceutical advice. The rule check and the AI can make mistakes or miss interactions. Discuss changes – especially with conditions and medication – with your doctor or pharmacist.

Sources: upper limits from EFSA opinions (up to 2024); reference ranges are general adult values; screening intervals follow common international guidelines and differ by country.

## Extending the knowledge base

All rules sit in `index.html` in the section marked **KNOWLEDGE BASE** (`window.KB`): nutrients, lab markers, interactions, medications, conditions, monitoring and screenings. If you'd rather not edit code, ask Claude to add entries and upload the new `index.html`.
