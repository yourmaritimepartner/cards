# CLAUDE.md - Shipwright Digital Business Cards

## Project Overview

This is a static website for **Shipwright**, a maritime services company, that hosts digital business cards for team members. The site is deployed via GitHub Pages at `cards.shipwright.biz`.

## Tech Stack

- **Static HTML/CSS** - No build system required
- **GitHub Pages** - Hosting
- **Node.js** - Asset generation only (QR codes, vCards)
- **Google Fonts** - Libre Caslon Text for headings

## Directory Structure

```
/
├── index.html              # Team directory page
├── styles.css              # Shared styles for all pages
├── generate-assets.js      # Node script to generate QR codes and vCards
├── package.json            # qrcode dependency for asset generation
├── CNAME                   # Custom domain: cards.shipwright.biz
├── [name].html             # Individual card pages (logo variant)
├── [name]-photo.html       # Individual card pages (avatar variant)
└── assets/
    ├── shipwright-header.jpg   # Banner image used on all cards
    ├── qr/
    │   └── [name]-qr.png       # QR codes linking to card URLs
    └── vcards/
        └── [name].vcf          # vCard files for contact download
```

## Card Page Variants

There are two HTML templates for individual cards:

### 1. Logo Variant (`[name].html`)
- Uses `.logo-wrapper` with company logo centered below banner
- Simpler design, no avatar
- Example: `spencer-barnes.html`

### 2. Avatar Variant (`[name]-photo.html`)
- Uses `.avatar-wrapper` with circular avatar (initials or photo)
- Small `.logo-badge` overlaying the avatar
- For employees with photos or who want the avatar style
- Example: `john-dixon-photo.html`

## Naming Conventions

- **File names**: `firstname-lastname.html` (lowercase, hyphenated)
- **URL slugs**: Same as filename (e.g., `cards.shipwright.biz/spencer-barnes.html`)
- **Assets**: `[slug]-qr.png`, `[slug].vcf`

## Brand Colors (CSS Variables)

```css
--color-primary: #c94a4a;     /* Red - CTA buttons */
--color-navy: #1a3a5c;        /* Navy - Headings, QR codes */
--color-teal: #2a7d8c;        /* Teal - Accent, links */
--color-text: #4a4a4a;        /* Body text */
--color-text-muted: #6b7280;  /* Secondary text */
```

## Adding a New Team Member

1. **Add employee data** to `generate-assets.js`:
   ```javascript
   {
     firstName: 'New',
     lastName: 'Person',
     email: 'nperson@shipwright.biz',
     phone: '555-123-4567',
     linkedin: 'https://www.linkedin.com/company/shipwright/',
     website: 'https://www.shipwright.biz'
   }
   ```

2. **Generate assets**:
   ```bash
   npm install  # First time only
   node generate-assets.js
   ```
   This creates:
   - `assets/qr/new-person-qr.png`
   - `assets/vcards/new-person.vcf`

3. **Create HTML card page** - Copy an existing card and update:
   - Title and meta description
   - Name in `<h1>`
   - Email link (both href and display text)
   - Phone link (both href and display text)
   - vCard download link and filename
   - QR code image src

4. **Add to index.html** - Add entry to `.card-grid` section:
   ```html
   <div class="employee-card">
     <h2>New Person</h2>
     <div class="contact">
       <a href="mailto:nperson@shipwright.biz">nperson@shipwright.biz</a>
       <a href="tel:+15551234567">(555) 123-4567</a>
     </div>
     <div class="card-links">
       <a href="new-person.html">View Card →</a>
     </div>
   </div>
   ```

## Key Files to Understand

- **`index.html`** - Contains inline styles for the team directory layout plus leader-row for principals
- **`styles.css`** - Shared card page styles, responsive breakpoints at 480px
- **`generate-assets.js`** - Contains `employees` array (source of truth for contact data)

## Phone Number Formatting

- Display format: `(XXX) XXX-XXXX`
- Tel link format: `+1XXXXXXXXXX` (no dashes)

## External Resources

- Company logo: Hosted on Squarespace CDN
- Google Fonts: Libre Caslon Text
- Favicon: Inline SVG anchor emoji

## Special Index.html Features

- **Leader row**: John Dixon and Corey Page displayed prominently with ", P.E." suffix
- **Card grid**: All other team members
- **Footer**: Office address and main phone number

## Development Workflow

1. No build step required - edit HTML/CSS directly
2. Test locally by opening HTML files in browser
3. Commit and push to deploy via GitHub Pages

## Important Notes

- The `generate-assets.js` employee list may be out of sync with actual HTML files - always verify both when adding/removing employees
- Some employees have both `.html` and `-photo.html` variants
- The company logo is externally hosted - do not modify the Squarespace URL
