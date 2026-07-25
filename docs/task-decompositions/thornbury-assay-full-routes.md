# Task Decomposition: Thornbury Assay — Full Route Coverage

**Project ID:** 1339a90c-6f41-4da7-bb4c-a4b3bc061048  
**Pipeline Run:** c9705bf4-f2a0-41a7-9865-0516760866aa  
**Branch:** ticket-fix/b99e0f38  
**Target Repo:** AEGIS-OSX/thornbury-assay  

## Approved Upstream Deliverables

| Type | Deliverable ID | Status |
|------|---------------|--------|
| Design Tokens | 59de44ad-0ca8-4673-870b-17b939fb51d1 | approved |
| Copy | b8a68292-4e48-4cb6-bc82-8c9192c13753 | approved |

## Tech Stack Context

- Next.js 14.2.5 (App Router, static export via `output: 'export'`)
- React 18.3.1, TypeScript 5.5.3
- Tailwind CSS 3.4.6
- Framer Motion 11.x
- Design tokens live in `app/globals.css` as CSS custom properties
- Copy integration uses `app/components/ProjectCopy.tsx` reading `public/content.json`
- Image integration uses `app/components/ProjectImage.tsx` reading `public/assets.json`

## Merge Order

1. **T-001 first** — shared navigation + layout enhancement (required by all pages)
2. **T-002 through T-007** — page scaffolds in any order after T-001 merges

---

## TASK ID: T-001
**ASSIGNED TO:** worker-t2  
**TIER:** T2  
**TITLE:** Build shared Navigation component and integrate into RootLayout  
**DESCRIPTION:**  
Create a `Navigation` component that renders a site-wide nav bar with links to all 6 routes. Integrate it into `app/layout.tsx` so every page inherits it. The component must use the approved design tokens (deliverable 59de44ad-0ca8-4673-870b-17b939fb51d1) for colors, fonts, and spacing. It must be keyboard-accessible and include visible focus rings. The nav should be responsive and use semantic HTML (`<nav>` landmark).  
**FILES TO CREATE:**  
- `app/components/Navigation.tsx`  
**FILES TO MODIFY:**  
- `app/layout.tsx`  
**DO NOT TOUCH:**  
- `app/globals.css`, `public/content.json`, `public/assets.json`, `next.config.js`  
**DEPENDENCIES:**  
- design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1)  
**INTERFACE CONTRACT:**  
- `Navigation()` exported as default React component, zero props.  
- `layout.tsx` renders `<Navigation />` immediately inside `<body>` before `{children}`.  
**ACCEPTANCE CRITERIA:**
  1. `app/components/Navigation.tsx` exists and exports a default React component.
  2. Navigation renders a `<nav>` landmark containing links to `/`, `/about`, `/blog`, `/contact`, `/privacy`, `/terms`.
  3. All styling uses CSS custom properties from `app/globals.css` (e.g., `var(--color-text)`, `var(--font-body)`).
  4. Navigation is keyboard-reachable; each link has a visible `:focus` ring.
  5. `app/layout.tsx` imports and renders `<Navigation />` before `{children}`.
  6. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** medium  

---

## TASK ID: T-002
**ASSIGNED TO:** worker-coder  
**TIER:** Coder  
**TITLE:** Build complete Home page (/) with content and asset integration  
**DESCRIPTION:**  
Replace the empty `app/page.tsx` with a full home page that integrates all approved copy (deliverable b8a68292-4e48-4cb6-bc82-8c9192c13753) and creative assets from `public/assets.json`. The page must include: a hero section (headline, subheadline, CTA buttons, hero image), a features section (3 features with titles, bodies, and images), a social proof section, and a footer area. All content must be rendered via `ProjectCopy` and `ProjectImage` components to maintain the established data-driven pattern. Styling must use the approved design tokens (deliverable 59de44ad-0ca8-4673-870b-17b939fb51d1).  
**FILES TO CREATE:**  
- none  
**FILES TO MODIFY:**  
- `app/page.tsx`  
**DO NOT TOUCH:**  
- `app/layout.tsx`, `app/globals.css`, `next.config.js`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753), assets (public/assets.json)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` and `ProjectImage` for all dynamic content.  
**ACCEPTANCE CRITERIA:**
  1. `app/page.tsx` renders a complete home page inside `<main id="top">`.
  2. Hero section uses `ProjectImage id="hero"` and `ProjectCopy` ids: `headline`, `subheadline`, `cta_primary`, `cta_secondary`.
  3. Features section displays 3 features using `ProjectImage` ids `feature_1`, `feature_2`, `feature_3` and `ProjectCopy` ids `feature_1_title`, `feature_1_body`, `feature_2_title`, `feature_2_body`, `feature_3_title`, `feature_3_body`.
  4. Social proof section uses `ProjectImage id="social_proof"` and `ProjectCopy id="social_proof"`.
  5. Footer area uses `ProjectCopy id="footer_text"`.
  6. All sections use design token CSS variables for colors, fonts, spacing, and radii.
  7. Heading hierarchy is logical (`h1` for headline, `h2` for section titles, etc.).
  8. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** high  

---

## TASK ID: T-003
**ASSIGNED TO:** worker-t2  
**TIER:** T2  
**TITLE:** Build About page (/about) scaffold with copy integration  
**DESCRIPTION:**  
Create `app/about/page.tsx` as a new route in the Next.js App Router. The page must render about content using the `ProjectCopy` component and the approved copy deliverable (b8a68292-4e48-4cb6-bc82-8c9192c13753). Extend `public/content.json` with new keys `about_headline` and `about_body` (empty strings as placeholders) so the copy pipeline can populate them later. Styling must use the approved design tokens (59de44ad-0ca8-4673-870b-17b939fb51d1). The page must be accessible with proper landmarks and heading hierarchy.  
**FILES TO CREATE:**  
- `app/about/page.tsx`  
**FILES TO MODIFY:**  
- `public/content.json`  
**DO NOT TOUCH:**  
- `app/globals.css`, `next.config.js`, `app/layout.tsx`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` for text content.  
**ACCEPTANCE CRITERIA:**
  1. `app/about/page.tsx` exists and exports a default React component.
  2. Page renders a `<main>` landmark with about content.
  3. Page uses `ProjectCopy` with ids `about_headline` and `about_body`.
  4. `public/content.json` is extended with `about_headline` and `about_body` keys containing `{ "text": "" }`.
  5. All styling uses design token CSS variables.
  6. Heading hierarchy is correct (`h1` for headline).
  7. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** medium  

---

## TASK ID: T-004
**ASSIGNED TO:** worker-t2  
**TIER:** T2  
**TITLE:** Build Blog page (/blog) scaffold with copy integration  
**DESCRIPTION:**  
Create `app/blog/page.tsx` as a new route. The page must render a blog listing with at least one sample post card to establish the layout pattern. Use `ProjectCopy` for the page headline and intro text, referencing the approved copy deliverable (b8a68292-4e48-4cb6-bc82-8c9192c13753). Extend `public/content.json` with new keys `blog_headline` and `blog_intro`. Styling must use the approved design tokens (59de44ad-0ca8-4673-870b-17b939fb51d1). The page must be accessible with proper landmarks and heading hierarchy.  
**FILES TO CREATE:**  
- `app/blog/page.tsx`  
**FILES TO MODIFY:**  
- `public/content.json`  
**DO NOT TOUCH:**  
- `app/globals.css`, `next.config.js`, `app/layout.tsx`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` for text content.  
**ACCEPTANCE CRITERIA:**
  1. `app/blog/page.tsx` exists and exports a default React component.
  2. Page renders a `<main>` landmark with a blog listing containing at least one post card.
  3. Page uses `ProjectCopy` with ids `blog_headline` and `blog_intro`.
  4. `public/content.json` is extended with `blog_headline` and `blog_intro` keys containing `{ "text": "" }`.
  5. Post cards use design token CSS variables for styling.
  6. Heading hierarchy is correct (`h1` for page title, `h2` for post titles).
  7. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** medium  

---

## TASK ID: T-005
**ASSIGNED TO:** worker-t2  
**TIER:** T2  
**TITLE:** Build Contact page (/contact) scaffold with copy integration  
**DESCRIPTION:**  
Create `app/contact/page.tsx` as a new route. The page must render contact information and a non-functional contact form (static export prevents server-side form handling). Use `ProjectCopy` for headline, body, and email text, referencing the approved copy deliverable (b8a68292-4e48-4cb6-bc82-8c9192c13753). Extend `public/content.json` with new keys `contact_headline`, `contact_body`, and `contact_email`. All form inputs must have associated `<label>` elements. Styling must use the approved design tokens (59de44ad-0ca8-4673-870b-17b939fb51d1).  
**FILES TO CREATE:**  
- `app/contact/page.tsx`  
**FILES TO MODIFY:**  
- `public/content.json`  
**DO NOT TOUCH:**  
- `app/globals.css`, `next.config.js`, `app/layout.tsx`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` for text content.  
**ACCEPTANCE CRITERIA:**
  1. `app/contact/page.tsx` exists and exports a default React component.
  2. Page renders a `<main>` landmark with contact info and a non-functional form.
  3. Page uses `ProjectCopy` with ids `contact_headline`, `contact_body`, `contact_email`.
  4. `public/content.json` is extended with `contact_headline`, `contact_body`, and `contact_email` keys containing `{ "text": "" }`.
  5. Every form `<input>` and `<textarea>` has an associated `<label>` with `htmlFor` matching the input `id`.
  6. All styling uses design token CSS variables.
  7. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** medium  

---

## TASK ID: T-006
**ASSIGNED TO:** worker-t1  
**TIER:** T1  
**TITLE:** Build Privacy page (/privacy) scaffold with copy integration  
**DESCRIPTION:**  
Create `app/privacy/page.tsx` as a new route. The page must render privacy policy content in a readable, structured layout. Use `ProjectCopy` for headline and body text, referencing the approved copy deliverable (b8a68292-4e48-4cb6-bc82-8c9192c13753). Extend `public/content.json` with new keys `privacy_headline` and `privacy_body`. Styling must use the approved design tokens (59de44ad-0ca8-4673-870b-17b939fb51d1). The page must be accessible with proper landmarks and heading hierarchy.  
**FILES TO CREATE:**  
- `app/privacy/page.tsx`  
**FILES TO MODIFY:**  
- `public/content.json`  
**DO NOT TOUCH:**  
- `app/globals.css`, `next.config.js`, `app/layout.tsx`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` for text content.  
**ACCEPTANCE CRITERIA:**
  1. `app/privacy/page.tsx` exists and exports a default React component.
  2. Page renders a `<main>` landmark with privacy policy content.
  3. Page uses `ProjectCopy` with ids `privacy_headline` and `privacy_body`.
  4. `public/content.json` is extended with `privacy_headline` and `privacy_body` keys containing `{ "text": "" }`.
  5. All styling uses design token CSS variables.
  6. Heading hierarchy is correct (`h1` for headline).
  7. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** low  

---

## TASK ID: T-007
**ASSIGNED TO:** worker-t1  
**TIER:** T1  
**TITLE:** Build Terms page (/terms) scaffold with copy integration  
**DESCRIPTION:**  
Create `app/terms/page.tsx` as a new route. The page must render terms of service content in a readable, structured layout. Use `ProjectCopy` for headline and body text, referencing the approved copy deliverable (b8a68292-4e48-4cb6-bc82-8c9192c13753). Extend `public/content.json` with new keys `terms_headline` and `terms_body`. Styling must use the approved design tokens (59de44ad-0ca8-4673-870b-17b939fb51d1). The page must be accessible with proper landmarks and heading hierarchy.  
**FILES TO CREATE:**  
- `app/terms/page.tsx`  
**FILES TO MODIFY:**  
- `public/content.json`  
**DO NOT TOUCH:**  
- `app/globals.css`, `next.config.js`, `app/layout.tsx`  
**DEPENDENCIES:**  
- T-001, design_tokens (59de44ad-0ca8-4673-870b-17b939fb51d1), copy (b8a68292-4e48-4cb6-bc82-8c9192c13753)  
**INTERFACE CONTRACT:**  
- Default export React component. Uses `ProjectCopy` for text content.  
**ACCEPTANCE CRITERIA:**
  1. `app/terms/page.tsx` exists and exports a default React component.
  2. Page renders a `<main>` landmark with terms of service content.
  3. Page uses `ProjectCopy` with ids `terms_headline` and `terms_body`.
  4. `public/content.json` is extended with `terms_headline` and `terms_body` keys containing `{ "text": "" }`.
  5. All styling uses design token CSS variables.
  6. Heading hierarchy is correct (`h1` for headline).
  7. `next build` completes with zero errors and generates valid HTML.
**BRANCH NAME:** ticket-fix/b99e0f38  
**ESTIMATED COMPLEXITY:** low  
