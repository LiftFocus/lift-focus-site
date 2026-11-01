# Lift Focus site

Static Support and Privacy pages for App Store Connect. Hosted free on GitHub Pages under the **brand** GitHub account (not your personal account).

| Page | File | App Store Connect field |
|------|------|-------------------------|
| Support | `support.html` | Version → Support URL |
| Privacy | `privacy.html` | App Privacy / App Information → Privacy Policy URL |

**Support email on the pages:** `liftfocusapp@gmail.com`  
**Commit identity for this repo:** name `Lift Focus`, email `liftfocusapp@gmail.com`

## Before you start — set your GitHub username

Replace every `BRAND_GITHUB_USERNAME` in this README with the brand account’s GitHub username (the one you log into, which may differ from the Gmail local-part).

Live base URL will be:

```text
https://BRAND_GITHUB_USERNAME.github.io/lift-focus-site/
```

## Change the support email later

Search for `SUPPORT_EMAIL` (or `liftfocusapp@gmail.com`) in `support.html` and `privacy.html`, update both, then commit and push.

## 1. Create the public repo (brand account)

1. Log into the **brand** GitHub account in the browser.
2. Create a **public** repository named `lift-focus-site` (no README/license needed if you will push this folder).

## 2. SSH key for the brand account only

Keep your personal `github.com` SSH setup as-is. Add a second key for the brand account.

```bash
ssh-keygen -t ed25519 -C "liftfocusapp@gmail.com" -f ~/.ssh/id_ed25519_liftfocus
```

Add the **public** key (`~/.ssh/id_ed25519_liftfocus.pub`) in the brand account:  
GitHub → Settings → SSH and GPG keys → New SSH key.

Append a host alias to `~/.ssh/config` (create the file if needed):

```text
Host github.com-liftfocus
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_liftfocus
  IdentitiesOnly yes
```

Test:

```bash
ssh -T git@github.com-liftfocus
```

You should see a success message naming the **brand** username.

## 3. Init this folder with brand commit identity

From this folder — **local** config only (does not change your global personal git identity):

```bash
cd "/Users/moaan/Projects/Mobile/lift-focus-site"

git init
git config user.name "Lift Focus"
git config user.email "liftfocusapp@gmail.com"

# Confirm (must show Lift Focus / liftfocusapp@gmail.com)
git config user.name
git config user.email

git add .
git commit -m "Add Lift Focus support and privacy pages"
git branch -M main

# Verify the commit author before pushing
git log -1 --format='%an <%ae>'
```

If the author is wrong, fix local config and amend **before** the first push:

```bash
git commit --amend --reset-author --no-edit
```

## 4. Push via the brand SSH alias

```bash
git remote add origin git@github.com-liftfocus:BRAND_GITHUB_USERNAME/lift-focus-site.git
git push -u origin main
```

Do **not** use `git@github.com:...` here — that can authenticate as your personal account.

## 5. Enable GitHub Pages

1. Brand repo → **Settings → Pages**
2. Build and deployment: **Deploy from a branch** → `main` → `/ (root)` → Save
3. Wait about a minute, then open in a private browser window:

```text
https://BRAND_GITHUB_USERNAME.github.io/lift-focus-site/support.html
https://BRAND_GITHUB_USERNAME.github.io/lift-focus-site/privacy.html
```

## 6. App Store Connect

Paste:

- **Support URL:** `https://BRAND_GITHUB_USERNAME.github.io/lift-focus-site/support.html`
- **Privacy Policy URL:** `https://BRAND_GITHUB_USERNAME.github.io/lift-focus-site/privacy.html`

## Notes

- This folder is separate from the Lift Tracker Xcode project on purpose (free Pages needs a public repo; the app repo can stay private).
- Always commit from this directory after the local `user.email` is set so personal email does not appear in history.
