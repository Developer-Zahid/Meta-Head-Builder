# Meta Head Builder

Generate Meta, Open Graph, Twitter, JSON-LD and icons for any page.

Meta Head Builder is a single-page web tool that turns a form into a ready-to-paste `<head>` block. Fill in your site details once and get title and description tags, robots directives, Open Graph and Twitter/X cards, a linked JSON-LD `@graph`, and favicon links. It also crops your OG image and favicons and exports them as a zip.

**Live:** https://developer-zahid.github.io/Meta-Head-Builder/

It runs entirely in your browser. There is no build step, no backend and no sign-up, and images you upload never leave your computer.

---

## Contents

- [Use cases](#use-cases)
- [Features](#features)
  - [Form sections](#form-sections)
  - [Field inheritance](#field-inheritance)
  - [Smart URL handling](#smart-url-handling)
  - [Code output](#code-output)
  - [Previews](#previews)
  - [SEO checks](#seo-checks)
  - [Import from HTML](#import-from-html)
  - [Image & icon kit](#image--icon-kit)
  - [Autosave](#autosave)
- [How to use](#how-to-use)
- [Generated output reference](#generated-output-reference)
- [Keyboard and mouse controls](#keyboard-and-mouse-controls)
- [Browser support](#browser-support)
- [Privacy](#privacy)
- [Author](#author)

---

## Use cases

- **Launching a new site or landing page.** Produce the complete head block (SEO, social cards, structured data and icons) in one pass instead of copying it from an old project and editing it by hand.
- **Agency and client work.** Generate consistent, correctly linked tags for every client project. Use the Checks tab as a quick on-page SEO QA pass before launch.
- **Webflow, WordPress, Framer and other site builders.** Paste the output into the custom code "Inside `<head>`" field of a page or site.
- **Static sites and frameworks.** Drop the output into an HTML file, an Astro layout, or a Next.js or Nuxt document head.
- **Auditing an existing site.** Paste a live site's `<head>` into Import from HTML. Every tag is read back into the form, so you can see what's missing, fix it and copy a clean version.
- **Making social share images and favicons.** Crop one image to 1200 × 630 for Open Graph, and one logo into every favicon and app-icon size, without opening a design tool.
- **GitHub Pages and other sub-folder hosting.** Asset paths resolve inside the project folder (for example `user.github.io/project/`), not the domain root, so links don't 404.
- **Learning.** See how Open Graph, Twitter cards and Schema.org entities relate, with live previews and an explanation for every warning.

---

## Features

### Form sections

| Section | What it outputs |
|---|---|
| **Site & page** | Site name, Site URL, Page URL, `<title>`, meta description, language (`inLanguage`) and locale (`og:locale`). |
| **Search & browser** | `author`, canonical URL, robots (`index`/`noindex`, `follow`/`nofollow`, `max-image-preview`, `max-snippet`, extra directives), `theme-color`, `color-scheme`, and optional `charset` and `viewport` tags. |
| **Open Graph** | `og:type`, `og:site_name`, `og:locale`, `og:url`, `og:title`, `og:description`, `og:image`, `og:image:type`, `og:image:width`, `og:image:height` and `og:image:alt`. |
| **Twitter / X** | `twitter:card` (`summary_large_image` or `summary`), `twitter:site`, `twitter:creator`, title, description, image and image alt. |
| **Structured data** | A JSON-LD `@graph` with a **WebSite** entity, a main entity (**WebApplication**, **SoftwareApplication**, **MobileApplication** or **WebPage**) and an author (**Person** or **Organization**), all linked by `@id`. |
| **Icons** | Apple touch icon, PNG favicons (16 and 32), `favicon.ico`, SVG favicon and web manifest. |
| **Image & icon kit** | Crops and exports the OG image and every icon size as a zip. |

The Open Graph, Twitter, Structured data and Icons sections each have an on/off switch, so you only output what the page needs.

Structured data details:

- **Application fields:** `applicationCategory`, `applicationSubCategory`, `operatingSystem`, `browserRequirements`, `isAccessibleForFree`, an `Offer` (price and currency), `screenshot` and `featureList`.
- **Author fields:** `name`, `alternateName`, `url`, `email`, `logo` (organizations only) and a `sameAs` list of profile URLs.
- **Linking:** WebSite gets `publisher`. The main entity gets `author`, `creator` and `isPartOf`. Each points to the other entity's `@id` instead of repeating its data.
- **Comment:** an optional explanatory comment above the `<script>`, reminding you to validate at validator.schema.org.

### Field inheritance

Most values only need to be typed once. An empty field takes its value from its parent and shows that value greyed out, marked **inherited**:

| Field | Inherits from |
|---|---|
| Page URL | Site URL |
| Canonical URL, `og:url` | Page URL |
| `og:site_name` | Site name |
| `og:title` / `og:description` | Page title / Description |
| `twitter:title` / `twitter:description` | `og:title` / `og:description` |
| `twitter:image` / `twitter:image:alt` | `og:image` / `og:image:alt` |
| `twitter:creator` | `twitter:site` |
| JSON-LD name | Site name (apps) or Page title (WebPage) |
| JSON-LD screenshot | `og:image` |
| JSON-LD author name | Author |
| `og:image:type` | Detected from the image's file extension |

To override an inherited value, type into the field. To go back to inheriting, clear it.

### Smart URL handling

- **Relative paths become absolute URLs.** Type `assets/images/og-image.jpg` and the output contains the full URL. Social platforms need absolute URLs for images.
- **Sub-folder sites work.** A Site URL such as `https://user.github.io/project` is treated as a folder, so `assets/…` resolves to `https://user.github.io/project/assets/…`.
- **Domain-root paths.** Start a path with `/` when you mean the domain root, for example `/static/icon.png`.
- **Full URLs are left alone.** URLs on other domains, such as a CDN, are never rewritten.

### Code output

- **Syntax highlighting** for tags, attributes, strings, comments and JSON keys and values.
- **Line numbers**, and **Wrap lines** with a hanging indent, so long `content="…"` values stay readable.
- **All tags** or **JSON-LD only** view.
- **Comments** toggle for the section comments (`<!-- Open Graph -->` and so on).
- **Indent** of 0, 2 or 4 spaces, to match where you'll paste the code.
- **Copy code** in one click, with a line and character count.
- **Safe output:** all values are HTML-escaped, and `</script` inside JSON-LD is escaped so it can't break the page.

### Previews

- **Google search result:** favicon, site name, URL breadcrumb, title and description. The title is cut off at Google's real width limit, so you can see where yours gets truncated.
- **Facebook · LinkedIn · Slack:** the large link card at 1.91:1 with domain, title and description.
- **X (Twitter):** `summary_large_image` with the title on the image, or `summary` with a square thumbnail.

Images cropped in the Image & icon kit appear in the previews right away, including the favicon in the Google result.

### SEO checks

The **Checks** tab lists problems by severity (**Fix**, **Check**, **Note**). Each item has a **Go to field** button that jumps to the field. It catches:

- A missing Site URL, or one that isn't HTTPS.
- A missing, too short (under 30) or too long (over 60) title.
- A missing, too short (under 70) or too long (over 160) description.
- `noindex` or `nofollow` left on.
- An invalid `theme-color` value.
- An `og:locale` in the wrong format (it should look like `en_US`).
- Relative image or icon URLs with no Site URL to resolve them.
- Image problems:
  - a missing `og:image`
  - missing image alt text
  - missing width or height
  - an aspect ratio that isn't 1.91:1
  - an image under 1200px wide
- `og:url` and canonical pointing to different URLs.
- Twitter handles missing the `@`.
- A large-image card with no image.
- JSON-LD problems:
  - no entities at all
  - an author entity with no name
  - an invalid email
  - profile links that aren't absolute URLs
  - a missing `applicationCategory` or `Offer`, which Google uses for software rich results

Character counters under the title and description fields turn green inside the recommended range.

### Import from HTML

Paste the `<head>` of any page into **Import from HTML**. The tool reads back:

- `<title>`, description, author, robots, theme-color, color-scheme and canonical
- every `og:*` and `twitter:*` tag
- JSON-LD entities: WebSite, application or WebPage, and Person or Organization
- icon links: apple-touch-icon, PNG favicons, `.ico`, SVG and manifest

Values that only repeat what a field would inherit are cleared, so inheritance keeps working. URLs on the same site are turned back into relative paths.

### Image & icon kit

Upload an image, crop it, and export everything in one zip.

**OG image tab (1200 × 630)**

- Drop an image, or click to choose one.
- Drag to position it, and scroll or use the slider to zoom.
- **Fit** shows the whole image. **Fill** covers the whole frame.
- Export as **JPG** (quality 60–100) or **PNG**, with a background color for any empty areas.

**Favicon & app icons tab (square)**

- Use a separate logo, or click **Use OG image**.
- **Padding** adds space around the mark, shown as a dashed safe-area line.
- Choose a **Transparent** or solid background.
- Live previews show the icon in a browser tab mock-up and at its real 16, 32, 180 (iOS, rounded corners) and 192 (Android, round) pixel sizes.
- Small sizes are scaled down in halving steps, so 16px and 32px icons stay sharp instead of jagged.
- The Apple touch icon always gets the background color, because iOS shows transparent areas as black.

**Shared controls**

- **Remove image** clears an image from an editor.
- **Asset folder** (default `assets/images/`) sets where you'll upload the files. Typing a folder rewrites the icon and OG image paths in the form as you type, so the generated code always points to the files in the zip.
- **Download ZIP** contains:

| File | Size / content |
|---|---|
| `og-image.jpg` or `.png` | 1200 × 630 |
| `favicon.ico` | 16, 32 and 48 px (PNG-encoded) |
| `favicon-16x16.png` | 16 × 16 |
| `favicon-32x32.png` | 32 × 32 |
| `apple-touch-icon.png` | 180 × 180, solid background |
| `android-chrome-192x192.png` | 192 × 192 |
| `android-chrome-512x512.png` | 512 × 512 |
| `site.webmanifest` | name, icons, theme and background color, `display: standalone` |

### Autosave

The form saves itself to your browser's local storage as you type, so a reload doesn't lose your work. Uploaded images are kept in memory only and are not saved.

---

## How to use

1. **Site & page:** enter the site name, Site URL, page title and description.
2. **Image & icon kit:** upload and crop your OG image and logo, set the Asset folder, then click **Download ZIP**.
3. Upload the zip contents to that folder on your site.
4. Review the remaining sections: robots, Open Graph type, Twitter handles, structured data and author.
5. Open **Checks** and fix anything marked **Fix** or **Check**.
6. Open **Previews** to see how the page will look in Google and when shared.
7. Click **Copy code** and paste it inside your page's `<head>`.

**To update an existing site:** click **Import from HTML**, paste its current `<head>`, make your changes, then copy the new code.

---

## Generated output reference

An abridged example of the output for a site hosted in a sub-folder:

```html
<title>Meta Head Builder</title>
<meta name="description" content="Generate Meta, Open Graph, Twitter, JSON-LD and icons for any page">
<meta name="author" content="Developer Zahid">
<meta name="robots" content="index, follow, max-image-preview:large">
<meta name="theme-color" content="#171717">
<link href="https://developer-zahid.github.io/Meta-Head-Builder/" rel="canonical">

<!-- Open Graph -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://developer-zahid.github.io/Meta-Head-Builder/">
<meta property="og:image" content="https://developer-zahid.github.io/Meta-Head-Builder/assets/images/og-image.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">

<!-- Twitter / X -->
<meta name="twitter:card" content="summary_large_image">

<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@graph": [
      { "@type": "WebSite", "@id": "https://developer-zahid.github.io/Meta-Head-Builder/#website" },
      { "@type": "WebApplication", "@id": "https://developer-zahid.github.io/Meta-Head-Builder/#webapp" },
      { "@type": "Person", "@id": "https://developer-zahid.github.io/Meta-Head-Builder/#author" }
    ]
  }
</script>

<!-- Icons -->
<link rel="apple-touch-icon" sizes="180x180" href="https://developer-zahid.github.io/Meta-Head-Builder/assets/images/apple-touch-icon.png">
<link rel="icon" href="https://developer-zahid.github.io/Meta-Head-Builder/assets/images/favicon.ico" sizes="any">
<link rel="manifest" href="https://developer-zahid.github.io/Meta-Head-Builder/assets/images/site.webmanifest">
```

The real output includes every tag you've filled in, and each JSON-LD entity carries all of its fields.

---

## Keyboard and mouse controls

**Crop area (OG image and icon)**

| Action | Control |
|---|---|
| Choose a file | Click the empty area, or focus it and press **Enter** or **Space** |
| Move the image | Drag, or use the **arrow keys** (hold **Shift** for bigger steps) |
| Zoom | Mouse wheel, the **Zoom** slider, or **+** and **−** |
| Replace the image | Drop a new file onto the crop area |

**Elsewhere**

- **Esc** closes the Import dialog.
- The chips at the top of the form (`base`, `meta`, `og:*`, `twitter:*`, `JSON-LD`, `link rel`, `images`) jump to each section.

---

## Browser support

Current versions of Chrome, Edge, Firefox and Safari, on desktop and mobile.

**Copy code** uses the Clipboard API, which needs HTTPS (or `localhost`). On plain HTTP the tool selects the code so you can copy it with Ctrl/Cmd + C.

---

## Privacy

- Everything runs in your browser.
- Form values are saved only in your browser's local storage.
- Uploaded images are processed on a canvas in memory and are never uploaded anywhere.
- The only network requests are for the JSZip script and the web fonts.

---

## Author

**Developer Zahid** (Zahid Hasan Munna)

- GitHub: [@Developer-Zahid](https://github.com/Developer-Zahid)
- LinkedIn: [zahid-hasan-munna](https://www.linkedin.com/in/zahid-hasan-munna/)
- X: [@ZahidHa45112113](https://x.com/ZahidHa45112113)
- YouTube: [Frontend CSS Simplified](https://www.youtube.com/@frontend-css-simplified)
- CodePen: [DeveloperZahid](https://codepen.io/DeveloperZahid)
