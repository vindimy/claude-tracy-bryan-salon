# Claude Code Prompt: Tracy Bryan's Gentlemen Salon — Website Redesign

---

## PROJECT BRIEF

Redesign the website for **Tracy Bryan's Gentlemen Salon** — a premium men's grooming salon located at **1459 Westwood Blvd, Los Angeles, CA 90024** (Westwood Village neighborhood). The new site will be a single-page HTML/CSS/JS website that serves as a digital storefront: showcasing the salon interior, listing all services, and converting visitors into booked clients.

---

## STEP 1: SCRAPE GOOGLE MAPS REVIEWS

Before writing any code, use your web browsing or fetch capabilities to collect the top 5–8 reviews from the Google Maps listing:

**Google Maps URL:** https://maps.app.goo.gl/8JdKEudKe8yKbTHR8

Extract:
- Reviewer first name (or first name + last initial)
- Star rating
- Review text (select the most vivid, specific, enthusiastic snippets — 1–3 sentences each)
- Date (approximate is fine)

Use these real reviews in the Testimonials section of the site. If you cannot scrape live reviews, use the following verified review blurbs collected from public sources:

```
1. "Tracy was fabulous. She listened carefully, took her time, and gave him the perfect haircut. He left the salon with a smile." — Jennifer M. ⭐⭐⭐⭐⭐

2. "If any barber or hairstylist has done you dirty in the past, Tracy will cure that haircut anxiety. It's great to have a professional that actually listens to what you want!" — Marcus T. ⭐⭐⭐⭐⭐

3. "On the west side, she's the best there is for a solid men's haircut at an affordable price. Great friendly staff, complimentary beverages, and a vibe you can't find anywhere else." — David R. ⭐⭐⭐⭐⭐

4. "Tracy has created a clean, welcoming space for salon services. It seems like a great place for men who want better — and more — service than a typical barbershop." — Sarah K. ⭐⭐⭐⭐⭐

5. "Really nice place to get my hair done! It just happened to be the best place I've visited in LA so far. The staff are really nice and friendly." — Alex L. ⭐⭐⭐⭐⭐
```

---

## STEP 2: BUILD THE WEBSITE

Create a single file: `index.html`

### DESIGN DIRECTION: Quiet Luxury / Timeless Editorial

**Aesthetic:** Think old-money Westwood — clean, assured, unhurried. Not trendy or loud. Inspired by upscale men's magazines (GQ, Esquire), luxury hotel lobbies, and high-end tailor shops. The site should feel like it belongs on a Westwood block next to boutique law firms and established restaurants.

**Color Palette:**
```
--color-cream:     #F5F2EC   (warm white background)
--color-ink:       #1A1A1A   (near-black for primary text)
--color-gold:      #B8975A   (warm gold for accents, CTAs, dividers)
--color-charcoal:  #3D3D3D   (secondary text)
--color-mist:      #E8E4DC   (subtle section dividers / cards)
```

**Typography:**
- Display / Hero heading: `Cormorant Garamond` (Google Fonts) — elegant, old-world serif with a modern edge
- Body / UI text: `Jost` (Google Fonts) — clean, geometric, contemporary. Weight 300/400/500
- Accent labels / navigation: `Jost` uppercase, wide letter-spacing (0.2em)

**Motion:**
- Subtle fade-in on scroll for each section (IntersectionObserver + CSS transitions)
- Smooth scroll between anchor sections
- Hover states on all interactive elements: gold underline animations on nav links, slight lift on cards
- CTA button: gold border → fills with gold on hover, text shifts to cream

**Layout Feel:**
- Generous whitespace — sections breathe
- Typography-led design — let the words carry weight
- Full-width hero with centered overlay text
- Services in a clean 3-column grid (responsive: 2-col tablet, 1-col mobile)
- Testimonials in a horizontal scrollable strip or masonry-style cards

---

## STEP 3: PAGE SECTIONS (IN ORDER)

### 1. `<head>` — SEO & Meta

```html
<title>Tracy Bryan's Gentlemen Salon | Premium Men's Grooming in Westwood, Los Angeles</title>
<meta name="description" content="Tracy Bryan's Gentlemen Salon — Westwood's premier destination for men's haircuts, shaves, facials, hair systems, and nail care. Book your appointment in Los Angeles today.">
<meta name="keywords" content="men's salon Westwood, men's haircut Los Angeles, barbershop Westwood Village, men's grooming LA, hair system Westwood, men's facial Los Angeles, Tracy Bryan salon, premium barber Westwood, men's manicure LA">
<meta property="og:title" content="Tracy Bryan's Gentlemen Salon | Westwood, Los Angeles">
<meta property="og:description" content="Premium grooming services for the modern gentleman. Haircuts, shaves, facials, hair systems & more — in the heart of Westwood, LA.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://www.tracybryansgentlemenssalon.com">
<link rel="canonical" href="https://www.tracybryansgentlemenssalon.com">
<meta name="robots" content="index, follow">
<!-- Schema.org Local Business Structured Data (see Step 4) -->
```

Also import Google Fonts:
```
Cormorant Garamond: 300, 400, 500, 600 (regular + italic)
Jost: 300, 400, 500, 600
```

---

### 2. NAVIGATION BAR

- Fixed top, transparent → shifts to `rgba(245,242,236,0.97)` with `backdrop-filter: blur(8px)` on scroll
- Left: Logo text — **TRACY BRYAN'S** in Cormorant Garamond, small · **GENTLEMEN SALON** in Jost uppercase tracking
- Center/Right: nav links — `Services`, `The Space`, `Reviews`, `Contact`
- Far right: CTA button — `Book Now` (gold outlined, fills on hover)
- Mobile: hamburger icon → full-screen overlay menu

---

### 3. HERO SECTION

- **Full-viewport-height** section
- Background: placeholder image (full-bleed) representing the salon interior or storefront. Use:
  ```html
  <img src="photos/hero-interior.jpg" alt="Tracy Bryan's Gentlemen Salon interior — Westwood, Los Angeles" ...>
  ```
  If image doesn't exist, use CSS `background-color: #2A2520` as fallback with a subtle noise texture overlay.
- Dark gradient overlay: `linear-gradient(to bottom, rgba(26,21,17,0.55) 0%, rgba(26,21,17,0.35) 100%)`
- Centered text block:
  ```
  [small caps label, gold, letter-spaced]
  WESTWOOD · LOS ANGELES

  [H1, Cormorant Garamond, large, cream]
  A Salon
  for Gentlemen.

  [body, Jost 300, cream/70% opacity]
  Premium grooming services for the modern man.
  Haircuts, shaves, facials, and more — in the heart of Westwood.

  [Two CTA buttons side-by-side]
  [Primary: gold filled] Book an Appointment →
  [Secondary: cream outlined] Explore Services
  ```
- Hero CTAs link to:
  - Book: `https://book.squareup.com/appointments/mvah5rz1ru5cmq/location/SP9AKEM3N8V0T/services`
  - Explore: `#services` (anchor scroll)

---

### 4. INTRO / ABOUT STRIP

Minimal 2-column layout (text left, small detail image right — or full-width centered text on mobile):

```
[small gold rule — 40px wide horizontal line]

THE SALON

Since 2019, Tracy Bryan's Gentlemen Salon has been Westwood's destination
for men who take their appearance seriously. Founded by Tracy Bryan —
a seasoned hairstylist with an eye for detail and a gift for listening —
the salon combines the precision of a master stylist with the comfort
of a private club.

No rush. No noise. Just exceptional grooming.

[Placeholder image: reception desk or waiting area]
photos/about-waiting-area.jpg
```

---

### 5. SERVICES SECTION

Anchor: `id="services"`

Section heading:
```
OUR SERVICES
[Cormorant Garamond subheading]
Everything a gentleman needs, under one roof.
```

Display services in a **3-column responsive card grid**. Each card has:
- Icon (use simple SVG or Unicode symbol — scissors ✂, razor 🪒, etc.)
- Service name (Jost, uppercase, medium weight)
- Short description (Jost 300, charcoal)
- Optional: starting price if available

**Services to include** (based on salon category and Square booking system — use these, but note that actual services/prices should be verified from the Square booking link):

```
HAIRCUTS
────────
Men's Haircut
Classic scissor or clipper cut tailored to your style. Every cut includes a consultation, shampoo, and finish.

Men's Haircut + Beard Trim
The complete look — precision cut paired with expert beard sculpting and lineup.

Children's Haircut
Expert cuts for boys of all ages, in a calm and welcoming environment.

SHAVING & GROOMING
──────────────────
Classic Hot Towel Shave
A traditional straight-razor shave with hot towels, pre-shave oil, and a soothing aftershave treatment.

Beard Trim & Shape
Precise beard sculpting and detailing. Defined lines, natural shape.

HAIR TREATMENTS
───────────────
Keratin Treatment
Frizz-free smoothing treatment for lasting manageability and shine.

Hair Color / Balayage
Natural-looking color enhancement and balayage, tailored to skin tone and style.

HAIR SYSTEMS
────────────
Hair System Consultation & Application
Discreet, natural-looking non-surgical hair replacement systems. Private room available. Consultation required.

Hair System Maintenance
Ongoing care and styling for existing hair systems. Taping, cleaning, and reattachment.

SKINCARE
────────
Men's Facial
A results-driven facial designed for men's skin: deep cleansing, exfoliation, and hydration. Conducted in a private treatment room.

NAIL CARE
─────────
Men's Manicure
Clean, shaped, and buffed nails for the gentleman who attends to every detail.

Pedicure
Relaxing foot care treatment — soak, exfoliate, trim, and hydrate.
```

**Below the service grid, a full-width CTA banner:**
```
[cream background, centered]
Ready to look your best?

[Gold CTA Button]
Book Your Appointment →
```
Link: `https://book.squareup.com/appointments/mvah5rz1ru5cmq/location/SP9AKEM3N8V0T/services`

---

### 6. THE SPACE — PHOTO GALLERY

Anchor: `id="the-space"`

Section header:
```
THE SPACE
[subheading]
Designed for the discerning gentleman.
```

Create a **CSS grid photo gallery** with placeholder `<img>` tags for each of the following photo assets. Use `object-fit: cover` on all images. Grid layout: asymmetric, editorial feel (one large image + two smaller, then repeat).

Photo slots with descriptive `alt` tags and `src` paths:
```
photos/storefront.jpg         — "Tracy Bryan's Gentlemen Salon storefront on Westwood Blvd, Los Angeles"
photos/interior-full.jpg      — "Full salon interior — premium men's grooming salon in Westwood"
photos/waiting-area.jpg       — "Comfortable waiting area at Tracy Bryan's Gentlemen Salon"
photos/reception-desk.jpg     — "Reception desk at Tracy Bryan's Gentlemen Salon, Westwood"
photos/barber-chair.jpg       — "Barber chair — precision grooming at Tracy Bryan's Gentlemen Salon"
photos/manicure-chair.jpg     — "Manicure station — men's nail care at Tracy Bryan's Gentlemen Salon"
photos/facial-room.jpg        — "Private facial treatment room at Tracy Bryan's Gentlemen Salon"
photos/hair-systems-room.jpg  — "Discreet hair systems consultation room — Tracy Bryan's Gentlemen Salon"
```

**Important:** If any image file doesn't exist yet, display a tasteful placeholder using CSS:
```css
.photo-placeholder {
  background-color: #2A2520;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(245,242,236,0.2);
  font-family: 'Jost', sans-serif;
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}
```
With the image label as the placeholder text (e.g., "Waiting Area").

---

### 7. TESTIMONIALS SECTION

Anchor: `id="reviews"`

Section header:
```
WHAT OUR CLIENTS SAY
[Cormorant Garamond, larger]
Trusted by gentlemen across Los Angeles.
```

Display the Google Maps reviews collected in Step 1 (or the fallback reviews provided) as elegant quote cards. Layout: horizontal scrollable row on desktop, stacked on mobile.

Each card:
- Large opening quote mark `"` in gold, Cormorant Garamond, oversized
- Review text in Jost 300
- Reviewer name in Jost 500, small
- Gold star row (⭐ count)
- Subtle cream card background with a thin gold-left-border accent

Below testimonials, a link:
```
[text link, gold, small]
Read more reviews on Google Maps →
```
Link: `https://maps.app.goo.gl/8JdKEudKe8yKbTHR8`

---

### 8. CONTACT & LOCATION SECTION

Anchor: `id="contact"`

Two-column layout: **left** — contact info & hours; **right** — embedded Google Maps iframe.

**Left column content:**
```
VISIT US
1459 Westwood Blvd
Los Angeles, CA 90024

[Google Maps link]
Get Directions →   (links to https://maps.app.goo.gl/8JdKEudKe8yKbTHR8)

HOURS
Tuesday    9:00 AM – 7:00 PM
Wednesday  9:00 AM – 7:00 PM
Thursday   10:00 AM – 7:00 PM
Friday     9:00 AM – 7:00 PM
Saturday   10:00 AM – 5:00 PM
Sunday & Monday   Closed

CONTACT
(424) 252-9971

FOLLOW
@tracybryansgs on Instagram  →  https://www.instagram.com/tracybryansgs
```

**Right column:**
```html
<iframe
  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3305.5!2d-118.4395!3d34.0577!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMzTCsDAzJzI3LjciTiAxMTjCsDI2JzIyLjIiVw!5e0!3m2!1sen!2sus!4v1"
  width="100%" height="400" style="border:0; border-radius: 4px;" allowfullscreen loading="lazy"
  title="Tracy Bryan's Gentlemen Salon location map — 1459 Westwood Blvd, Los Angeles">
</iframe>
```
Note: Replace the embed src with the correct Google Maps embed URL for `1459 Westwood Blvd, Los Angeles, CA 90024`.

---

### 9. FOOTER

Full-width dark footer (`background: #1A1A1A`, `color: #F5F2EC`):

```
[Logo text]
TRACY BRYAN'S GENTLEMEN SALON

[Tagline]
Premium grooming for the modern gentleman.
Westwood · Los Angeles

[Links row]
Services   |   Book Appointment   |   My Bookings   |   Instagram   |   Google Maps

[Booking CTAs — two subtle text links]
Book New Appointment →   (https://book.squareup.com/appointments/mvah5rz1ru5cmq/location/SP9AKEM3N8V0T/services)
Manage My Bookings →     (https://book.squareup.com/appointments/mvah5rz1ru5cmq/location/SP9AKEM3N8V0T/bookings)

[Bottom bar]
© 2025 Tracy Bryan's Gentlemen Salon · 1459 Westwood Blvd, Los Angeles, CA 90024 · (424) 252-9971
```

---

## STEP 4: SCHEMA.ORG STRUCTURED DATA

Include this JSON-LD in the `<head>` for local business SEO:

```json
{
  "@context": "https://schema.org",
  "@type": "HairSalon",
  "name": "Tracy Bryan's Gentlemen Salon",
  "image": "https://www.tracybryansgentlemenssalon.com/photos/storefront.jpg",
  "url": "https://www.tracybryansgentlemenssalon.com",
  "telephone": "+14242529971",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "1459 Westwood Blvd",
    "addressLocality": "Los Angeles",
    "addressRegion": "CA",
    "postalCode": "90024",
    "addressCountry": "US"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 34.0577,
    "longitude": -118.4395
  },
  "openingHoursSpecification": [
    { "@type": "OpeningHoursSpecification", "dayOfWeek": "Tuesday", "opens": "09:00", "closes": "19:00" },
    { "@type": "OpeningHoursSpecification", "dayOfWeek": "Wednesday", "opens": "09:00", "closes": "19:00" },
    { "@type": "OpeningHoursSpecification", "dayOfWeek": "Thursday", "opens": "10:00", "closes": "19:00" },
    { "@type": "OpeningHoursSpecification", "dayOfWeek": "Friday", "opens": "09:00", "closes": "19:00" },
    { "@type": "OpeningHoursSpecification", "dayOfWeek": "Saturday", "opens": "10:00", "closes": "17:00" }
  ],
  "sameAs": [
    "https://www.instagram.com/tracybryansgs",
    "https://maps.app.goo.gl/8JdKEudKe8yKbTHR8"
  ],
  "priceRange": "$$",
  "description": "Tracy Bryan's Gentlemen Salon is Westwood's premier destination for men's grooming — haircuts, shaves, facials, hair systems, and nail care. Founded by master stylist Tracy Bryan in 2019."
}
```

---

## STEP 5: TECHNICAL REQUIREMENTS

- **Single file:** All CSS and JS embedded in `index.html` (no external stylesheets or scripts beyond Google Fonts CDN)
- **Fully responsive:** Mobile-first. Test breakpoints at 375px, 768px, 1280px, 1440px
- **Performance:** Use `loading="lazy"` on all `<img>` tags. Preconnect to Google Fonts.
- **Accessibility:** All images have descriptive `alt` tags (already specified above). Nav has `aria-label`. Color contrast ratios meet WCAG AA.
- **Smooth scroll:** `scroll-behavior: smooth` on `html` element
- **Scroll animation:** Use `IntersectionObserver` with a CSS class `.is-visible` that triggers `opacity: 1; transform: translateY(0)` transitions. Default state: `opacity: 0; transform: translateY(24px)`
- **No JavaScript frameworks** — vanilla JS only
- **Photo file structure:**
  ```
  index.html
  photos/
    hero-interior.jpg
    storefront.jpg
    interior-full.jpg
    waiting-area.jpg
    reception-desk.jpg
    barber-chair.jpg
    manicure-chair.jpg
    facial-room.jpg
    hair-systems-room.jpg
    about-waiting-area.jpg
  ```
  All photo slots should gracefully degrade to CSS placeholders if files are missing.

---

## STEP 6: FINAL CHECKLIST BEFORE DELIVERING

- [ ] All external links open in `target="_blank" rel="noopener noreferrer"`
- [ ] Both booking links work: `/services` (new booking) and `/bookings` (manage bookings)
- [ ] Google Maps link present in footer, contact section, and reviews section
- [ ] Instagram link present in footer
- [ ] Phone number `(424) 252-9971` is a `tel:` link on mobile
- [ ] Schema.org JSON-LD is valid
- [ ] HTML passes basic W3C validation (no unclosed tags, proper nesting)
- [ ] Meta description is under 160 characters
- [ ] All section anchors are present and nav links scroll correctly
- [ ] Reviews section includes real Google Maps reviews (or verified fallback quotes)
- [ ] Placeholder CSS shows gracefully for missing photos

---

## NOTES FOR CLAUDE CODE

- The business is located in **Westwood Village**, adjacent to UCLA — the demographic is educated, professional men of all ages who value quality and discretion
- Tracy Bryan personally cuts hair and has built a loyal following — the site should feel personal and trustworthy, not corporate
- **Hair systems** (non-surgical hair replacement) is a specialty service — treat it with discretion, privacy emphasis, and dignity in the copy
- The salon has dedicated **private rooms** for facials and hair systems — highlight this as a luxury feature
- Complimentary beverages are offered — mention this subtly in the About section as a hospitality touch
- The salon is **women-owned** — this can be subtly noted (Tracy Bryan is the founder) without making it the focus, since the audience is men