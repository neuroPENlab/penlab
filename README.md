# PENLab Website

Official website of the Pain and Emotion Neuroscience Lab (PENLab), led by Dr. Marina López-Solà at the University of Barcelona.

**Live site:** [neuropenlab.github.io/penlab](https://neuropenlab.github.io/penlab)

---

## How the site works

The site is built with **Jekyll** and published automatically via **GitHub Pages**. This means:

1. Edit a `.md` (Markdown) or `.html` file inside the `docs/` folder
2. Run `git push` to the `main` branch
3. GitHub Pages rebuilds the site automatically in ~1–2 minutes

No local installation or build commands are needed to publish changes.

---

## Folder structure

```
penlab/
├── README.md                   ← This file
└── docs/                       ← All site content lives here
    ├── _config.yml             ← Global settings (title, URL, colors, nav menu...)
    ├── index.html              ← Home page
    ├── about.md                ← About page
    ├── vision.md               ← Vision page
    ├── news.md                 ← ⭐ Lab news
    ├── publications.md         ← ⭐ Publication list
    ├── personnel.md            ← ⭐ Main personnel page (photo cards)
    ├── contact.md              ← Contact page
    ├── resources.md            ← External resources
    │
    ├── personnel/              ← Detailed pages per personnel category
    │   ├── lab-director.md
    │   ├── postdocs.md
    │   ├── graduate-students.md
    │   ├── staff.md
    │   └── undergraduate.md
    │
    ├── research/               ← Research section
    │   ├── projects.md
    │   ├── codes.md
    │   └── participation.md
    │
    ├── lab-stories/            ← Lab Stories section
    │   ├── videos.md
    │   ├── art-gallery.md
    │   └── media.md
    │
    └── assets/                 ← Static files
        ├── img/
        │   ├── penlab-banner.jpg          ← Main banner image
        │   └── personnel/                 ← ⭐ Personnel photos
        │       ├── marina-lopez-sola.jpg
        │       ├── maria-sunol.jpg
        │       └── ...
        ├── pdf/                           ← Publication PDFs
        └── css/ / js/                     ← Custom styles and scripts
```

---

## Common tasks

### Add a news item

Edit `docs/news.md`. News items are organized by year using `##` headings.

**Format:**

```markdown
## 2025

### Event or news title
**Month Day, Year**

Brief description of the news item. You can use *italics* and **bold**.

---
```

**Example:**

```markdown
## 2025

### Neuroscience Conference — Barcelona
**March 12, 2025**

Dr. López-Solà presented results from the SPRINT project at the European
Congress of Pain Neuroscience, held at the CCIB in Barcelona.

---
```

Add new items just **below the corresponding year heading**. If the year doesn't exist yet, add a new `## YEAR` heading at the top of the list.

---

### Add a publication

Edit `docs/publications.md`. Publications are organized by year with continuous numbering across years.

**Basic format (DOI only):**

```markdown
1. Surname N, López-Solà M\*. Article title. ***Journal Name***. Year;Vol(Num):pages.
[[DOI]](https://doi.org/XXXXXXX){:target="_blank" .pub-link}
```

**Full format (DOI + downloadable PDF + Press release):**

```markdown
1. Surname N, López-Solà M\*. Article title. ***Journal Name***. Year;Vol(Num):pages.
[[DOI]](https://doi.org/XXXXXXX){:target="_blank" .pub-link}
[[Download]]({{ site.baseurl }}/assets/pdf/Surname_Year_Journal_keyword.pdf){:target="_blank" .pub-link}
[[Press]](https://url-to-press-release){:target="_blank" .pub-link}
```

**Important notes:**
- The `\*` after a name marks the corresponding author (renders as `*` without breaking Markdown).
- Journal names go in `***bold italic***`.
- If adding a downloadable PDF, upload the file to `docs/assets/pdf/` first, using a descriptive name like `Surname_Year_Journal_keyword.pdf`.
- Since numbering is continuous across years, use `{:start="N"}` before the first entry of each year (except the first year in the file) to keep numbers correct:

```markdown
## 2024

{:start="4"}
4. Surname N, ...
```

---

### Change a personnel photo

1. **Prepare the photo:**
   - Recommended format: JPG or PNG
   - Minimum size: **200×200 px** (displayed cropped as a 180×180 px circle)
   - File name: use hyphens instead of spaces, all lowercase — e.g. `firstname-lastname.jpg`

2. **Upload the photo** to `docs/assets/img/personnel/`

3. **Update the reference** in `docs/personnel.md` by finding the person's card block and changing the filename:

```html
<img src="{{ '/assets/img/personnel/firstname-lastname.jpg' | relative_url }}" ...>
```

---

### Add a new team member

You need to edit **two files**: `docs/personnel.md` (main page with photo cards) and the relevant file inside `docs/personnel/`.

#### 1. Add the card in `docs/personnel.md`

Copy the block below into the correct section (`## Post-doctoral Fellows`, `## Graduate Students`, etc.) and fill in the details:

```html
<div class="person-card" style="display: flex; gap: 25px; margin-bottom: 40px; padding: 25px; background: #f8f9fa; border-radius: 10px;">
  <div style="flex-shrink: 0;">
    <img src="{{ '/assets/img/personnel/firstname-lastname.jpg' | relative_url }}" alt="Full Name" style="width: 180px; height: 180px; border-radius: 50%; object-fit: cover;">
  </div>
  <div>
    <h3 style="margin-top: 0;">Full Name</h3>
    <p><strong>Role / Category</strong> — Joined Month Year</p>
    <p>Brief description of the person and their background.</p>
    <p>Current research interests or projects.</p>
    <p>📧 <a href="mailto:email@ub.edu">email@ub.edu</a></p>
  </div>
</div>
```

Remember to upload the photo to `docs/assets/img/personnel/` first (see section above).

#### 2. Add the detailed profile in `docs/personnel/`

Add the entry in the file matching their category (e.g. `docs/personnel/graduate-students.md`):

```markdown
## Full Name

**Role** — Joined Month Year

Description of the person, their background, and research projects.
```

---

### Remove a team member

1. Delete their `<div class="person-card">...</div>` block from `docs/personnel.md`
2. Delete their section from the corresponding file in `docs/personnel/`
3. Optionally, delete their photo from `docs/assets/img/personnel/` if no longer needed

---

### Change the main banner image

Replace `docs/assets/img/penlab-banner.jpg` with the new image (keeping the same filename), or upload a new image and update the path in `docs/index.html`:

```yaml
cover-img: "/assets/img/new-banner.jpg"
```

---

### Edit the navigation menu

Edit the `navbar-links` section in `docs/_config.yml`. Items without a submenu are simple `Name: "path"` pairs. Items with a submenu use an indented list:

```yaml
navbar-links:
  About:
    - About: "/"
    - Vision: "vision"
  News: "news"
  Personnel: "personnel"
```

Paths are relative to `baseurl` (`/penlab`), so `"news"` points to `neuropenlab.github.io/penlab/news`.

---

## Basic Markdown syntax

| Element | Syntax |
|---|---|
| Large heading | `## Heading` |
| Subheading | `### Subheading` |
| **Bold** | `**text**` |
| *Italic* | `*text*` |
| ***Bold italic*** | `***text***` |
| [Link](URL) | `[text](https://url.com)` |
| Horizontal rule | `---` |
| Bullet list | `- item` |
| Numbered list | `1. item` |

`.md` files are automatically converted to HTML when the site is published.

---

## Global configuration (`_config.yml`)

This file controls site-wide settings. The most relevant fields:

| Field | Description |
|---|---|
| `title` | Site name (shown in the browser tab) |
| `subtitle` | Secondary title shown below the main title |
| `url` | Base domain: `https://neuropenlab.github.io` |
| `baseurl` | Site subpath: `/penlab` |
| `email` | Lab contact email |
| `navbar-links` | Navigation menu structure |
| `navbar-col` | Navigation bar background color |
| `hover-col` | Link hover highlight color |

> ⚠️ **Caution:** Changing `url` or `baseurl` will break all internal links on the site. Only modify these if the repository or GitHub organization changes.

---

## FAQ

**How long does it take for a change to go live?**
Between 1 and 3 minutes after `git push`. You can monitor the status under the *Actions* tab of the repository on GitHub.

**Can I edit files directly on GitHub without cloning the repo?**
Yes. Navigate to the file on github.com, click the pencil icon (✏️), make your edits, and click *Commit changes*. The site will update automatically.

**What if something breaks?**
Go to the commit history on GitHub and click *Revert* on the commit that caused the issue. The previous version of the site will remain live until the new build completes.

**Where can I see build errors?**
Under the *Actions* tab of the repository on GitHub. A failed build will appear in red with a detailed error message.
