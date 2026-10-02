# Portfolio SEO & Google Discoverability Audit

**Portfolio URL:** `https://aryavengurlekar03.github.io/Machine-Learning/`  
**Repository:** `https://github.com/AryaVengurlekar03/Machine-Learning`  
**Author:** Arya Vengurlekar  
**Date:** October 2, 2026  

---

## 1. Executive Summary

This report documents the search engine optimization (SEO) and discoverability enhancements implemented for the portfolio website. All additions comply strictly with search engine guidelines (Googlebot/Bingbot), XML sitemap schema standards, and Schema.org structured data protocols.

No visual designs, CSS styles, contact form logic, or existing content were altered during this enhancement.

---

## 2. What Was Checked & Inspected

1. **HTML Head Structure (`index.html` & `resume.html`)**:
   * Verified title tags (`<title>Arya Vengurlekar | Machine Learning Engineer</title>` and `<title>Arya Vengurlekar — CV / Resume</title>`).
   * Verified meta descriptions, robots meta tags (`index, follow`), and canonical link URLs (`https://aryavengurlekar03.github.io/Machine-Learning/` and `.../resume.html`).
   * Verified Open Graph tags (`og:title`, `og:description`, `og:type`, `og:url`).

2. **Root Crawl Configuration (`robots.txt` & `sitemap.xml`)**:
   * Confirmed absence of prior `robots.txt` or `sitemap.xml` files in the repository root.
   * Created valid standards-compliant `sitemap.xml` and `robots.txt`.

3. **Structured Data Integration**:
   * Implemented Schema.org `Person` JSON-LD structured data in `index.html` referencing factual portfolio details (Name, Job Title, Employer, GitHub profile, LinkedIn profile).

---

## 3. Files Created & Modified

### Created Files:
1. **`sitemap.xml`** (Repository root)
   * XML sitemap specifying public site pages and priority hierarchy.
2. **`robots.txt`** (Repository root)
   * Web crawler configuration allowing unrestricted indexing and linking to `sitemap.xml`.
3. **`docs/SEO_DISCOVERABILITY.md`** (Documentation)
   * Audit log and discoverability report.

### Modified Files:
1. **`index.html`**
   * Added `Person` JSON-LD structured data block to `<head>`. Visual styling and layout remain 100% unchanged.

---

## 4. Sitemap & Crawl Configuration Details

### XML Sitemap (`sitemap.xml`)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://aryavengurlekar03.github.io/Machine-Learning/</loc>
    <lastmod>2026-10-02</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://aryavengurlekar03.github.io/Machine-Learning/resume.html</loc>
    <lastmod>2026-10-02</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
</urlset>
```

**Sitemap Verification**:
* Valid XML 1.0 syntax.
* Every URL corresponds to an existing, publicly accessible HTML document in the repository.

### Crawler Instructions (`robots.txt`)
```text
User-agent: *
Allow: /

Sitemap: https://aryavengurlekar03.github.io/Machine-Learning/sitemap.xml
```

**Robots Verification**:
* Grants full crawl permission (`Allow: /`) to all compliant search engine bots (`User-agent: *`).
* Contains **zero** `noindex` or `disallow` directives for public pages.
* Explicitly declares the absolute HTTPS URL of the XML sitemap.

---

## 5. Canonical & Metadata Status

* **Homepage Canonical (`index.html`)**: `https://aryavengurlekar03.github.io/Machine-Learning/`
* **Resume Page Canonical (`resume.html`)**: `https://aryavengurlekar03.github.io/Machine-Learning/resume.html`
* **Robots Meta Tag**: `<meta name="robots" content="index, follow">` present on both pages.

---

## 6. Structured Data (JSON-LD Schema)

Added to `index.html` head section:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Arya Vengurlekar",
  "url": "https://aryavengurlekar03.github.io/Machine-Learning/",
  "jobTitle": "Machine Learning Engineer",
  "worksFor": {
    "@type": "Organization",
    "name": "FlyRank"
  },
  "sameAs": [
    "https://github.com/AryaVengurlekar03",
    "https://linkedin.com/in/aryavengurlekar"
  ]
}
</script>
```

---

## 7. Indexing & Google Search Console Requirements

> [!IMPORTANT]
> **Local vs. Live Verification Disclaimer:**
> Local static testing verifies XML syntax, canonical tags, and HTML structure. However, search engine indexing **cannot** be verified locally. Google Search Console setup and sitemap submission must be performed manually by the site owner.

### Manual Actions Required in Google Search Console:
1. **Property Setup**:
   * Open [Google Search Console](https://search.google.com/search-console).
   * Add URL prefix property: `https://aryavengurlekar03.github.io/Machine-Learning/`.
   * Verify ownership via HTML tag or GitHub Pages DNS/file verification.
2. **Sitemap Submission**:
   * Navigate to **Sitemaps** in the left sidebar.
   * Submit sitemap URL: `sitemap.xml` (Full path: `https://aryavengurlekar03.github.io/Machine-Learning/sitemap.xml`).
3. **Request Indexing**:
   * Use the **URL Inspection Tool** to inspect `https://aryavengurlekar03.github.io/Machine-Learning/`.
   * Click **Request Indexing** to queue the site for Googlebot crawling.
