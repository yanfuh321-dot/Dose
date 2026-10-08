# Google Drive – setup

Dose can read lab and examination reports – photos and PDFs – from one Google Drive folder and add them for you. You set this up once in Google Cloud; it's free. In mainland China you need your VPN for this. A computer makes the setup easier.

## 1. Create a Google Cloud project

1. Open [console.cloud.google.com](https://console.cloud.google.com) and sign in with the Google account that owns the Drive folder.
2. In the top bar open the project picker → **New project** → name it `Dose` → **Create**, then select it.

## 2. Enable the Google Drive API

Menu → **APIs & Services → Library** → search **Google Drive API** → **Enable**.

## 3. Set up the consent screen

Menu → **APIs & Services → OAuth consent screen** (newer consoles call this **Google Auth Platform**).

1. **Get started:** app name `Dose`, your email as support email → Audience **External** → contact email → agree → **Create**.
2. **Audience:** leave the publishing status on **Testing**. Under **Test users** → **Add users** → your own Google address.
3. **Data access:** **Add or remove scopes** → search `drive.readonly` → tick `…/auth/drive.readonly` → **Update** → **Save**.

## 4. Create the client ID

**Clients** → **Create client** (older consoles: Credentials → Create credentials → OAuth client ID):

- Application type: **Web application**, name `Dose`
- **Authorized JavaScript origins** → **Add URI** → your app's address without a path, e.g. `https://yourname.github.io`. Dose shows the exact value under Settings → Google Drive.
- No redirect URI is needed.
- **Create** and copy the **Client ID** (ends in `.apps.googleusercontent.com`). It isn't secret.

## 5. Connect Dose

1. In Google Drive open the folder with your reports and copy its link (Share → Copy link, or the address bar).
2. Dose → **Settings → Google Drive**: paste client ID and folder link → **Connect and check**.
3. A Google window opens. Choose your account. Because the app is in testing, Google says *“Google hasn't verified this app”* → **Continue**, then allow access to your Drive files (read only).
4. From now on: **Results → From Drive** reads all new files in the folder.

## Good to know

- Readable: PDF, JPG, PNG, WebP. Phone photos in HEIC format and Google Docs are skipped – save them as JPG or PDF.
- Subfolders (up to 3 levels) are included.
- Dose remembers which files were imported – also across synced devices. A file that changes is read again; a report that's already in Dose is recognized and skipped.
- Each file is one AI request. Imported reports are marked *“Imported – please check”* until you open and save them.
- Dose only reads – nothing in your Drive is changed. Files go from Drive to your browser and on to your AI provider; the original is attached to the imported report.
- The sign-in lasts about an hour; after that one tap renews it. In testing mode Google may ask you to sign in again about once a week.

## Troubleshooting

| Message | What to do |
|---|---|
| The Google sign-in window was blocked | Allow pop-ups for your app's site. In Brave, lower Shields for the site if sign-in keeps failing. |
| `origin_mismatch` or `redirect_uri_mismatch` | The authorized JavaScript origin must match your app's address exactly (step 4). |
| `access_denied` / app blocked | Add your Google account as a test user (step 3). |
| Google Drive refused access … API | Enable the Google Drive API (step 2). |
| The Drive folder wasn't found | Check the folder link; sign in with the account that owns the folder or has access to it. |
| Google sign-in couldn't be loaded | Turn on your VPN. |
