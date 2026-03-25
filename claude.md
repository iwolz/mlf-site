# Omolola's Website — Project Context

## What this project is

A personal website and blog for Omolola Omolambe, built as a birthday gift by Wole.
The site showcases her work as a Senior Software Engineer at Checkout.com and hosts her writing.

The site is modelled on the format of [timdietrich.me](https://timdietrich.me) — clean,
editorial, personal brand style with a writing/blog section at its core.

---

## Live URLs

| | |
|---|---|
| **Live site** | https://omololaomolambe.com |
| **CMS admin** | https://omololaomolambe.com/admin |
| **GitHub repo** | https://github.com/iwolz/mlf-site |
| **Netlify dashboard** | app.netlify.com (logged in as woleolorunleke@gmail.com) |
| **Namecheap domain** | omololaomolambe.com — registered, pointing to Netlify DNS |

---

## Tech stack

- **Single HTML file** — the entire site is `index.html`. No framework, no build step.
- **Hosting** — Netlify (free tier), connected to GitHub. Auto-deploys on every push.
- **CMS** — Netlify CMS (Decap CMS) at `/admin`. Uses Netlify Identity + Git Gateway.
- **Blog posts** — stored as markdown files in `/posts/` folder in the GitHub repo.
- **Post rendering** — the site fetches posts from the GitHub API at runtime and renders them client-side using `marked.js`.
- **DNS** — Namecheap domain, nameservers pointing to Netlify.
- **SSL** — auto-provisioned by Netlify via Let's Encrypt.

---

## Local development setup

- **Local folder** — `C:/Users/woleo/OneDrive/Documents/mlf-site` (cloned from GitHub)
- **Editor** — VS Code with Live Server extension (Ritwick Dey)
- **Local preview** — open `index.html` → click "Go Live" → runs at `127.0.0.1:5500`
- **Git** — connected, auto-stages on commit. Push via Ctrl+Shift+G → Commit → Sync.

> **Note:** Live Server shows "No posts yet" because posts are fetched from the GitHub API,
> not the local filesystem. To preview a new post, push it to GitHub first.

---

## Repo structure

```
mlf-site/
├── index.html          ← entire site (HTML + CSS + JS in one file)
├── admin/
│   ├── config.yml      ← Netlify CMS configuration
│   └── index.html      ← CMS admin interface loader
├── posts/
│   ├── .gitkeep
│   └── 2026-03-05-my-first-post.md   ← example post
├── images/
│   └── .gitkeep        ← store post images here
└── README.md
```

---

## How to create a blog post

### Option A — Via VS Code (developer workflow)

1. Create a new `.md` file in the `posts/` folder
2. Name it: `YYYY-MM-DD-post-title.md`
3. Use this frontmatter template:

```markdown
---
title: "Your Post Title"
date: 2026-03-05
tag: Engineering
---

Your post content here in markdown.

## Section heading

Paragraph text.

- Bullet point
- Another point

`inline code` and code blocks work too.
```

4. Save → commit → sync → live within 30 seconds

### Option B — Via CMS (no-code workflow, for Omolola)

1. Go to `omololaomolambe.com/admin`
2. Log in with Netlify Identity credentials
3. Click **New Post** → fill in title, date, tag, and body
4. Click **Publish** → auto-commits to GitHub → Netlify deploys

### Available tags
`Engineering` | `Payments` | `Career` | `Books` | `Learning`

---

## How to add images to posts

1. Copy image file into `images/` folder in local `mlf-site`
2. Compress images to under 500KB at [squoosh.app](https://squoosh.app)
3. Name files with hyphens, no spaces: `event-flow-diagram.png`
4. Reference in markdown:

```markdown
![Description of image](../images/your-image-name.png)
```

5. Commit and sync

---

## Site design

### Colour palette (CSS variables in `:root` block at top of `index.html`)

The entire colour scheme is controlled by these variables — change only these to retheme:

```css
:root {
  --ink:       #12110f;    /* main text */
  --muted:     #5c574f;    /* secondary text */
  --faint:     #a09a90;    /* dates, labels */
  --rule:      #e6e0d5;    /* borders and dividers */
  --bg:        #f7f4ef;    /* page background */
  --surface:   #edeae3;    /* card backgrounds */
  --surface2:  #e4dfd6;    /* deeper card tone */
  --accent:    #b85c38;    /* primary colour — buttons, active nav */
  --accent2:   #2a7c8a;    /* secondary colour — about page links */
  --sage:      #7a9e8a;    /* eyebrow labels */
  --serif:     'Playfair Display', Georgia, serif;
  --sans:      'Instrument Sans', system-ui, sans-serif;
}
```

**Tested alternative palettes:**

Cool sage & blue (current deployed version):
```css
--ink: #1c2b2b; --muted: #4a5e5e; --faint: #8fa8a8;
--rule: #d4e2e0; --bg: #f2f7f6; --surface: #e8f0ef;
--surface2: #dceae8; --accent: #3d7a6f; --accent2: #5b8fa8; --sage: #6b9e8f;
```

Warm parchment (original v1):
```css
--ink: #12110f; --muted: #5c574f; --faint: #a09a90;
--rule: #e6e0d5; --bg: #f7f4ef; --surface: #edeae3;
--surface2: #e4dfd6; --accent: #b85c38; --accent2: #2a7c8a; --sage: #7a9e8a;
```

Slate & lavender:
```css
--ink: #1e1e2e; --muted: #4a4a6a; --faint: #9090b0;
--rule: #d8d8e8; --bg: #f4f4f8; --surface: #ebebf4;
--surface2: #e0e0f0; --accent: #5a4a9e; --accent2: #7a6ab0; --sage: #7a7aaa;
```

### Typography

- **Headings** — Playfair Display (Google Fonts)
- **Body** — Instrument Sans (Google Fonts)
- To change fonts: update `--serif` and `--sans` in `:root` AND update the Google Fonts `<link>` at the top of `index.html`

---

## Pages

| Page | Description |
|------|-------------|
| **Home** | Hero, areas of focus, latest 3 posts |
| **Writing** | Full post list + post reader (click to open post inline) |
| **Now** | Currently reading (with progress bars), building, life, thinking |
| **About** | Bio, skill tags, GitHub/LinkedIn/Medium/email links |

Navigation is handled client-side — all pages are in one HTML file, shown/hidden via JavaScript.

---

## Netlify CMS config (`admin/config.yml`)

```yaml
backend:
  name: github
  repo: iwolz/mlf-site
  branch: main

media_folder: "images"

collections:
  - name: "posts"
    label: "Posts"
    folder: "posts"
    create: true
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "Date", name: "date", widget: "datetime" }
      - { label: "Tag", name: "tag", widget: "select", options: ["Engineering", "Payments", "Career", "Books", "Learning"] }
      - { label: "Body", name: "body", widget: "markdown" }
```

---

## Netlify Identity

- Registration: **Invite only**
- Git Gateway: **Enabled** (connects CMS to GitHub)
- Invited user: woleolorunleke@gmail.com (to be transferred to Omolola's email after launch)

---

## Medium cross-posting workflow

Once a post is live on the site:
1. Go to Medium → **Stories → Import a story**
2. Paste the post URL e.g. `https://omololaomolambe.com`
3. Medium imports and sets the **canonical URL** back to her site
4. This protects SEO — Google treats her site as the original source

---

## Known issues / outstanding items

- [ ] Post clicking from Home page required a fix to `openPost()` to switch to Writing page first before showing post reader
- [ ] Profile photo placeholder (OO initials) — to be replaced with real photo when Omolola is ready
- [ ] GitHub/LinkedIn/Medium URLs in About page still use placeholder paths — need real URLs
- [ ] Netlify Identity invite to be re-sent to Omolola's own email before birthday reveal
- [ ] Now page content is placeholder — update with real books and life updates before launch
- [ ] DNS propagation for omololaomolambe.com — confirm SSL is fully provisioned

---

## How to update the Now page

Find the `page-now` div in `index.html`. Update:
- Book titles, authors and `width` percentage in `style="width:XX%"` for reading progress
- Life and thinking sections are plain `<li>` items — just edit the text
- Update the "Last updated" date at the bottom

---

## Git commit workflow

```
Ctrl+Shift+G       → open Source Control panel
Type message       → e.g. "update now page"
Click Commit       → stages and commits
Click Sync         → pushes to GitHub → Netlify auto-deploys
```

Netlify deploys within ~30 seconds of a push.

---

## Reverting to a previous version

1. Go to `github.com/iwolz/mlf-site` → click `index.html` → click **History**
2. Click `<>` on any commit to view that version
3. Click **Raw** → select all → copy
4. Edit current `index.html` on GitHub → paste → commit