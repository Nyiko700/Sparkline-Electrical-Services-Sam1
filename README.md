# Sparkline-Electrical-Services-Sam1
## Student Information
## Student Number: ST10506659
## Module: WEDE5020 - Web Development

## Live Site and Repository
Live website: https://nyiko700.github.io/Sparkline-Electrical-Services-Sam1/
GitHub repository: https://github.com/Nyiko700/Sparkline-Electrical-Services-Sam1.git

## Project Overview

This repository contains the code for a fictional small business website built for Sparkline Electrical Services, a Cape Town-based electrical contracting business. The project is developed in three parts across the module:

Part 1 — Building the Foundation: Project planning, research, and HTML structure. Complete
Part 2 — Designing the Visuals: CSS styling and responsive design. Complete
Part 3 — Enhancing Functionality and SEO: JavaScript, form validation, SEO, and deployment. Complete (deployment link to be added above)sitory: 

## Design Direction

The visual identity is drawn from the electrical trade itself rather than a generic corporate template:

Colour: deep navy (
#16283F) and electric amber (
#F2A20C) — the "spark" accent used consistently for CTAs, focus states, and the underline mark on every heading.
Typography: Oswald (headings, industrial/condensed), Inter (body, readable), and IBM Plex Mono (labels, contact details, nav — evokes spec-sheet/datasheet lettering).
Signature element: a thin dotted "circuit trace" divider between page sections, and CTA buttons that flip to amber on hover/focus like a switch being thrown.
Layout: CSS Grid for the hero and card layouts, Flexbox for navigation and tag lists, fully responsive with breakpoints at 768px and 480px using relative units (rem, em, %).
Website Goals and Objectives
Generate qualified leads through an online enquiry/quote form.
Reduce phone-based scheduling by allowing clients to request quotes online.
Build credibility through a professional online presence.
Provide clear service information so clients self-select before contacting the business.

## Key Performance Indicators (KPIs):

Number of enquiry form submissions per month.
Average time spent on the Services page.
Percentage of enquiries that convert to booked jobs.
Key Features and Functionality
Homepage: two-column hero, introduction, call to action, internal links to services.
About Us: company history, mission, vision, and animated count-up statistics.
Services: three service cards, a searchable/filterable/sortable Recent Projects gallery with a lightbox, and an accessible FAQ accordion.
Enquiry: validated quote form that returns an instant cost guide and availability estimate.
Contact: two branch locations on an interactive Leaflet map (with "find my nearest branch"), and a validated contact form that compiles an email to the business.
Fully responsive (desktop, tablet ≤768px, mobile ≤480px) with responsive images (srcset/sizes).
Accessibility: visible focus states, ARIA labelling, keyboard-operable widgets, prefers-reduced-motion support.

## Timeline and Milestones
Milestone	Deliverable	Target Date	Status
Milestone 1	Project proposal approved; content research completed	Week 1	Done
Milestone 2	HTML structure for all 5 pages complete (Part 1)	Week 3	Done
Milestone 3	CSS styling and responsive design complete (Part 2)	Week 6	Done
Milestone 4	JavaScript functionality and SEO optimisation complete (Part 3)	Week 9	Done (deployment pending)

## Part 2 Details

Part 2 delivered the full CSS styling and responsive design layer in css/style.css:

A single external stylesheet linked from all five pages, with a CSS reset and a design-token layer (:root custom properties) for colour, type, spacing, and shadows.
Layout with CSS Grid (hero, cards, team, contact details) and Flexbox (nav, tags, footer).
Box-shadows, border-radius, hover/focus states, and the "circuit trace" section divider.
Media queries at max-width: 768px and max-width: 480px, using relative units throughout.
Responsive images (srcset/sizes) at 480w/800w/1200w.
Part 3 Details
1. JavaScript enhancements (js/main.js)

All behaviour lives in one commented, sectioned script written in plain JavaScript (no framework). Where the brief allows "jQuery or other frameworks", vanilla JavaScript was chosen to keep the site light and fast.

Brief requirement	Implementation	Where
2.1 Accordion / tabs / modals	FAQ accordion (one panel open at a time, ARIA aria-expanded/aria-controls, smooth CSS height transition) and a modal lightbox	Services
2.1 Interactive map	Leaflet map (OpenStreetMap tiles) with a marker and popup per branch, "show location" buttons, and a Geolocation-based "find my nearest branch" using the haversine distance formula	Contact
2.1 Animations / transitions	CSS transitions plus JavaScript: scroll-reveal fade-ins (IntersectionObserver), count-up statistics (requestAnimationFrame), lightbox fade, accordion slide. All disabled for visitors who prefer reduced motion	All / About
2.1 Advanced DOM manipulation	Elements built with a small el() helper using createElement (never innerHTML), event handling, re-ordering and hiding nodes, live-region updates, focus management	All
2.1 Gallery with lightbox	Click a project photo for a larger view; keyboard arrows, Esc, backdrop click, focus trap, and focus returns to the thumbnail on close	Services
2.2 Dynamic content	The Recent Projects gallery is rendered from a JavaScript data array	Services
2.2 Search, filter, sort	Live keyword search, category filter (Residential / Commercial / Maintenance), and sort (most recent, A–Z, Z–A), all combinable, with a live result count	Services
2. Form functionality and validation (brief section 4)

## The two forms have different purposes, as the brief requires.

enquiry.html — ask about a service, get a cost and availability response

Fields: name, email, phone, job type, suburb, preferred date, optional message.
Validation: HTML5 attributes (required, type, minlength, maxlength, pattern) and JavaScript validation with specific messages: names (letters only), email format, South African phone numbers (021 555 0134, 0821234567, +27 82 123 4567), job type chosen, date not in the past and within 12 months, message length with a live character counter.
Error handling: inline messages beside each field, aria-invalid, role="alert", focus moves to the first invalid field, and errors clear live as the visitor corrects them.
Processing and response: once valid, the form shows a cost guide for the chosen job type and an availability message based on the chosen date (weekday, Saturday surcharge, Sunday emergency-only, or short-notice limits), plus a clear note that it is an estimate, not a final quote.
AJAX submission: the form is sent asynchronously with a loading state, then the response panel appears without a page reload.
action attribute: action="/" with data-github="true", so the form also works without JavaScript when deployed on GitHub.
Spam protection: a hidden honeypot field (bot-field) that real visitors never fill in.

contact.html — send a general message to the organisation

Fields: name, email, type of message (general question, callback, compliment, complaint, other), full message.
Same validation approach and messaging as the enquiry form (message 10–1000 characters).
Compiled email: once valid, the details are compiled into an email preview (To, Subject, body) and a "Open in my email app" button (mailto: link) addressed to the recipient set in the code (RECIPIENT_EMAIL in js/main.js). The form's action="mailto:..." is the no-JavaScript fallback.

Important honesty note about AJAX: a static website has no server of its own, so by default SIMULATE_SERVER = true in js/main.js and the enquiry "send" is simulated with a short delay (the validation, loading state, and response are all real). To send real submissions, deploy on Netlify (the form is already marked up for Netlify Forms) and set SIMULATE_SERVER = false; the code then POSTs the form with fetch().

3. Search Engine Optimisation (SEO)

3.1 On-page SEO

Item	What was done

Keyword research	Keywords were chosen from the services offered and the way a local customer would phrase a search, then used naturally in titles, headings and body text: electrician Cape Town, residential wiring, commercial electrical installations, fault finding, certificate of compliance (CoC), electrician Bellville / Claremont. No keyword tool was used, so the list should be validated with Google Search Console / Keyword Planner after launch.

Title tags & meta descriptions	Unique title (51–55 characters) and meta description (140–160 characters) on every page.
Header tags	One <h1> per page (business name in the header), <h2> for sections, <h3> for sub-sections; no skipped levels.
Image optimisation	Descriptive file names (e.g. project-full-house-rewire-480.jpg), descriptive alt text, explicit width/height to stop layout shift, loading="lazy" below the fold, and fetchpriority="high" on the hero image.
URL structure	Short, lowercase, descriptive page names (services.html, enquiry.html) and <link rel="canonical"> on every page.

Internal linking	Homepage service tags link to the matching service cards; contextual links between Home, About, Services, Enquiry and Contact; FAQ answers link to the quote form and map.

Mobile-friendliness	viewport meta tag, responsive layout, large touch targets, tested at 390px width.
Structured data	JSON-LD (schema.org Electrician) on the homepage with address, phone, hours and service area, for local rich results.

Social sharing	Open Graph and Twitter card tags, plus a Share this page button (Web Share API, falling back to copy-link).
meta keywords	Included for completeness, but Google has stated it ignores this tag; the real keyword work is in the visible content above.

3.2 Off-page SEO (plan — these are actions for the business, not code)

Backlinks: request links from local suppliers, the Cape Town chamber of commerce, property agents and landlords' associations the business works with; ask happy clients for reviews that link back.
Social media: create Facebook and Instagram business profiles that link to the site and share recent projects (the gallery photos are designed to be reused).
Local SEO: claim and verify a Google Business Profile for both the Bellville office and Claremont depot with identical name/address/phone details to the website, and list the business in South African online business directories using the same details.

3.3 Additional SEO and technical requirements

robots.txt: allows all crawlers and points to the sitemap.
sitemap.xml: lists all five pages (sitemaps.org protocol) with lastmod, changefreq, priority.
Page speed: deferred scripts, preconnect for fonts with display=swap, lazy-loaded and responsive images, long-lived caching headers for static assets (_headers), no JavaScript framework.
Security: HTTPS comes from the hosting platform; _headers adds X-Content-Type-Options, X-Frame-Options, Referrer-Policy and Permissions-Policy on GitHub; all user input is written to the page with textContent (never innerHTML) so it cannot inject HTML or scripts; external links use rel="noopener noreferrer"; the Leaflet library is loaded with a pinned version and an integrity (SRI) hash; forms include a honeypot field. A Content-Security-Policy was deliberately not added because it could not be tested against every third-party resource in this project.

## 4. Accessibility notes

Keyboard-operable accordion, lightbox (focus trap, Esc, arrow keys, focus restored), and map buttons; aria-pressed on filter buttons; aria-live regions for result counts and form responses; aria-current="page" in the navigation; and prefers-reduced-motion honoured by every animation.

## References

Google, 2026. SEO Starter Guide. Google Search Central. [online] Available at: https://developers.google.com/search/docs/fundamentals/seo-starter-guide [Accessed 29 October 2026].
Leaflet, 2026. Leaflet Quick Start Guide. [online] Available at: https://leafletjs.com/examples/quick-start/ [Accessed 29 October 2026].
Leaflet, 2026. Download Leaflet. [online] Available at: https://leafletjs.com/download [Accessed 29 October 2026].
Mozilla Developer Network (MDN), 2026. Intersection Observer API. [online] Available at: https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API [Accessed 29 October 2026].
Mozilla Developer Network (MDN), 2026. Geolocation API. [online] Available at: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API [Accessed 29 October 2026].
Mozilla Developer Network (MDN), 2026. Web Share API. [online] Available at: https://developer.mozilla.org/en-US/docs/Web/API/Web_Share_API [Accessed 29 October 2026].
OpenStreetMap, 2026. Copyright and licence. [online] Available at: https://www.openstreetmap.org/copyright [Accessed 29 October 2026].
Schema.org, 2026. Electrician. [online] Available at: https://schema.org/Electrician [Accessed 29 October 2026].
Sitemaps.org, 2026. Sitemaps XML format. [online] Available at: https://www.sitemaps.org/protocol.html [Accessed 29 October 2026].
W3C Web Accessibility Initiative, 2026. Accordion pattern and Dialog (modal) pattern. ARIA Authoring Practices Guide. [online] Available at: https://www.w3.org/WAI/ARIA/apg/patterns/accordion/ and https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/ [Accessed 29 October 2026].
Netlify, 2026. Forms setup. Netlify Docs. [online] Available at: https://docs.netlify.com/forms/setup/ [Accessed 29 October 2026].
Afrihost, 2026. Web hosting plans. [online] Available at: <www.afrihost.com> [Accessed 10 August 2026].
Flaticon, 2026. Free icons. [online] Available at: <www.flaticon.com> [Accessed 10 August 2026].
Unsplash, 2026. Free high-resolution photos. [online] Available at: <www.unsplash.com> [Accessed 10 August 2026].
Mozilla Developer Network (MDN), 2026. HTML: HyperText Markup Language. [online] Available at: <developer.mozilla.org/en-US/docs/Web/HTML> [Accessed 10 August 2026].
Mozilla Developer Network (MDN), 2026. CSS Grid Layout. [online] Available at: <developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout> [Accessed 14 August 2026].
Mozilla Developer Network (MDN), 2026. Responsive images. [online] Available at: <developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images> [Accessed 14 August 2026].
Google Fonts, 2026. Oswald, Inter & IBM Plex Mono. [online] Available at: <fonts.google.com> [Accessed 14 August 2026].
CSS-Tricks, 2026. A Complete Guide to CSS Grid. [online] Available at: <css-tricks.com/snippets/css/complete-guide-grid> [Accessed 14 August 2026].


