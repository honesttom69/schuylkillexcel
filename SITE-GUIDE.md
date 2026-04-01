# SchuylkillExcel.com -- Site Management Guide

## Quick Reference
- **Live site:** https://honesttom69.github.io/schuylkillexcel/
- **GitHub repo:** https://github.com/honesttom69/schuylkillexcel
- **Site files on homelab:** C:\Users\tomdh\schuylkillexcel\
- **How it deploys:** Push to GitHub -> GitHub Actions builds -> live in ~60 seconds

---

## SOP: Write a New Blog Post

### Step 1: Create the file

Create a new .md file in C:\Users\tomdh\schuylkillexcel\content\blogs\

Naming: use-lowercase-with-dashes.md (e.g., my-ai-morning-briefing.md)

### Step 2: Add frontmatter

Every post starts with this header:

```yaml
---
title: "Your Post Title Here"
date: 2026-04-01
draft: false
author: "Tom Hinkle"
tags:
  - AI
  - Operations
  - Whatever fits
description: "One sentence summary for SEO and social previews."
toc: false
---
```

- Set draft: true if you want to write it but not publish yet
- Tags show up on the blog page as filters
- Description appears in link previews when shared on LinkedIn

### Step 3: Write the post

Regular markdown below the frontmatter. You can use:

- ## Headings for sections
- **bold** and *italic*
- Bullet lists
- Numbered lists
- [link text](url) for links
- ![alt text](/images/filename.jpg) for images (put images in static/images/)

### Step 4: Preview locally (optional)

```bash
cd C:\Users\tomdh\schuylkillexcel
hugo server
```

Open http://localhost:1313 to preview. Ctrl+C to stop.

### Step 5: Publish

```bash
cd C:\Users\tomdh\schuylkillexcel
git add .
git commit -m "New post: whatever the title is"
git push
```

Live in ~60 seconds at the blog URL.

---

## SOP: Edit the Homepage

Edit C:\Users\tomdh\schuylkillexcel\hugo.toml

All homepage content is in this one file:
- Hero section: [params.hero] -- intro text, button, social links
- About section: [params.about] -- bio, skills list
- Experience: [[params.experience.items]] -- job entries
- Services: [[params.projects.items]] -- service offerings
- Contact: [params.contact] -- email/booking link

After editing, push to deploy:

```bash
cd C:\Users\tomdh\schuylkillexcel
git add hugo.toml
git commit -m "Update homepage content"
git push
```

---

## SOP: Add Images

1. Put the image in C:\Users\tomdh\schuylkillexcel\static\images\
2. Reference it as /images/filename.jpg in your post or in hugo.toml
3. Push to deploy

Headshot: Replace static/images/headshot.jpg -- it shows in the hero and about sections automatically.

Blog post images: Add to static/images/ and reference in the post:

```markdown
![Description of image](/images/my-image.jpg)
```

---

## SOP: Ask Claude to Do It

You can also just tell Claude Code:
- "Write a blog post about [topic] and publish it"
- "Update the homepage services section"
- "Add this image to the site"

Claude has access to the site files and can push to GitHub directly.

---

## LinkedIn Workflow

1. Write the full post on the blog (or have Claude write it)
2. Publish it (push to GitHub)
3. On LinkedIn, write a short commentary/hook (2-3 paragraphs)
4. Put the blog link in the FIRST COMMENT, not the post body (links in the post kill reach)
5. In the post, say something like "Full writeup in the comments" or "Link below"

Blog post URL format: https://honesttom69.github.io/schuylkillexcel/blogs/post-filename-without-md/

---

## Custom Domain (When Ready)

When you transfer schuylkillexcel.com from Bluehost:

1. In the GitHub repo: Settings -> Pages -> Custom domain -> enter schuylkillexcel.com
2. At your domain registrar, add these DNS records:
   - A record: 185.199.108.153
   - A record: 185.199.109.153
   - A record: 185.199.110.153
   - A record: 185.199.111.153
   - CNAME record: www -> honesttom69.github.io
3. Check "Enforce HTTPS" in GitHub Pages settings
4. Update baseURL in hugo.toml to https://schuylkillexcel.com/

---

## File Structure

```
C:\Users\tomdh\schuylkillexcel\
  hugo.toml                  -- All homepage config
  content/
    blogs/
      _index.md              -- Blog listing page
      *.md                   -- Individual posts
  static/
    images/
      headshot.jpg           -- Your photo
  themes/
    hugo-profile/            -- Theme (don't edit)
  .github/
    workflows/
      hugo.yml               -- Auto-deploy config
```

---

## Troubleshooting

**Site not updating after push?**
Check https://github.com/honesttom69/schuylkillexcel/actions for build status.
Build takes ~60 seconds.

**Post not showing up?**
- Make sure draft: false in frontmatter
- Make sure date is today or in the past (future dates are hidden)

**Broken layout?**
- Check hugo.toml for syntax errors (missing quotes, brackets)
- Run hugo server locally to see error messages

**Need to undo a change?**

```bash
cd C:\Users\tomdh\schuylkillexcel
git log --oneline        # find the commit to go back to
git revert HEAD          # undo last commit safely
git push
```
