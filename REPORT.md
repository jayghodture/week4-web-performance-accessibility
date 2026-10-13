# Week 4 Report: Web Page Performance and Accessibility

**Project:** Spoke & Chain Co-op (a simple one-page website for a community bike repair workshop)
**Files:** `index.html`, `styles.css`, `assets/hero-bike.svg`, `assets/workshop.svg`

## 1. Introduction

For this task I improved a static web page so that it loads faster and can be used by more people, including people who use screen readers or only a keyboard. I followed the WCAG 2.1 AA guidelines and checked the page using Lighthouse, WAVE and axe.

## 2. Problems found in the first version

Before making changes I tested the page and looked through the code. The main problems were:

- The page used `<div>` for everything, so screen readers could not find the header, menu or main content.
- Headings were chosen by how big they looked, and some levels were skipped.
- Images had no alt text and no width and height, which makes the page jump while loading.
- Some text colours were too light and failed the contrast check.
- There was no focus outline, so it was hard to see where you were when using Tab.
- Form fields used placeholders instead of labels.
- The CSS had a lot of repeated code.

## 3. Performance improvements

| Change | Why it helps |
|---|---|
| Put a small amount of critical CSS in the `<style>` tag in the head | The header and hero style load straight away without waiting for the CSS file |
| Used SVG images | They are very small (under 1 KB) and stay sharp at any size |
| Added `width` and `height` to images | The browser keeps space for the image, so the layout does not move (less CLS) |
| Added `loading="lazy"` to the image lower down the page | It only loads when the user scrolls near it |
| Used Arial instead of a Google font | No extra font download |
| Cleaned up the CSS using variables (`--navy`, `--yellow`) and simple class selectors | Less repeated code and easier to read |
| No JavaScript or libraries | Fewer files to download |

**For a real website I would also:**
- Minify the CSS and HTML (for example with `csso` and `html-minifier`).
- Convert photos to WebP and compress them (for example with Squoosh).
- Turn on gzip compression on the server.

## 4. Accessibility improvements

**Semantic HTML**
- Added `<header>`, `<nav>`, `<main>`, `<section>`, `<article>` and `<footer>`.
- Added `lang="en"` on the `<html>` tag.
- Used one `<h1>` and then headings in order (h2, h3).
- The opening hours use a proper `<table>` with `<caption>` and `scope` on the headings.

**Keyboard navigation**
- Added a "Skip to main content" link that appears when you press Tab.
- Added a clear focus outline for links, buttons and form fields.
- Everything can be reached with Tab and used with Enter or Space.

**ARIA and alt text**
- `aria-label="Main navigation"` on the menu.
- `aria-describedby` links the email field to its help text.
- Alt text added to both images describing what they show.
- I kept ARIA to a minimum because normal HTML elements already work well with screen readers.

**Forms**
- Every input has a `<label>` connected with `for` and `id`.
- Radio buttons are grouped using `<fieldset>` and `<legend>`.
- Added `required` and `autocomplete` attributes.

**Colour contrast**

| Colours | Ratio | Result |
|---|---|---|
| Dark text on light background | about 15:1 | Pass |
| White on navy | about 12.9:1 | Pass |
| Dark text on yellow | about 7.6:1 | Pass |

The minimum needed for normal text is 4.5:1. I checked these with the WebAIM contrast checker.

**Other**
- Smooth scrolling only turns on if the user has not asked for reduced motion.
- The layout is responsive and works on small screens.

## 5. Tools used

| Tool | Used for |
|---|---|
| Lighthouse (Chrome DevTools) | Performance and accessibility scores |
| WebPageTest | Checking load time and what blocks loading |
| WAVE | Finding missing alt text, labels and contrast problems |
| axe DevTools | Finding accessibility errors in the code |
| WebAIM Contrast Checker | Checking colour contrast |
| Keyboard testing (Tab key) | Checking focus order and the skip link |
| NVDA screen reader | Listening to how the page is read out |

## 6. Results

I have not filled in these numbers yet. Run Lighthouse on the old and new versions and add your scores.

| Measure | Before | After |
|---|---|---|
| Lighthouse Performance | | |
| Lighthouse Accessibility | | |
| Largest Contentful Paint (LCP) | | |
| Cumulative Layout Shift (CLS) | | |
| Page size | | |
| WAVE errors | | |

## 7. What I learned

- Using the right HTML elements fixes many accessibility problems without extra code.
- Performance and accessibility often help each other. For example, simple pages with fewer files are faster and easier to use.
- Automatic tools do not find everything, so testing with a keyboard and a screen reader is also needed.
- Setting image sizes is a simple change that stops the page jumping around.

## 8. Conclusion

The page is now more semantic, easier to navigate with a keyboard, has good colour contrast and loads fewer resources. In future I would add real photos in WebP format, minify the files and test with more users.
