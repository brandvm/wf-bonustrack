# Audit: Bonus Track (www.thisisbonustrack.com)

Read-only baseline, 2026-11-20, before any change from this repo
(webflow-audit › 1). Nothing was written to Webflow. Each point is marked
**measured** (a check run against the live domain) or **read** (from the
published HTML or the Webflow API through `webflow-bonustrack`).

How it was run: the `pnpm wf:*` checks with a config whose staging and live
URLs are both `https://www.thisisbonustrack.com` (`.webflow-build/live-audit/`,
not in git). Template 1.0.0's `--live` flag still measures staging in
several scripts, so the config pins them to the live domain. Raw output is
in `.webflow-build/live-audit/out/`.

Key pages (10): `/`, `/services`, `/works`, `/liner-notes`, `/cherry-picked`,
`/contact`, `/fwb`, and one item per CMS template: `/post/we-have-hit-play`,
`/portfolios/park-hyatt-toronto`, `/cherrypicked/cake-mix`. The sitemap
lists 61 URLs.

## Findings, by what they gain and what they risk

Lowest risk first. Tracker IDs are in brackets.

1. **No JSON-LD on any of 61 pages** [BT-01], measured (wf:seo). Adding it is head code only, and visitors see nothing.
2. **H1 count wrong on 49 of 61 pages** [BT-02], measured: `/services` and `/liner-notes` have 0; 36 pages have 2; blog posts and portfolios have 4–6 (`/portfolios/park-hyatt-toronto` has 6).
3. **The footer newsletter title is a heading** [BT-03], measured: an H5 "Join the P&C Mailing list andSubscribe to Cherry Picked" on 8 of 10 key pages (H3 on `/cherry-picked`). It skips levels, and it has no space at its line break ("andSubscribe").
4. **og:image is empty on 31 pages and missing on `/cherry-picked`** [BT-04], measured. That makes 32, matching the tracker.
5. **Links without text** [BT-05/BT-08], measured (axe `link-name`, serious): 2 on every page (the menu and logo icons), 9 on `/works`, 10 on `/cherry-picked`. The tracker's alt-text request (BT-05) still needs its own image pass.
6. **`#` links: 52 distinct** [BT-07], measured (wf:links). They include the "Cherry Picked" menu link on 8 pages, the /works category tags, the /services sub-items, the shop's FAQs and Contact Us links, and a "Ready? Just.Hit.Play." link on all 38 posts.
7. **Colour contrast**, measured (axe, serious): 76–81 elements on `/liner-notes` and blog posts, 20 on `/contact`, 16 on `/services`, 13–14 on `/fwb`, 10 on `/cherry-picked`, and 3 on `/` at phone width. This isn't in the tracker yet.
8. **CSP console error**, measured (wf:html): seen this run on `/contact` only. A Cloudflare Turnstile script tries to fetch `data:,` and the page's CSP refuses it [BT-11]. The tracker says every page; this run saw it once, so recheck before the batch.
9. **Speed** [BT-12], measured (wf:perf, median of 5 with range, below). The worst mobile LCPs are `/liner-notes` at 34 s (range 28–66 s, score 50), `/works` at 14.0 s (score 73), `/cherrypicked/cake-mix` at 10.2 s and `/cherry-picked` at 8.0 s. Mobile CLS: `/portfolios/*` 0.32, `/liner-notes` 0.27, `/contact` 0.20. Desktop CLS on `/fwb` is 0.28. `/` and `/services` score 97 on mobile.
10. **Two canonical tags on every `/cherrypicked/*` page** (9 pages), measured. Webflow emits one and a second sits in the head right after it, so the source still has to be found. Not in the tracker.
11. **Template leftovers**, read: Team Members Template and Style Guide still carry the "Gringo - Webflow HTML website template" SEO title and description; Team Members has lorem-ipsum items. Team, Category and Services templates are set not to publish.
12. **Path clash**, read: the Services CMS template's path is `/services`, the same as the static Services page (the template is not published).
13. **Unused classes**, measured (wf:html): `copyright`, `g-nav-brand-link`, `cherry-picked`, `_w-footer-carousel` and others are on elements but in no stylesheet. They're harmless, but worth knowing before a rename.
14. **Links to other sites** (wf:links --external): 143 checked. Several 404/410/DNS failures in blog posts (hbr.org, sproutsocial, hubspot, mastermindbehavior, mimiqit, sephorasquad, kattstearns, digitalagencynetwork, growth-x.com, topmediadvertising.co.uk). Many 403s are bot blocks, not dead links. The /contact Facebook link answers 400 to bots. These are CMS edits, not site changes.
15. **No cookie banner; consent mode on**, measured (wf:tracking). GA4 (G-7W8K4TV2Y6, through GTM-TKM5QNH) and the LinkedIn Insight Tag run on first visit. A question for the client, not a fix.

## Speed (wf:perf, live, 5 runs each)

Median (range). Lighthouse defaults: mobile is throttled.

| Page | Device | Score | LCP | FCP | TBT | CLS | Transfer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| / | mobile | 97 (96–97) | 1.9 s (1875–1969ms) | 1.9 s | 88 ms | 0.002 (0.002–0.002) | 9.9 MB |
| / | desktop | 99 (93–99) | 0.7 s (649–1305ms) | 0.7 s | 0 ms | 0.014 (0.014–0.014) | 9.9 MB |
| /services | mobile | 97 (93–98) | 1.9 s (1869–2742ms) | 1.9 s | 83 ms | 0.003 (0.003–0.003) | 4.5 MB |
| /services | desktop | 97 (75–100) | 0.7 s (675–2132ms) | 0.7 s | 0 ms | 0.09 (0.013–0.117) | 4.5 MB |
| /works | mobile | 73 (72–73) | 14.0 s (13921–15210ms) | 1.9 s | 78 ms | 0 (0–0) | 3.7 MB |
| /works | desktop | 82 (80–82) | 3.2 s (2997–3299ms) | 0.7 s | 0 ms | 0 (0–0) | 3.7 MB |
| /liner-notes | mobile | 50 (39–54) | 34.2 s (27913–66340ms) | 1.9 s | 132 ms | 0.271 (0.151–0.367) | 25.2 MB |
| /liner-notes | desktop | 85 (77–89) | 2.8 s (2187–5011ms) | 0.7 s | 0 ms | 0.002 (0.002–0.002) | 14.5 MB |
| /cherry-picked | mobile | 74 (73–76) | 8.0 s (6584–8738ms) | 1.9 s | 86 ms | 0.017 (0.017–0.02) | 6.4 MB |
| /cherry-picked | desktop | 90 (87–93) | 2.0 s (1717–2356ms) | 0.7 s | 0 ms | 0.002 (0.002–0.009) | 12.7 MB |
| /contact | mobile | 66 (65–71) | 6.4 s (4696–6574ms) | 1.9 s | 109 ms | 0.204 (0.204–0.204) | 3.2 MB |
| /contact | desktop | 95 (94–95) | 1.5 s (1425–1542ms) | 0.7 s | 0 ms | 0.051 (0.051–0.051) | 3.2 MB |
| /fwb | mobile | 98 (98–98) | 1.9 s (1847–1907ms) | 1.9 s | 106 ms | 0.008 (0.008–0.008) | 1.2 MB |
| /fwb | desktop | 83 (73–84) | 1.2 s (1122–1910ms) | 0.7 s | 0 ms | 0.275 (0.275–0.289) | 1.4 MB |
| /post/we-have-hit-play | mobile | 70 (67–74) | 6.5 s (5117–18140ms) | 1.9 s | 109 ms | 0.144 (0.144–0.144) | 5.2 MB |
| /post/we-have-hit-play | desktop | 79 (78–85) | 3.9 s (2660–4123ms) | 0.7 s | 0 ms | 0 (0–0) | 7.5 MB |
| /portfolios/park-hyatt-toronto | mobile | 67 (65–67) | 4.5 s (4403–4675ms) | 1.9 s | 81 ms | 0.315 (0.312–0.338) | 3.8 MB |
| /portfolios/park-hyatt-toronto | desktop | 91 (81–94) | 1.9 s (1540–3298ms) | 0.7 s | 0 ms | 0.02 (0.02–0.023) | 3.6 MB |
| /cherrypicked/cake-mix | mobile | 72 (71–73) | 10.2 s (9239–11520ms) | 1.8 s | 145 ms | 0.015 (0.015–0.015) | 4.9 MB |
| /cherrypicked/cake-mix | desktop | 89 (87–90) | 2.1 s (2058–2352ms) | 0.6 s | 0 ms | 0.005 (0.005–0.005) | 4.9 MB |

## Visual baselines and noise floor

`pnpm wf:baseline save`, then `compare` straight after with no change, at
1440, 820, 667 and 390 px (images in `.webflow-build/live-audit/baselines/`,
not in git). What differs between two untouched runs is the noise floor:

| Page | Noise floor |
| --- | --- |
| `/` | 1.1% at 820 (rows 2856–3405); 0% elsewhere |
| `/services` | 0.1–0.3% at 820/667/390 (tab feed) |
| `/post/*` | 0.2–3.5%, and the page height moves by 18–633 px (the related-posts list near the foot changes between loads) |
| all other key pages | 0% |

## Accessibility (wf:a11y --all-widths)

Serious failures only; no critical ones. `link-name` on every page;
`color-contrast` on 8 of 10; `link-in-text-block` on `/contact`. Full list
in `out/a11y.txt`. Keyboard and screen-reader checks are still a person's.

## Tracking (wf:tracking, data requests blocked)

GTM (GTM-TKM5QNH), GA4 (G-7W8K4TV2Y6), LinkedIn Insight (4086844) and the Meta
Pixel are on 10 of 10 pages. Each counts one page view. Ahrefs Analytics is in
the site head too. No cookie banner, Google consent mode on. http→https and
apex→www redirects keep the query string. Cloudflare Turnstile is on 10 pages
and Finsweet Attributes on 2.

## Domain (wf:domain)

Certificate Google Trust Services, expires 2027-01-30 (renews itself).
Domain thisisbonustrack.com, registrar GoDaddy, expires 2028-05-04. DNS at
GoDaddy.

## Heading outlines (wf:outline, live)

```text
## /
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  BONUSTRACK   << no space at a line break
  H2  Bonus Track, the creative content division of Pomp & Circumstance PR.
  H2  Selected Works
        H5  Join the P&C mailing list andsubscribe to CheRry Picked   << no space at a line break   << skipped a level
## /services
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
<< 0 h1 elements (expected 1)
## /works
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  Creative Marketing Case Studies
  H2  SPORTING LIFE x ADIDAS: Back-to-School
  H2  SHE'S MERCEDES POWER SUIT PROGRAM
  H2  SIMPLII SIDE HUSTLE
  H2  DERMALOGICA CIRCULAR HYDRATION
  H2  SPORT CHEK BACK TO SCHOOL
  H2  PARK HYATT TORONTO
  H2  NOBIS FALL/WINTER 2022 PREVIEW
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
## /liner-notes
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
  H2  Social Media Trends That Actually Matter vs. Pure Distractions in 2026
  H2  How Audiences Actually Decide to Follow a Brand
  H2  What 'Quality' Content Actually Looks Like in 2026 and Why It Wins
  H2  How to Build a UGC Program That Runs Without Legal Headaches
  H2  The Surprise-and-Delight Playbook That Won't Break the Bank
  H2  How to Turn Comments Into Content Ideas at Scale
  H2  Why LinkedIn Is Becoming the Hottest Platform for Personal Branding
  H2  The Rise of Nano-Influencers: Are Smaller Audiences More Valuable?
  H2  Social Media Myths Debunked: What Actually Works in 2025?
  H2  Pop Star to Business Mogul: How Artists Build Sustainable Brands
  H2  Interactive Content: The Secret Weapon for Higher Social Media Engagement
  H2  How to Build a Social Media Content Calendar that Drives Engagement
  H2  The Psychology Behind Viral Social Media Campaigns
  H2  Top Tools for Managing Your Brand’s Social Media Presence
  H2  The Role of User-Generated Content in Building Authenticity
  H2  The Power of Social Commerce: Turning Followers into Buyers
  H2  The Dos and Don’ts of Social Media Etiquette for Brands
  H2  The Art of Engagement: Creating Interactive Social Media Campaigns
  H2  Navigating Algorithm Changes: Staying Ahead in Social Media
  H2  How AI is Revolutionizing Social Media Marketing
  H2  From Likes to Loyalty: Cultivating Brand Advocates Online
  H2  The Power of Storytelling in Social Media Marketing
  H2  The Future of Social Media Content: What Trends to Watch in 2025
  H2  Instagram vs. TikTok: Which Platform Is Best for a Brand?
  H2  Influencer Marketing on a Budget: Fresh Approaches to Working With Micro-Influencers
  H2  How to Measure Success in Social Media Marketing
  H2  How to Balance Organic vs. Paid Content on Social Media
  H2  A Guide to Building a Personal Brand on Social Media
  H2  Launching a rebrand
  H2  Examples To Launch Your Rebrand
  H2  Brand Ambassador vs Brand Representative
  H2  Influencer Management Toronto
  H2  Creative Agency vs. Advertising Agency vs. Marketing Agency: What’s the Difference?
  H2  4 Brands That Collaborate With Small Influencers on Instagram
  H2  A Guide on How to Start Creating Content
  H2  Best Print Advertisements of 2021
  H2  What Does Experiential Marketing Mean?
  H2  WE'VE HIT PLAY!
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
<< 0 h1 elements (expected 1)
## /cherry-picked
H1  Serving The
H1  Cherry on Top
    H3  jOIN THE MAILING LIST AND SUBSCRIBE TO CHERRY PICKED   << skipped a level
<< 2 h1 elements (expected 1)
## /contact
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  Reach out
H1  Reach out
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
<< 2 h1 elements (expected 1)
## /fwb
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  Friends with Benefits
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
## /post/we-have-hit-play
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  WE'VE HIT PLAY!
  H2  Social Media Trends That Actually Matter vs. Pure Distractions in 2026
  H2  How Audiences Actually Decide to Follow a Brand
  H2  What 'Quality' Content Actually Looks Like in 2026 and Why It Wins
  H2  How to Build a UGC Program That Runs Without Legal Headaches
  H2  The Surprise-and-Delight Playbook That Won't Break the Bank
  H2  How to Turn Comments Into Content Ideas at Scale
  H2  Why LinkedIn Is Becoming the Hottest Platform for Personal Branding
  H2  The Rise of Nano-Influencers: Are Smaller Audiences More Valuable?
  H2  Social Media Myths Debunked: What Actually Works in 2025?
  H2  Pop Star to Business Mogul: How Artists Build Sustainable Brands
  H2  Interactive Content: The Secret Weapon for Higher Social Media Engagement
  H2  How to Build a Social Media Content Calendar that Drives Engagement
  H2  The Psychology Behind Viral Social Media Campaigns
  H2  Top Tools for Managing Your Brand’s Social Media Presence
  H2  The Role of User-Generated Content in Building Authenticity
  H2  The Power of Social Commerce: Turning Followers into Buyers
  H2  The Dos and Don’ts of Social Media Etiquette for Brands
  H2  The Art of Engagement: Creating Interactive Social Media Campaigns
  H2  Navigating Algorithm Changes: Staying Ahead in Social Media
  H2  How AI is Revolutionizing Social Media Marketing
  H2  From Likes to Loyalty: Cultivating Brand Advocates Online
  H2  The Power of Storytelling in Social Media Marketing
  H2  The Future of Social Media Content: What Trends to Watch in 2025
  H2  Instagram vs. TikTok: Which Platform Is Best for a Brand?
  H2  Influencer Marketing on a Budget: Fresh Approaches to Working With Micro-Influencers
  H2  How to Measure Success in Social Media Marketing
  H2  How to Balance Organic vs. Paid Content on Social Media
  H2  A Guide to Building a Personal Brand on Social Media
  H2  Launching a rebrand
  H2  Examples To Launch Your Rebrand
  H2  Brand Ambassador vs Brand Representative
  H2  Influencer Management Toronto
  H2  Creative Agency vs. Advertising Agency vs. Marketing Agency: What’s the Difference?
  H2  4 Brands That Collaborate With Small Influencers on Instagram
  H2  A Guide on How to Start Creating Content
  H2  Best Print Advertisements of 2021
  H2  What Does Experiential Marketing Mean?
  H2  WE'VE HIT PLAY!
H1  BONUSTRACK   << no space at a line break
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
<< 2 h1 elements (expected 1)
## /portfolios/park-hyatt-toronto
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break
H1  PARK HYATT TORONTO
H1  The Ask
H1  The work
H1  The result
H1  THE CHERRY ON TOP
H1  BONUSTRACK   << no space at a line break
        H5  Join the P&C Mailing list andSubscribe to Cherry Picked   << no space at a line break   << skipped a level
<< 6 h1 elements (expected 1)
## /cherrypicked/cake-mix
H1  Cherry On Top Cake Mix
      H4  Made in Canada   << skipped a level
      H4  100% Certified Fresh Creative
      H4  Delivering the Extra
    H3  jOIN THE MAILING LIST AND SUBSCRIBE TO CHERRY PICKED
```

## Inventory (read through `webflow-bonustrack`, 2026-11-20)

### Site

| Field | Value |
|---|---|
| Name (displayName) | Bonus Track Template |
| shortName | wf-bonus-track |
| Site ID | 62d59e99627a3f5bc7a3bec8 (the only site this server can reach) |
| Workspace ID | 629f79b62e4ec02ee9fe6d03 |
| Domains | `wf-bonus-track.webflow.io` (staging), `www.thisisbonustrack.com`, `thisisbonustrack.com` |
| Last published, site / staging | 2026-11-20T20:16:19.643Z |
| Last published, custom domains | 2026-10-09T21:05:08.767Z (both) |
| Last updated | 2026-11-20T20:16:27.865Z |
| Created | 2022-07-18T17:55:37.396Z |
| Timezone | America/Los_Angeles |
| Locales | Primary English (`en`), no secondary locales |
| Google tag IDs (site setting) | none |
| Data collection | disabled |

### Pages

18 pages in total. None are archived. The folder `Template` (id 64b84b0e2e330d5af94d4f30, path `/template`) is not returned by `list_pages`. It only shows up as the parent of Style Guide and as a form location.

| Title | Slug / published path | Folder / CMS template | Draft | Archived | Utility | Page custom code |
|---|---|---|---|---|---|---|
| Home | `/` | — | no | no | — | yes (og:url) |
| Services | `/services` | — | no | no | — | yes (og:url + Finsweet CMS Library tabs in footer) |
| Work | `/works` | — | no | no | — | yes (og:url) |
| Contact | `/contact` | — | no | no | — | yes (og:url) |
| FWB | `/fwb` | — | no | no | — | yes (style + og:url) |
| Liner Notes Blog | `/liner-notes` | — | no | no | — | yes (og:url) |
| Trend Report | `/trend-report` | — | no | no | — | yes (og:url) |
| Thank you ! | `/thank-you` | — | no | no | — | yes (og:url) |
| Shop Home | `/cherry-picked` | — | no | no | — | yes (og:url) |
| Style Guide | `/template/style-guide` | folder: Template | **yes** | no | — | yes (noindex + og:url) |
| Password | `/401` | — | no | no | **password** | yes (og:url) |
| 404 | `/404` | — | no | no | **404** | yes (og:url) |
| Blog Posts Template | `detail_post` → `/post` | CMS: Blog Posts | no | no | — | yes (og:url) |
| Portfolios Template | `detail_portfolios` → `/portfolios` | CMS: Portfolios | no | no | — | yes (og:url) |
| Cherry Pickeds Template | `detail_cherrypicked` → `/cherrypicked` | CMS: Cherry Pickeds | no | no | — | yes (Finsweet CMS Tabs + og:url) |
| Services Template | `detail_services` → `/services` | CMS: Services | no | no | — | yes (og:url), shouldPublish: false |
| Categories Template | `detail_category` → `/category` | CMS: Categories | no | no | — | yes (og:url), shouldPublish: false |
| Team Members Template | `detail_team` → `/team` | CMS: Team Members | no | no | — | yes (og:url), shouldPublish: false |

- The Services Template's collection path is also `/services`, the same as the static Services page.
- Team Members Template and Style Guide still use the stock "Gringo - Webflow HTML website template" SEO title and description.

### CMS collections

Item counts come from `pagination.total`, which includes drafts.

| Name | Slug | Items | Fields (name:type) |
|---|---|---|---|
| Blog Posts | `post` | 43 | seo-title:PlainText (req), post-summary:PlainText (req), date-posted:DateTime, post-body:RichText, image-1:Image, 2nd-paragraph:RichText, image-2:Image, 3rd-paragraph:RichText, image-3:Image, 4th-paragraph:RichText, image-4:Image, main-image:Image, thumbnail-image:Image, featured:Switch, color:Color, authors:Reference→Team Members, alt-text-for-blog-image:PlainText, name:PlainText, slug:PlainText. Field group "SEO" holds seo-title and post-summary. |
| Team Members | `team` | 5 | profile-picture:Image, bio:RichText, bio-summary:PlainText, job-title:PlainText, email:Email, phone-number:Phone, twitter-link:Link, instagram-link:Link, facebook-link:Link, linkedin-link:Link, icon-hover:Image, name:PlainText, slug:PlainText. The first item checked is lorem-ipsum template content. |
| Portfolios | `portfolios` | 10 | project-details:RichText, small-thumbnail:Image, thumbnail:Image, main-project-image:Image, caterogies:MultiReference→Categories, project-summary:PlainText, image-story-one-image:Image, image-story-1-description:PlainText, image-story-2-image:Image, image-story-2-description:PlainText, the-ask:PlainText, the-ask-image:Image, the-ask-image-description:PlainText, the-work-summary:PlainText, the-result:PlainText, the-work-image-1:Image, the-work-image-1-description:PlainText, the-work-image-2:Image, the-work-image-2-description:PlainText, the-work-image-3:Image, the-work-image-3-description:PlainText, cherry-on-top-text:PlainText, cherry-on-top-image-1:Image, cherry-on-top-image-2:Image, 3-social-media-post:Image, bottom-video:VideoLink, field-of-work:PlainText, sorting-by-number:Number, meta-title:PlainText, meta-description:PlainText, name:PlainText, slug:PlainText. Field group "SEO" holds meta-title and meta-description. |
| Categories | `category` | 9 | icon:Image, color:Color, name:PlainText, slug:PlainText |
| Services | `services` | 7 | main-para:PlainText, second-para:PlainText, button-1 … button-8:PlainText (8 fields), name:PlainText, slug:PlainText |
| Cherry Pickeds | `cherrypicked` | 9 | image:Image, price-2:PlainText, coming-soon:Switch, other-images:MultiImage, desc-2:PlainText, phrase:PlainText, shopify:Link, title:PlainText, service:Switch, order:Number, product-id:PlainText, meta-title:PlainText, meta-description:PlainText, name:PlainText, slug:PlainText. Field group "SEO" holds meta-title and meta-description. |

### Custom code

No registered or applied scripts. Site head: GTM, Google Search Console
verification, Ahrefs Analytics, LinkedIn Insight, Meta Pixel, Pinterest and
Facebook domain verification, and a `<style>` block. Site footer: GTM
noscript. Page code: `og:url` on every page; Finsweet CMS Library on
`/services` (footer), Finsweet CMS Tabs on the Cherry Pickeds template, a
`<style>` on `/fwb`, noindex on Style Guide. Embeds: a global CSS embed
(responsive type) in `Global | Embed Code`, SVG icons, a Shopify Buy Button on
the Cherry Pickeds template. All of it word for word in `ROLLBACK.md`.

### Forms

`list_forms` returned 84 records. They are repeated entries for the 5 distinct forms below.

| Form name | Fields | Pages (form element ID) |
|---|---|---|
| The Drop Subscription | Email | Home, Work, Trend Report, Thank you !, Services, Liner Notes Blog, FWB, Blog Posts Template, Portfolios Template, Contact, 404 (a separate element on each page) |
| The Drop Subscription | Email 4 | One shared element `0a46537e-4098-0d80-9123-9e6032e42e8b` (probably inside a component) on Home, Work, Trend Report, Thank you !, Services, Liner Notes Blog, FWB, Blog Posts Template, Portfolios Template, Contact, 404, Style Guide, Template folder |
| The Drop Subscription | Email 2 | Shop Home (`b129c3e7…`), Cherry Pickeds Template (`fe5ee99c…`) |
| Email Form | Company Name, Contact Name, Email, Budget | Contact (`d2b076a7-28a9-06cb-4f2c-9dbfaf2cffe7`) |
| Email Form | Name 2, Email 2, Budget 2, Message 2 | Contact (`61b69729-47df-f22e-bbdd-e6e4a062e5a5`) |

### Components

6 components:

| Name | Group | Instances |
|---|---|---|
| Cherries Header | — | 1 |
| Cherries Footer | — | 2 |
| Global \| Embed Code | 00 - Global | 13. Its description says it is always present inside "G \| Components". |
| C // Footer Carousel CTA | — | 7 |
| Global \| Components | 00 - Global | 13 |
| Global \| Navigation | 00 - Global | 12 |

### Not read

- **Applied scripts** on the site and on every page: `get_site_scripts` and `get_page_scripts` returned 404 "Custom code block not found". This most likely means none are applied (there are also no registered scripts), not that access was refused.
- **Template folder** (id 64b84b0e2e330d5af94d4f30): `list_pages` doesn't return it, so its settings and custom code weren't read.
- **Form field types and settings:** `list_forms` was too long to return in full. Only form names, field names, pages and element IDs were pulled from the saved output, so field types, required flags and notification settings weren't read.
- **`webflow_guide_tool` output** (113k characters) was too long to return and was not read beyond the session ID it issued. Only the list/get/read actions above were called; nothing was written.
- **Not read at all:** CMS item contents beyond one sample item per collection, and the elements inside components (props, contents).

## State of the Designer

The staging subdomain was published on **2026-11-20 20:16 UTC**, but the
custom domains were last published on 2026-10-09. Someone published the site
to staging today, and not from this repo. The Designer may hold changes that
are not live, and the next live publish would send them out. Ask who did it
before the first batch (webflow-audit › 6, step 5).

## Corrections to the earlier audit

The read-only audit earlier on 2026-11-20 said the only custom code was a
Finsweet tag on `/services`. In fact the site head and footer carry the
tracking and verification code above, and the Cherry Pickeds template has
Finsweet CMS Tabs and a Shopify embed.
