---
title: "Reveals - Markdown Presentation Loader"
description: "Create instant reveal.js presentations from GitHub repositories with frontmatter support"
author: "The Tech Collective"
theme: "white"
transition: "slide"
separators:
  section: '\n\n---\n---\n\n'
  slide: '\n\n---\n\n'
---

![.tt](./techthat.png) <!-- .element style="height: 180px; margin: 0 auto 4rem auto; background: transparent;" -->

.tech that - this


![.t&do](../t&do.png) <!-- .element style="height: 180px; margin: 0 auto 4rem auto; background: transparent;" -->

.t&do - parent


![.t&do](/t&do.png) <!-- .element style="height: 180px; margin: 0 auto 4rem auto; background: transparent;" -->

.t&do - root

---

# 🎯 Reveals

## Markdown Presentation Loader

Create instant **reveal.js presentations** from GitHub repositories

---

## ✨ Features

- 📁 **Load from any GitHub repository**
- 🎨 **Frontmatter configuration support**
- 🖼️ **Automatic relative path resolution**
- 🎬 **Theme and transition customization**
- 📱 **Mobile-friendly interface**

---
---

# 🚀 Quick Start

---

## Basic Usage

1. **Navigate to the loader**

   ```text
   /markdownloader/
   ```

2. **Fill in repository details**
   - GitHub username/organization
   - Repository name  
   - Markdown filename (optional)

3. **Click Load** 🎉

---

## URL Format

```text
/markdownloader/?owner=USERNAME&repo=REPOSITORY&file=FILENAME
```

**Example:**

```text
/markdownloader/?owner=lakruzz&repo=presentations&file=demo.md
```

---
---

# 📝 Frontmatter Support

---

## Supported Fields

```yaml
---
title: "My Presentation"
description: "A great presentation"
author: "Your Name"
theme: "black"
transition: "fade"
separators:
  section: '\n\n---\n---\n\n'
  slide: '\n\n---\n\n'
---
```

---

---

## Metadata Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `title` | Page title | `"My Presentation"` |
| `description` | Meta description | `"About my topic"` |
| `author` | Meta author | `"Jane Doe"` |

---

## Theme Options

Available themes:

- `white` (default) - `black` - `league`
- `sky` - `beige` - `simple` - `serif`
- `blood` - `night` - `moon` - `solarized`

```yaml
theme: "black"
```

---

## Transition Options

Available transitions:

- `none` - `fade` - `slide` (default)
- `convex` - `concave` - `zoom`

```yaml
transition: "fade"
```

---

## Custom Separators

Override default slide separators:

```yaml
separators:
  section: '\n\n---\n---\n\n'  # Horizontal slides
  slide: '\n\n---\n\n'         # Vertical slides
```

---
---

# 🖼️ Image Support

---

## Relative Paths

The loader automatically converts relative paths to absolute GitHub URLs:

**In your markdown:**

```markdown
![My Image](./images/photo.jpg)
```

**Becomes:**

```markdown
![My Image](https://raw.githubusercontent.com/owner/repo/main/images/photo.jpg)
```

---

## Supported References

- **Markdown images:** `![alt](./path)`
- **Markdown links:** `[text](./path)`  
- **HTML src attributes:** `src="./path"`
- **HTML href attributes:** `href="./path"`

All `./` prefixed paths are automatically resolved!

---
---

# 🎨 Advanced Features

---

## Slide-Specific Backgrounds

Use reveal.js slide directives in your markdown:

```markdown
<!-- .slide: data-background="#ff0000" -->
# Red Background Slide

<!-- .slide: data-background="./background.jpg" -->
# Image Background Slide
```

---

## Element Styling

Style individual elements:

```markdown
![Logo](./logo.png) <!-- .element: style="height: 200px;" -->

<q>Quoted text</q> <!-- .element: style="color: blue;" -->
```

---
---

# 📚 Examples

---

## Example Repository Structure

```text
my-presentation/
├── presentation.md      # Main presentation
├── images/
│   ├── logo.png
│   └── chart.jpg
└── assets/
    └── data.json
```

---

## Example Markdown

```markdown
---
title: "My Talk"
theme: "black"
transition: "fade"
---

# Welcome

![Logo](./images/logo.png)

<!--section-->

# Section 2

![Chart](./images/chart.jpg)
```

---
---

# 🛠️ Development

---

## Repository Structure

- **`/site/`** - Deployable website files
- **Root** - Development tools and configuration

```bash
npm ci          # Install dependencies
npm run build   # Build the site
npm start       # Development server
```

---

## Building

The site builds reveal.js components into `/site/dist/`:

- CSS themes and core styles
- JavaScript modules and plugins  
- Optimized for production deployment

---
---

# 🎭 Try It Now

---

## View This Manual

This README.md is itself a reveal.js presentation!

**Try it:**

```text
/markdownloader/?owner=thetechcollective&repo=reveals&file=README.md
```

---

## Create Your Own

1. **Create a GitHub repository**
2. **Add a markdown file with frontmatter**
3. **Include relative image paths**
4. **Load it with the presentation loader**

---

**Happy presenting!** 🎉
