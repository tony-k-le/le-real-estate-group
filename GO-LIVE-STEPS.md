# Go Live — Beginner Step-by-Step

Three parts, in order:
- **Part 1:** Put the website on GitHub (no software to install).
- **Part 2:** Connect GitHub to Cloudflare so it publishes.
- **Part 3:** Point your Squarespace domain at Cloudflare.

Take it slow, one numbered step at a time. You've got this.

The folder you'll be uploading is:
`...\LE real estate group - Claude Deploy Folder\le-real-estate-group`

---

## Part 1 — Put the site on GitHub

### A. Make a GitHub account (skip if you have one)
1. Go to **https://github.com**.
2. Click **Sign up** (top right). Follow the prompts (email, password, username). Verify your email.

### B. Create an empty repository ("repo")
1. Once logged in, click the **+** icon in the very top-right corner.
2. Click **New repository**.
3. **Repository name:** type `le-real-estate-group`.
4. Leave it on **Public** (simplest). 
5. **Do NOT** check "Add a README file" (we already have one).
6. Click the green **Create repository** button.

### C. Upload your website files
1. On the new empty repo page, find the line of small links and click **uploading an existing file** (it's in the sentence "…or **uploading an existing file**"). 
   - If you don't see it, go to this address in your browser, replacing `YOUR-USERNAME`: `https://github.com/YOUR-USERNAME/le-real-estate-group/upload`
2. Open your `le-real-estate-group` folder on your computer in a separate window.
3. Select **everything INSIDE** that folder (the `public` folder, `README.md`, `wrangler.toml`, etc.) — **not** the folder itself. A quick way: click inside the folder, then press **Ctrl+A** to select all.
4. **Drag** those selected items onto the GitHub upload page where it says "Drag files here".
5. Wait for the files to finish uploading (you'll see them listed).
6. Scroll down to **Commit changes**. In the first box type: `Initial website`.
7. Click the green **Commit changes** button.

✅ Your website code now lives on GitHub. Leave this tab open.

---

## Part 2 — Publish it with Cloudflare Pages

### A. Make a Cloudflare account (skip if you have one)
1. Go to **https://dash.cloudflare.com/sign-up**.
2. Enter email + password, click **Sign up**, and verify your email.

### B. Create the Pages project from GitHub
1. In the Cloudflare dashboard left sidebar, click **Workers & Pages**.
2. Click the blue **Create** button.
3. Click the **Pages** tab.
4. Click **Connect to Git**.
5. Click **Connect GitHub** (or **Sign in / Add account**). A GitHub window pops up — click **Authorize Cloudflare**.
6. When asked which repositories, choose **Only select repositories**, pick **le-real-estate-group**, and click **Install & Authorize**.
7. Back in Cloudflare, select **le-real-estate-group** from the list and click **Begin setup**.

### C. Tell Cloudflare how to build it
On the setup screen, set these three fields:
1. **Framework preset:** choose **None**.
2. **Build command:** leave **empty** (blank).
3. **Build output directory:** type **`public`**.
4. Click **Save and Deploy**.

Cloudflare will work for ~1 minute and then show a success screen with a web address like
`https://le-real-estate-group.pages.dev`.

5. Click that link and check that your site looks right. 🎉

> From now on, any change you upload to GitHub will automatically re-publish here.

---

## Part 3 — Point your Squarespace domain to Cloudflare

This makes `lerealestategroup.com` show your new site instead of the old Squarespace one.

### A. Add your domain to Cloudflare and get your nameservers
1. In Cloudflare, click the Cloudflare logo (top-left) to go to the main dashboard.
2. Click **+ Add a domain** (or **Add a site**).
3. Type **`lerealestategroup.com`** and click **Continue**.
4. Choose the **Free** plan and click **Continue**.
5. Cloudflare scans your existing settings — click **Continue** / **Add records** to accept what it found.
6. Cloudflare now shows you **two nameservers**, for example:
   - `xxxx.ns.cloudflare.com`
   - `yyyy.ns.cloudflare.com`
   **Keep this page open** — you'll copy these in the next step. (They're unique to your account.)

### B. Enter those nameservers at Squarespace
1. In a new tab, log in at **https://account.squarespace.com/domains**.
2. Click your domain **lerealestategroup.com**.
3. Click **DNS** (or **DNS Settings**), then look for **Nameservers** / **Advanced Settings**.
4. Find the **Nameservers** section and switch it to **Use custom nameservers** (you may need to toggle off "Use Squarespace nameservers").
5. Delete any existing nameservers, then **paste the two Cloudflare nameservers** from Part 3A.
6. If Squarespace warns you about **DNSSEC**, follow its prompt to **disable DNSSEC** (Cloudflare needs this off to take over).
7. Click **Save**.

### C. Wait, then finish in Cloudflare
1. Nameserver changes take anywhere from a few minutes to ~24 hours. Cloudflare will **email you** when your domain is **Active**.
2. Once active, go to **Workers & Pages → le-real-estate-group → Custom domains**.
3. Click **Set up a domain**, type **`lerealestategroup.com`**, click **Continue / Activate domain**.
4. Click **Set up a domain** again and add **`www.lerealestategroup.com`** the same way.
5. Cloudflare automatically turns on **HTTPS (the padlock)** — no action needed, just give it a few minutes.

### D. Check it worked
1. Open **https://lerealestategroup.com** and **https://www.lerealestategroup.com** — both should show your new site with a padlock.
2. Try an old link like **lerealestategroup.com/properties** — it should jump to the Properties section (the redirects handle this).

✅ You're live!

---

## After you're confident it's stable (a few days later)
- You can stop paying for the **Squarespace website** plan. **Do not** let the **domain registration** lapse — that's separate, and it's what keeps `lerealestategroup.com` yours.
- Before cancelling anything, make sure you've kept the **Squarespace content export** (the `.xml` file) and saved any photos. See `DEPLOY-GUIDE.md`.

---

## If you get stuck
- **Squarespace won't let you set custom nameservers?** Some domains only allow "DNS connect." In that case, tell me and I'll give you the alternative (adding CNAME records instead of changing nameservers).
- **Site shows but photos are missing / forms don't send?** Those are the two optional improvements (self-hosting images, wiring up forms). Ask me and I'll handle them.
- Stuck on any single step? Tell me the screen you're on and what you see, and I'll walk you through it.
