# Dash Digital - Client Uploads

A page where clients upload their logo, photos and other files. Everything lands in a Client Uploads folder in your Google Drive, one folder per submission, and you get an email when they're done.

Hosted at **upload.dashdigital.ca** (change it to whatever subdomain you like).

## Files
- `index.html`: the upload page
- `Code.gs`: the Google Apps Script that saves files to Drive (this does NOT go on Cloudflare)
- `logo.png`, `favicon.png`, `apple-touch-icon.png`

## Step 1: Set up the Google side (one time, about 5 minutes)
1. Go to https://script.google.com while signed in to the Google account whose Drive should get the files. Click **New project**.
2. Delete the sample code, paste in everything from `Code.gs`, and click **Save**. Name the project "Dash Digital Uploads".
3. In the dropdown at the top, pick **setup** and click **Run**. Google will ask for permission: click through and **Allow**. (If it says "Google hasn't verified this app", click **Advanced**, then **Go to Dash Digital Uploads**. That's normal for your own scripts.)
4. Click **Deploy**, then **New deployment**. Click the gear icon and pick **Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Click **Deploy** and copy the **Web app URL** (it ends in `/exec`).

## Step 2: Connect the page
Done. `index.html` already has your Apps Script URL in `UPLOAD_URL`. If you ever make a brand-new deployment, paste the new URL there.

## Step 3: Put it online
1. Upload these files (not `Code.gs`) to a new GitHub repo, e.g. `client-uploads`.
2. Cloudflare: Workers & Pages, then Create, then Pages, then Connect to Git. Pick the repo. Framework preset: None. Build command: empty. Output directory: `/`.
3. In the project: Custom domains, add `upload.dashdigital.ca`.

## Where files go
Google Drive: `Client Uploads / Business Name / Logo, Photos, Anything else`. Every submission gets its own new folder.

## Good to know
- Max 35 MB per file. Bigger files (like long videos) need another way, like a shared Drive link.
- If you ever change `Code.gs`, deploy again with **Deploy, Manage deployments, Edit, New version** so the URL stays the same.
