# Status

Every request for Bonus Track, in the wording of the change tracker (Figma
"Documentations" › 01 · Change tracker, rows BT-01…BT-18). States: not
started · in progress · on staging · live · dropped (why).

**Count (2026-11-20):** 0 of 18 live, 0 on staging, 1 in progress (BT-13), 17 not started.

| ID | Area | Request | Baseline (tracker) | State | Batch | Date |
| --- | --- | --- | --- | --- | --- | --- |
| BT-01 | SEO | Organization + WebSite schema in the site head; page-level schema | No JSON-LD on any page. | not started | | |
| BT-02 | SEO | One H1 per page (49 of 61 pages wrong) | /services and /liner-notes have none; blog posts 2–5. | not started | | |
| BT-03 | SEO | Footer newsletter title: H5 → not a heading | First heading on every page. | not started | | |
| BT-04 | SEO | og:image on 32 pages | | not started | | |
| BT-05 | Accessibility | alt attributes on every page's images | | not started | | |
| BT-06 | Content | Copyright year (2022 → current, set automatically) | | not started | | |
| BT-07 | Code | Fix the "Cherry Picked" menu link that points to # | | not started | | |
| BT-08 | Accessibility | Menu button: a real `<button>` with aria-expanded; a close (×) icon | Today an SVG; keyboard users can't open the menu. | not started | | |
| BT-09 | Content | Fix the typo "where an how" on /services | | not started | | |
| BT-10 | Accessibility | Footer newsletter: label and submit button | | not started | | |
| BT-11 | Code | Fix the CSP console errors on every page | A Cloudflare challenge script refused a data: fetch. | not started | | |
| BT-12 | Speed | Lift /works speed (72 mobile, 82 desktop) | LCP 14 s on mobile. | not started | | |
| BT-13 | Template | Move the site onto wf-template | No repo today; a decision for the team. | in progress: repo, workspace, baseline and rollback point done; loader and parity release not started | setup | 2026-11-20 |
| BT-14 | Design | Hero: statement, reel and two CTAs | Redesign proposal. | not started | | |
| BT-15 | Design | Services page: real H1, one section per service with anchors | Redesign proposal. | not started | | |
| BT-16 | Design | Work grid: captions with results, linked case studies | Redesign proposal. | not started | | |
| BT-17 | Design | Menu: descriptors for Liner Notes, Cherry Picked, FWB | Redesign proposal. | not started | | |
| BT-18 | Design | Footer: newsletter, social icons, "A Pomp & Circumstance company" | Redesign proposal. | not started | | |

Gate: the person confirms nothing is missing from this list.

Fixes BT-01…BT-12 go batch by batch, lowest risk first, each with the
person's go-ahead (webflow-audit › 6). BT-14…BT-18 are new client-facing
content and need the client's approval.
