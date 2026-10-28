# Course knowledge base

Markdown notes, written in Obsidian, published as a website for students with [Quartz](https://quartz.jzhao.xyz). Every push to `main` rebuilds and republishes the site automatically through GitHub Actions and GitHub Pages.

```
content/            ← your Obsidian vault: everything you write lives here
  index.md          ← the home page
  lessons/          ← lesson pages
  resources/        ← glossary, links, reference material
  attachments/      ← images (Obsidian saves pasted images here)
  templates/        ← Obsidian templates (never published)
  private/          ← your own notes (never published)
quartz.config.yaml  ← site title, colours, language, features
.github/workflows/  ← the automatic build-and-publish job
```

Everything outside `content/` is the website engine. You don't need to touch it apart from `quartz.config.yaml`.

---

## One-time setup (about 10 minutes)

### 1. Create an empty repository on GitHub

On github.com, click **New repository**. Give it a name (for example `course-notes`), set it to **Public**, and **don't** add a README, .gitignore or licence. The site address will be:

```
https://YOUR-USERNAME.github.io/REPO-NAME
```

> GitHub Pages is free for public repositories. Publishing from a private repository needs a paid GitHub plan.

### 2. Put your details in the config

Open `quartz.config.yaml` in any text editor and change two lines:

- `baseUrl: YOUR-USERNAME.github.io/YOUR-REPO`: your address from step 1, without `https://`
- `Source on GitHub: https://github.com/YOUR-USERNAME/YOUR-REPO` (in the footer section): your repository link, or delete the line

You can also change `pageTitle: Course Notes` here.

### 3. Push the files to GitHub

This folder is already a Git repository with one commit on the `main` branch. Pick one of these options.

**With GitHub Desktop (no command line):** *File → Add local repository…*, choose this folder, then click **Publish repository**. Untick "Keep this code private" if you want the free plan, and make sure the name matches the one from step 1. (If you let GitHub Desktop create the repository here, you can skip step 1.)

**With the terminal:**

```bash
cd path/to/this/folder
git add -A
git commit -m "Set my site address"
git remote add origin https://github.com/YOUR-USERNAME/REPO-NAME.git
git push -u origin main
```

### 4. Turn on GitHub Pages

In the repository on GitHub, go to **Settings → Pages**. Under **Build and deployment → Source**, choose **GitHub Actions**.

Then go to the **Actions** tab, open **Deploy site to GitHub Pages**, and click **Run workflow** (or re-run the failed first run, which fails only because Pages wasn't on yet). After a minute or two the site is live at your address.

### 5. Open the notes in Obsidian

In Obsidian, choose **Open folder as vault** and select the **`content`** folder (not the whole repository). It comes with sensible settings: pasted images go to `attachments/`, new notes go to `lessons/`, and the Templates core plugin points at `templates/`.

---

## Everyday workflow

1. Write and edit in Obsidian.
2. Commit and push.
3. About a minute later, students see the update.

You can push in either of these ways:

- **GitHub Desktop:** write a short summary of what changed, click **Commit to main**, then **Push origin**.
- **The Obsidian Git community plugin:** install it from *Settings → Community plugins*. It adds a "Commit and sync" command, and it can push automatically every few minutes.

To check whether a publish succeeded, look at the **Actions** tab on GitHub: a green tick means it's live, a red cross means the build failed (click it to see why).

---

## Writing reference

| You want to… | Do this |
| --- | --- |
| Link to another page | `[[Page name]]` or `[[Page name\|text to show]]` |
| Link to a heading | `[[Glossary#Markdown]]` |
| Embed part of another page | `![[Glossary#Wikilink]]` |
| Add an image | Paste or drag it into Obsidian. PNG, JPG and GIF work as-is. **SVG** files need a relative markdown link instead, e.g. `![diagram](../attachments/diagram.svg)` from a page in `lessons/` |
| Highlight information | Callouts: `> [!tip]`, `> [!warning]`, `> [!question]`, `> [!important]` … |
| Hide an answer until clicked | Add `-` to a callout: `> [!success]- Show answer` |
| Keep a page unpublished for now | Add `draft: true` to its properties |
| Keep notes off the site permanently | Put them in `private/` |
| Group pages by topic | Add `tags` in the properties; each tag gets its own overview page |
| Set the page title shown on the site | Add `title:` in the properties (otherwise the file name is used) |
| Diagrams | ```` ```mermaid ```` code blocks |
| Maths | `$inline$` or `$$block$$` (LaTeX) |

`lessons/02 Working with Markdown.md` shows all of these in action.

> **Privacy note:** `private/`, `templates/` and drafts don't appear on the website, but in a public repository anyone can still read them on GitHub itself. Never put grades or student data in this repository.

---

## Customising the site

All of these settings are in `quartz.config.yaml`:

- **Title:** `pageTitle`
- **Language of the interface** (dates, "Search", "Table of Contents"…): `locale`, for example `nl-NL`, `fr-FR` or `en-GB`
- **Colours and fonts:** the `theme` section (any [Google Font](https://fonts.google.com) works)
- **Hide a sidebar element:** set `enabled: false` on its plugin, for example `@quartz-community/graph`
- **Analytics** are turned off. Turn them on with `analytics` if you want visitor statistics (check your school's privacy policy first).

Full documentation: <https://quartz.jzhao.xyz/configuration>

## Previewing locally (optional)

You don't need anything installed to publish, because GitHub does the building. To preview changes on your own computer first, install [Node.js](https://nodejs.org) 22 or later, then run:

```bash
npm ci
npx quartz build --serve
```

Open <http://localhost:8080>. The preview refreshes as you save in Obsidian.

---

Built with [Quartz](https://github.com/jackyzha0/quartz) (MIT licence, see `LICENSE.txt`).
