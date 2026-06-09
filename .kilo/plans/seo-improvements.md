# SEO Improvements Plan

## Current State Analysis
- Jekyll site with basic SEO in `_includes/head.html`
- Open Graph and Twitter card tags present
- Canonical URL set
- No robots.txt or sitemap.xml
- No structured data (JSON-LD)
- Meta descriptions present but could be more specific per page
- No schema.org markup for organization/local business
- No hreflang tags for multilingual/multi-regional setup

## Priority SEO Improvements

### 1. Core Technical SEO

#### Add robots.txt
Create `robots.txt` in root with:
```
User-agent: *
Allow: /
Sitemap: https://evohomeloans.co.za/sitemap.xml
```

#### Add sitemap.xml
Enable in `_config.yml`:
```yaml
plugins:
  - jekyll-sitemap
```
Or create manual sitemap with calculator pages.

### 2. Structured Data (JSON-LD)

Add to `_includes/head.html` inside `<head>`:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FinancialService",
  "name": "Mortgage4U",
  "description": "{{ site.description }}",
  "url": "{{ site.url }}",
  "logo": "{{ "/assets/mortage4u-logo.png" | absolute_url }}",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "South Africa"
  },
  "telephone": "+27845476711",
  "email": "esme@mo4u.co.za",
  "areaServed": "ZA",
  "serviceType": ["Bond Origination", "Mortgage Broker", "Home Loan Application"]
}
</script>
```

### 3. Page-Specific Meta Descriptions

Update calculator pages with unique descriptions:

**affordability-calculator.md:**
```yaml
---
layout: page
title: Bond Affordability Calculator
description: "Calculate how much you can afford for your home loan. Determine your bond qualification amount based on income and expenses."
---
```

**bond-calculator.md:**
```yaml
---
layout: page
title: Bond Repayment Calculator  
description: "Calculate your monthly bond repayments. Enter property price and interest rate to estimate monthly home loan payments."
---
```

**amplification-calculator.md:**
```yaml
---
layout: page
title: Transfer Cost Calculator
description: "Calculate registration and transfer costs for South African property transactions. Estimate legal and transfer fees."
---
```

### 4. Open Graph Image Optimization

Current: Uses generic `social_916x509.jpg` for all pages

Add to `_config.yml`:
```yaml
defaults:
  - scope:
      path: ""
    values:
      image: "/social_916x509.jpg"
```

Or create page-specific images in frontmatter for key pages.

### 5. HTML Semantic Improvements

Update `_layouts/default.html`:
```html
<!DOCTYPE html>
<html lang="en-ZA">
<body id="page-top" class="d-flex flex-column min-vh-100">
  ...
</body>
</html>
```

### 6. Title Tag Optimization

Current: `{{ page.title | append: " | " | append: site.title }}`

Improve to handle missing titles:
```liquid
{% if page.title %}
  <title>{{ page.title }} | {{ site.title }}</title>
{% else %}
  <title>{{ site.title }} - {{ site.description }}</title>
{% endif %}
```

### 7. Meta Viewport & Mobile

Add to head for better mobile SEO:
```html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<meta name="format-detection" content="telephone=yes">
```

### 8. Structured Data for Calculator Pages

Each calculator page should include specific schema markup:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "{{ page.title }}",
  "description": "{{ page.description }}",
  "primaryImageOfPage": "{{ site.url }}{{ page.image }}",
  "breadcrumb": {
    "@type": "BreadcrumbList",
    "itemListElement": [{
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "{{ site.url }}/"
    },{
      "@type": "ListItem",
      "position": 2,
      "name": "{{ page.title }}"
    }]
  }
}
</script>
```

### 9. Local Business Markup

For SEO in South Africa, add geo-specific schema:
```json
{
  "address": {
    "@type": "PostalAddress",
    "addressCountry": "ZA",
    "addressRegion": "Western Cape"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": -33.9249,
    "longitude": 18.4241
  }
}
```

### 10. Performance SEO (Core Web Vitals)

- Preconnect to Google Fonts
- Add font-display swap (already using `&display=swap`)
- Optimize iframe loading for calculators:
```html
<iframe loading="lazy" ...>
```

### 11. Content SEO Improvements

**Calculators section** - Add FAQ structured data:
```json
{
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "How much can I borrow for a bond?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Use our affordability calculator to determine your qualification amount..."
    }
  }]
}
```

### 12. Analytics Verification Tags

Add to verify with search consoles:
```html
<meta name="google-site-verification" content="YOUR-VERIFICATION-ID">
<link rel="pingback" href="{{ site.url }}/pingback">
```

## Implementation Priority

1. **Done**: Add robots.txt and sitemap.xml
2. **Done**: Add JSON-LD organization schema with ZA region specifics
3. **Done**: Add page-specific meta descriptions for calculators
4. **Done**: Add FAQ structured data to calculator pages and contact page
5. **Medium**: Add semantic HTML attributes (lang, schema types)
6. **Low**: Optimize Open Graph images per section

## Completed Changes Summary

### Files Changed:
- `robots.txt` - Created with sitemap reference
- `_config.yml` - Added jekyll-sitemap plugin
- `Gemfile` - Added jekyll-sitemap gem
- `_layouts/default.html` - Added `lang="en-ZA"` attribute
- `_includes/head.html` - Added JSON-LD FinancialService schema, page-specific description handling, preconnect to fonts, FAQ schema for homepage
- `affordability-calculator.md` - Added description and FAQ schema
- `bond-calculator.md` - Added description, FAQ schema, loading="lazy" on iframe
- `deposit-savings-calculator.md` - Added FAQ schema and loading="lazy" on iframe
- `transfer-cost-calculator.md` - Added FAQ schema and loading="lazy" on iframe
- `amortisation-calculator.md` - Added FAQ schema and loading="lazy" on iframe
- `contact.md` - Added FAQ schema

## Expected SEO Impact

- Better indexing of calculator pages with unique descriptions
- Rich result eligibility for FAQ/pages
- Improved local SEO with ZA-specific markup
- Better mobile search ranking with viewport/format-detection
- Faster indexing with sitemap submission