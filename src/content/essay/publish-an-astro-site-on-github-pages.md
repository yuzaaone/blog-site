---
title: Publish an Astro Site on GitHub Pages
description: Choose an Astro theme, publishing it with GitHub Pages, connecting a custom domain, and turning on HTTPS.
date: 2026-08-12
badge: Guide
tags: ["Astro", "GitHub Pages"]
draft: false
---

You do not need to be a developer to put a small, fast website online. With a ready-made [Astro theme](https://astro.build/themes/), GitHub’s website, and a domain name, you can publish a static site without opening a terminal.

> **What "static" means:** your pages are prepared ahead of time and served as simple files. That makes them fast, inexpensive to host, and well suited to blogs, portfolios, documentation, and personal sites.

## Before you begin

You will need:

- A [GitHub account](https://github.com/)
- A domain name if you want a custom address, such as `blog.example.com`. Don't worry if you don't have one, GitHub would host the site on their own domain, such as `blog.github.io`.
- An Astro theme of your choosing.

## 1. Choose a theme you actually like

Open the [Astro themes directory](https://astro.build/themes/) and use its filters to look for free themes. Open a theme’s preview and read its description. A theme built for a blog, portfolio, or documentation site will usually be easiest to adapt.

When you find one you like, click through to its GitHub repository. In this case, the starting point was the [Astro Whono theme](https://github.com/cxro/astro-whono).

## 2. Fork the theme into your GitHub account

On the theme repository page, click **Fork** near the top-right corner. GitHub will ask where to place the copy, choose your own account and keep the suggested repository name, or give it a name you prefer.

A fork is your own editable copy of the project. You can safely change its text, images, colours, and layout without changing the original creator’s work.

Once the fork is created, use the **Code** tab to browse the files. GitHub lets you edit many text files directly in the browser:

1. Open a file.
2. Click the pencil icon, **Edit this file**.
3. Make the change.
4. Add a short description at the bottom, then click **Commit changes**.

Each commit is simply a saved version of your site. If something goes wrong later, the history makes it easier to understand and undo.

## 3. Add the GitHub Pages workflow

Astro creates the finished static files during a build. GitHub Actions can perform that build every time you save a change to the repository.

In your fork, create a file called `.github/workflows/deploy.yml` using GitHub’s browser editor. You can do this by choosing **Add file** → **Create new file**, entering that full path as the filename, and pasting the workflow from [Astro’s GitHub Pages guide](https://docs.astro.build/en/guides/deploy/github/).

The important idea is simple: the workflow checks out your files, builds the Astro site, uploads the finished site, and deploys it to GitHub Pages. It runs on GitHub’s computers; you do not need to install anything locally.

If the theme already includes a Pages workflow, keep it and read its trigger line. Most workflows publish whenever you commit to the repository’s default branch, commonly `main` or `master`.

## 4. Enable GitHub Pages

Open your repository’s **Settings** tab. In the left sidebar, select **Pages**.

Under **Build and deployment**, choose **GitHub Actions** as the source. GitHub will then use the workflow you added instead of trying to publish source files directly.

Open the **Actions** tab and watch the first run. A green check mark means the build and deployment completed. The Pages settings screen will show a temporary GitHub address, usually similar to:

`https://your-name.github.io/your-repository/`

Visit it before changing the domain. This is a useful checkpoint: it confirms that your theme can build and that GitHub Pages is working.

## 5. Keep the site address accurate

Astro uses its `site` setting to make correct canonical links, RSS feeds, and sitemap entries. Themes store that setting in different places, so use the theme’s README to locate it.

If you publish on the default GitHub Pages address, use that address. If you later use a custom domain, replace it with the custom domain. For a project site hosted under a GitHub URL, Astro may also need the repository name as a `base` path; [Astro’s deployment guide](https://docs.astro.build/en/guides/deploy/github/) explains this distinction.

For a custom domain such as `blog.example.com`, the site lives at the domain root, so it should not keep a repository-name base path.

## 6. Connect a custom domain (Optional)

First, return to **Settings** → **Pages** in your GitHub repository. Under **Custom domain**, enter the address you want people to use for example, `blog.example.com` and save it.

Then open the DNS control panel where you manage your domain. The record depends on the kind of address you choose:

- For a subdomain such as `blog.example.com` or `www.example.com`, create a `CNAME` record that points to `your-name.github.io`.
- For the bare domain, such as `example.com`, create the GitHub Pages `A` records listed in [GitHub’s custom-domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

Do not add the repository name to the CNAME target. For example, `blog.example.com` should point to `your-name.github.io`, not `your-name.github.io/my-site`.

DNS changes are not instant. They can take several minutes and sometimes up to a day to appear everywhere. While you wait, leave the GitHub Pages custom-domain setting in place.

## 7. Enforce HTTPS

Once GitHub can see the correct DNS record, return to **Settings** → **Pages**. The **Enforce HTTPS** option will become available. Turn it on.

GitHub then provides and renews the certificate for you. Visitors will be sent to the secure `https://` version of your site automatically.

If the checkbox is unavailable, it usually means GitHub is still checking the DNS record or issuing the certificate. Check that the DNS record is spelled correctly, remove conflicting records for the same hostname, and give it some time. GitHub notes that certificate availability can take up to 24 hours after DNS is configured.

## 8. Publish future edits from the browser

After the first setup, the routine is pleasantly small:

1. Open a content or settings file in your repository.
2. Edit it in GitHub’s browser editor.
3. Commit the change to the publishing branch.
4. Wait for the Pages workflow to finish.

Your site updates automatically. The **Actions** tab is the first place to look if a change does not appear: a red mark means GitHub will show a readable log explaining which build step needs attention.

That is the whole loop: choose a theme, make it yours, save changes on GitHub, and let GitHub Pages handle the hosting. It is a calm way to begin publishing without turning your personal website into a complicated project.
