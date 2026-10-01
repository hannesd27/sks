# SKS Lernapp – Privacy Policy Website

This repository holds the public privacy policy and Impressum for the mobile app **SKS** (in-app title **SKS Lernapp**, iOS and Android, bundle ID / application ID `com.einsteinhain.sks`).

It is a small static website: plain HTML and CSS only. It has no backend, database, build step, JavaScript, cookies, analytics, tracking, external fonts or other external resources. You don't need any secrets or API keys to run or deploy it.

> **Disclaimer:** The texts were drafted from the facts and decisions in [`docs/content-notes.md`](docs/content-notes.md). They are not legal advice and have not been reviewed by a lawyer. They don't guarantee compliance with the GDPR, Apple or Google rules, or any other law.

## URLs

The whole repository is published under **`https://einsteinhain.com/sks/`**. These are the only public URLs:

| Page | Public URL | File | Local preview |
|---|---|---|---|
| Datenschutzerklärung (German, **primary**) | `https://einsteinhain.com/sks/datenschutz/` | `datenschutz/index.html` | http://localhost:8000/datenschutz/ |
| Privacy Policy (English translation) | `https://einsteinhain.com/sks/privacy-policy/` | `privacy-policy/index.html` | http://localhost:8000/privacy-policy/ |
| Impressum | `https://einsteinhain.com/sks/impressum/` | `impressum/index.html` | http://localhost:8000/impressum/ |
| Landing page (links to the three pages above) | `https://einsteinhain.com/sks/` | `index.html` | http://localhost:8000/ |

The `localhost` addresses only work on your own computer while the preview server is running. They are never given to Apple, Google or users.

**The URL to give Apple and Google is `https://einsteinhain.com/sks/datenschutz/`.** See [`docs/store-submission.md`](docs/store-submission.md) for every field.

Always use the URLs **with** the trailing slash.

## Structure

```
/                             → https://einsteinhain.com/sks/
├── index.html                landing page with links to the pages below
├── datenschutz/index.html    German privacy policy (primary)
├── privacy-policy/index.html English translation
├── impressum/index.html      Impressum (§ 5 DDG)
├── css/styles.css            the only stylesheet (light and dark mode)
├── icons/                    tab and home-screen icons (the app icon, from the app repo)
├── .github/workflows/pages.yml  publishes only the files above to GitHub Pages
├── docs/                     (not published on the website)
│   ├── content-notes.md      facts, decisions, sources
│   ├── store-submission.md   exact values for App Store Connect and Play Console
│   ├── in-app-link.md        how to link the policy from the app
│   └── github-pages-user-site/  the two files for the separate user-site repo
├── README.md
├── LICENSE                   all rights reserved
└── .gitignore
```

## Local preview

```bash
cd /Users/hd/apps/einsteinhain/web && python3 -m http.server 8000
```

Then open http://localhost:8000/. Locally the site runs at `/`; on the web it runs at `/sks/`. All links are relative, so both work without changes.

## Deployment (GitHub Pages)

The site is hosted on GitHub Pages; the privacy policy's section “Diese Website / This website” describes this. Hosting it at `einsteinhain.com/sks/` needs two GitHub repositories. **A repository named `sks` is served at `einsteinhain.com/sks/` when your user site has the custom domain `einsteinhain.com`.** The URL path comes from the GitHub repository name, not from the local folder name (`web`), so the folder can be renamed freely, but renaming the repository changes every public URL.

Below, `<username>` is your GitHub username. Your git user name is `hannesd27`; use your actual GitHub username if it is different.

### 1. This repository → `github.com/<username>/sks`

1. On GitHub, create a new repository named exactly **`sks`**, with no README. On the free plan it must be **public** to use Pages. The files in `docs/` are then visible in the repository, but not on the website.
2. Push this folder:

   ```bash
   cd /Users/hd/apps/einsteinhain/web && git add -A && git commit -m "SKS privacy policy website" && git branch -M main && git remote add origin https://github.com/<username>/sks.git && git push -u origin main
   ```

3. Repository → *Settings → Pages → Build and deployment → Source*: choose **GitHub Actions**. The workflow `.github/workflows/pages.yml` then publishes on every push to `main`. **Don't** set a custom domain in this repository.

### 2. User site → `github.com/<username>/<username>.github.io`

1. Create a public repository named exactly **`<username>.github.io`**.
2. Add the two files from `docs/github-pages-user-site/`:
   - `CNAME`, containing `einsteinhain.com`
   - `index.html`, which redirects `einsteinhain.com/` to `/sks/`
3. Repository → *Settings → Pages*: source **Deploy from a branch**, `main`, `/ (root)`. The custom domain field should show `einsteinhain.com`.
4. Recommended: your GitHub profile → *Settings → Pages → Add a domain*, and verify `einsteinhain.com` with the TXT record GitHub shows. This stops anyone else from using your domain on GitHub Pages.

### 3. DNS at Namecheap → *Domain List → einsteinhain.com → Advanced DNS*

Delete the existing parking records (the `www` CNAME to `parkingpage.namecheap.com` and any URL-redirect record for `@`). Then add:

| Type | Host | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `<username>.github.io.` |

These are the addresses from GitHub's documentation (checked 30 September 2026).

### 4. HTTPS and test

1. When DNS has updated (minutes to hours), go to the user-site repository → *Settings → Pages* and tick **Enforce HTTPS**. The certificate can take a little while to appear.
2. Open these in a normal browser and in a private window:
   - https://einsteinhain.com/sks/datenschutz/
   - https://einsteinhain.com/sks/privacy-policy/
   - https://einsteinhain.com/sks/impressum/
   - https://einsteinhain.com/ (should land on the SKS landing page)
3. Then fill in the store forms ([`docs/store-submission.md`](docs/store-submission.md)) and add the link to the app ([`docs/in-app-link.md`](docs/in-app-link.md)).

If you ever move away from GitHub Pages, update the section “Diese Website / This website” in both languages.

## Keeping the two languages in sync

The German page is the primary text, and the English page is a translation with the same sections in the same order. When you change the policy:

1. Change `datenschutz/index.html`, then make the same change in `privacy-policy/index.html`.
2. Update **Zuletzt aktualisiert** / **Last updated** on both pages. Dates use `<time datetime="YYYY-MM-DD">`.
3. Change **Gültig ab** / **Effective date** only if the new version takes effect on a different date.
4. Update `docs/content-notes.md`.

If your name, address or email change, update `datenschutz/`, `privacy-policy/`, `impressum/`, `LICENSE` and `docs/store-submission.md`.

While drafting, you can mark unfinished text with `<mark class="placeholder">[…]</mark>`, which shows up in yellow. Before publishing, this command must print nothing:

```bash
grep -rn -E 'class="placeholder"|\[[A-Z ]+\]' --include='*.html' .
```

## Privacy of this website

The site contains **no analytics, tracking, cookies, JavaScript, external fonts, external images or third-party requests**. A Content-Security-Policy `<meta>` tag lets each page load only its own stylesheet. Server logs kept by the hosting provider are described in the section “Diese Website” / “This website” of the policy.

## Publication checklist

- [x] Developer name, address and email supplied
- [x] Effective date supplied
- [x] Public domain and URLs decided
- [x] German version written
- [x] Impressum written
- [x] Hosting provider chosen (GitHub Pages) and policy updated for it
- [ ] Texts reviewed by developer (and ideally a lawyer)
- [ ] Both GitHub repositories set up and DNS changed (README → Deployment)
- [ ] Published over HTTPS under `https://einsteinhain.com/sks/`
- [ ] All three URLs tested in a normal browser
- [ ] App Store Connect and Google Play Console filled in as in `docs/store-submission.md`
- [ ] Privacy policy linked inside the app (`docs/in-app-link.md`)
