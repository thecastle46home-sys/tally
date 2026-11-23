# Tally: setup for two phones with Google Drive sync

## 1. Put Tally online (free)
Google sign-in only works from a real https web address, so host this folder:
- **GitHub Pages**: create a repo, upload every file in this folder, then Settings > Pages > Deploy from branch (main, root). You get an address like `https://<user>.github.io/tally/`.
- **Netlify Drop**: drag this folder onto app.netlify.com/drop. You get an address like `https://<name>.netlify.app`.

## 2. Create a Google client ID (signed in as the new Gmail)
1. Go to console.cloud.google.com and create a project called "Tally".
2. APIs & Services > Library > enable **Google Drive API**.
3. Google Auth Platform (OAuth consent screen): app name "Tally", audience **External**, leave it in **Testing**, and add the new Gmail address as a **test user**.
4. Clients > Create client > **Web application**. Under **Authorised JavaScript origins** add your address from step 1 with no path or trailing slash (for example `https://<user>.github.io`).
5. Copy the client ID (it ends in `.apps.googleusercontent.com`).

Optional: paste the ID into `GOOGLE_CLIENT_ID` near the "Google Drive sync" section of index.html so the phones don't have to enter it.

## 3. On each phone
1. Open your Tally address in Chrome (Android) or Safari (iPhone).
2. Settings > paste the client ID > Connect Google Drive, then sign in with the **shared Gmail**. Google will warn that the app isn't verified because it's your own app in testing; tap Continue.
3. Add to home screen: Chrome menu > Add to home screen / Install app; Safari share button > Add to Home Screen.

## How sync works
- The data lives in one file, `tally-data.json`, in that Gmail's Drive. Tally can only see files it created itself, not the rest of the Drive.
- Changes upload about 2 seconds after you make them. The other phone pulls them in when it's opened, and every minute while it's open.
- Google sign-in lasts about an hour. When the pill at the top says "Tap to sync", tap it.
- If both phones change things while offline, the changes merge. If the same statement gets imported on both phones, Tally keeps one copy.
- Don't edit or rename `tally-data.json` by hand.
