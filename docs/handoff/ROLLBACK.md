# Rollback

Rollback point for Bonus Track (Webflow site `62d59e99627a3f5bc7a3bec8`, www.thisisbonustrack.com) before any change made from this repo.

- **Git tag:** `rollback-2026-11-20`: the repo as created from wf-template 1.0.0, with no code on the site. The live site loads nothing from this repo (no loader yet).
- **Live state captured:** 2026-11-20, from the published HTML (custom domains last published 2026-10-09 21:05 UTC), and checked against the Designer through the `webflow-bonustrack` MCP: site head and footer code match word for word. No registered or applied scripts (API), no loader.
- **Caution:** the staging subdomain was published on 2026-11-20 20:16 UTC, not from this repo. The Designer may hold changes that are not live yet.
- **Webflow backup:** not made yet ([Person], see below).

## How to roll back

1. **Custom code:** paste the blocks below back word for word: Site settings › Custom code (head, footer); each page's Page settings › Custom code; each Embed on the canvas. Publish to staging, compare, then publish live after the word "publish".
2. **Loader:** none installed yet. Once one is, point `RELEASE` in the head snippet back at the previous tag, or remove the loader snippets to return to this state.
3. **Webflow backup:** Site settings › Backups › restore the backup named `2026-11-20 before wf-template` (restores the Designer; then publish).

Each step is possible today: the code is below, the site has no loader, and a backup can be made by a person on the site.

## Site head code (Site settings › Custom code › Head)

As published, word for word:

```html
<!-- Start — Google Tag Manager -->
<script>
  (function (w, d, s, l, i) {
    w[l] = w[l] || [];
    w[l].push({ "gtm.start": new Date().getTime(), event: "gtm.js" });
    var f = d.getElementsByTagName(s)[0],
      j = d.createElement(s),
      dl = l != "dataLayer" ? "&l=" + l : "";
    j.async = true;
    j.src = "https://www.googletagmanager.com/gtm.js?id=" + i + dl;
    f.parentNode.insertBefore(j, f);
  })(window, document, "script", "dataLayer", "GTM-TKM5QNH");
</script>
<!-- End — Google Tag Manager -->

<!-- BrandVM Search Console-->
<meta name="google-site-verification" content="Ya5FpO3SEi9XJUckQ_eGbjzr4Ec8x5dlQMNWYbyOZbs" />

<script src="https://analytics.ahrefs.com/analytics.js" data-key="MOWiiF+NLlMqRphCBuMULw" async></script>

<!-- Start — LinkedIn Tracker -->
<script type="text/javascript">
  _linkedin_partner_id = "4086844";
  window._linkedin_data_partner_ids = window._linkedin_data_partner_ids || [];
  window._linkedin_data_partner_ids.push(_linkedin_partner_id);
</script>
<script type="text/javascript">
  (function (l) {
    if (!l) {
      window.lintrk = function (a, b) {
        window.lintrk.q.push([a, b]);
      };
      window.lintrk.q = [];
    }
    var s = document.getElementsByTagName("script")[0];
    var b = document.createElement("script");
    b.type = "text/javascript";
    b.async = true;
    b.src = "https://snap.licdn.com/li.lms-analytics/insight.min.js";
    s.parentNode.insertBefore(b, s);
  })(window.lintrk);
</script>
<noscript>
  <img
    height="1"
    width="1"
    style="display: none"
    alt=""
    src="https://px.ads.linkedin.com/collect/?pid=4086844&fmt=gif"
  />
</noscript>
<!-- End — LinkedIn Tracker -->

<!-- Start - Meta Pixel Code -->
<script>
  !(function (f, b, e, v, n, t, s) {
    if (f.fbq) return;
    n = f.fbq = function () {
      n.callMethod ? n.callMethod.apply(n, arguments) : n.queue.push(arguments);
    };
    if (!f._fbq) f._fbq = n;
    n.push = n;
    n.loaded = !0;
    n.version = "2.0";
    n.queue = [];
    t = b.createElement(e);
    t.async = !0;
    t.src = v;
    s = b.getElementsByTagName(e)[0];
    s.parentNode.insertBefore(t, s);
  })(
    window,
    document,
    "script",
    "https://connect.facebook.net/en_US/fbevents.js"
  );
  fbq("init", "598292061909934");
  fbq("track", "PageView");
</script>
<noscript>
  <img
    height="1"
    width="1"
    style="display: none"
    src="https://www.facebook.com/tr?id=598292061909934&ev=PageView&noscript=1"
  />
</noscript>
<!-- End – Meta Pixel Code -->

<!-- Site Verifications -->
<meta name="p:domain_verify" content="e43bcea03fbbf5f5cfee0116dda93de8" />

<meta
  name="facebook-domain-verification"
  content="yri3izwd3zfv81ith0byxd2kv33nwo"
/>

<style>
  body {
    height: 100vh;
    width: 100vw;
    overflow-x: hidden;
  }
  .global-embed-code {
    display: none;
    z-index: -99999;
  }
</style>
```

## Site footer code (Site settings › Custom code › Footer)

```html
<!-- Start — Google Tag Manager -->
<!-- Google Tag Manager (noscript) -->
<noscript>
  <iframe
    src="https://www.googletagmanager.com/ns.html?id=GTM-TKM5QNH"
    height="0"
    width="0"
    style="display: none; visibility: hidden"
  >
  </iframe>
</noscript>
<!-- End Google Tag Manager (noscript) -->
<!-- End — Google Tag Manager -->
```

## Page code

Every page's head code (Page settings › Custom code), as the API returned it on 2026-11-20. Template pages bind the slug in `og:url`.

| Page | Head | Footer |
|---|---|---|
| Home | `<meta property="og:url" content="https://www.thisisbonustrack.com/" />` | — |
| Services | `<meta property="og:url" content="https://www.thisisbonustrack.com/services" />` | see below |
| Work | `<meta property="og:url" content="https://www.thisisbonustrack.com/works" />` | — |
| Contact | `<meta property="og:url" content="https://www.thisisbonustrack.com/contact" />` | — |
| FWB | `<style>body { overflow-x: hidden; }</style>` + `<meta property="og:url" content="https://www.thisisbonustrack.com/fwb" />` | — |
| Liner Notes Blog | `<meta property="og:url" content="https://www.thisisbonustrack.com/liner-notes" />` | — |
| Trend Report | `<meta property="og:url" content="https://www.thisisbonustrack.com/trend-report" />` | — |
| Thank you ! | `<meta property="og:url" content="https://www.thisisbonustrack.com/thank-you" />` | — |
| Shop Home | `<meta property="og:url" content="https://www.thisisbonustrack.com/cherry-picked" />` | — |
| Style Guide | `<meta name="robots" content="noindex">` + `<meta property="og:url" content="https://www.thisisbonustrack.com/template/style-guide" />` | — |
| Password (401) | `<meta property="og:url" content="https://www.thisisbonustrack.com/401" />` | — |
| 404 | `<meta property="og:url" content="https://www.thisisbonustrack.com/404" />` | — |
| Blog Posts Template | `<meta property="og:url" content="https://www.thisisbonustrack.com/post/{{wf {&quot;path&quot;:&quot;slug&quot;,&quot;type&quot;:&quot;PlainText&quot;\} }}" />` | — |
| Portfolios Template | `…/portfolios/{{wf slug}}` og:url (same pattern) | — |
| Services Template | `…/services/{{wf slug}}` og:url | — |
| Categories Template | `…/category/{{wf slug}}` og:url | — |
| Team Members Template | `…/team/{{wf slug}}` og:url | — |
| Cherry Pickeds Template | see below | — |

The longer blocks, word for word:

### Cherry Picked template (/cherrypicked/*), head

```html
<!-- [Attributes by Finsweet] CMS Tabs -->
<script async src="https://cdn.jsdelivr.net/npm/@finsweet/attributes-cmstabs@1/cmstabs.js"></script>
```

### /fwb, head

```html
<style>body { overflow-x: hidden; }</style>
```

### /services, before </body>

```html
<script src="https://cdn.jsdelivr.net/npm/@finsweet/cms-library@1/cms-library.js"></script>
<script>
(function() {
var fsComponent = new FsLibrary('.as-dynamic-feed')

fsComponent.tabs({
  tabComponent: '.as-tabs',
  tabName: '.as-tab-name',
  resetIx: true
})
})();
</script>
```

## Embeds on the canvas

Read from the published pages (one sample per template). The Storefront token in the Shopify embed is a public, read-only token that Shopify's Buy Button publishes on the page by design.

### `global-embed-code w-embed` (/cherry-picked, /contact, /fwb, /, /liner-notes, Portfolio template (/portfolios/*), Blog post template (/post/*), /services, /works)

```html
<div class="global-embed-code w-embed"><style>
  /* =========================
  Responsive Typography
  ========================= */

  :root {
    /* Fallback for browsers without clamp() */
    font-size: 16px; 
    font-size: clamp(15px, 0.95vw, 16px);
  }
  @supports (color: color(display-p3 1 1 1)) {
    :root{
      --color--tropical-indigo: color(display-p3 0.823529 0.788235 1.000000 / 1.000000);
      --color--oxford-blue: color(display-p3 0.027451 0.070588 0.231373 / 1.000000);
      --color--uranian-blue: color(display-p3 0.701961 0.819608 0.937255 / 1.000000);
      /*--color--orange-red: color(display-p3 1.000000 0.203922 0.000000 / 1.000000);*/
      --color--fire-engine: color(display-p3 0.803922 0.000000 0.094118 / 1.000000);
      --color--chrysler-blue: color(display-p3 0.117647 0.207843 0.898039 / 1.000000);
      --color--lime: color(display-p3 0.815686 1.000000 0.000000 / 1.000000);
      --color--neon-blue: color(display-p3 0.356863 0.431373 1.000000 / 1.000000);
    }
  }

  @media only screen and (max-width: 991px) {
    :root {
      /* Fallback for older browsers */
      font-size: 16px;
      font-size: 1.7125vw;
    }
  }

  @media only screen and (max-width: 767px) {
    :root {
      font-size: 15px;
      font-size: 3.2375vw;
    }
  }

  @media only screen and (max-width: 478px) {
    :root {
      /* Fallback for older browsers */
      font-size: 15px;
      font-size: clamp(14px, 4vw, 16px);
    }
  }

  /* =========================
  Custom Style Overwriting
  ========================= */

  html {
    /* Uncomment for smooth scrolling (modern browsers only) */
    /* scroll-behavior: smooth; */
  }

  * {
    /* Smoothing and rendering */
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-rendering: optimizeLegibility;

    /* Fallback for older browsers */
    unicode-bidi: isolate;
    text-size-adjust: 100%;
    text-underline-offset: 0.24em;

    /* Box model consistency */
    box-sizing: border-box;
  }

  @supports (font-variation-settings: normal) {
    body {   
      font-feature-settings: 'cv12' on, 'cv13' on;
    }
  }

  textarea {
    resize: none; /* Disable resizing */
  }

  .article-rich-text > div:first-child > :first-child {
    margin-top: 0; /* Reset top margin */
  }

  .article-rich-text > div:first-child > :last-child {
    margin-bottom: 0; /* Reset bottom margin */
  }

  /* Animation for the first right to left marquee */
  @keyframes slide {
    0% {
      transform: translateX(0%);
    }
    100% {
      transform: translateX(-100%);
    }
  }

  .logo-animate {
    animation: slide 16s infinite linear; /* Adjust the seconds for a slower or faster animation */
  }

  /* =========================
  Attribute Styles
  ========================= */

  [blog-card-description] {
    display: -webkit-box;
    -webkit-line-clamp: 2; /* Limit text to 2 lines */
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;

    /* Fallback for older browsers */
    white-space: nowrap;
    overflow: hidden;
  }

  [scroll-show="false"] {
    scrollbar-width: none; /* Firefox */
    -ms-overflow-style: none; /* Internet Explorer, Edge */
  }

  [scroll-show="false"]::-webkit-scrollbar {
    display: none; /* Chrome, Safari, Opera */
  }

  input[type="checkbox"]:checked ~ .text-menu-label,
  input[type="radio"]:checked ~ .text-menu-label {
    color: white; /* Styling checked inputs */
  }


  /* =========================
  Real Page Styling
  ========================= */

  .pre-loader-pillar:nth-child(1){transition-delay: 0.06s;}
  .pre-loader-pillar:nth-child(2){transition-delay: 0.12s;}
  .pre-loader-pillar:nth-child(3){transition-delay: 0.18s;}
  .pre-loader-pillar:nth-child(4){transition-delay: 0.29s;}
  .pre-loader-pillar:nth-child(5){transition-delay: 0.35s;}
  .pre-loader-pillar:nth-child(6){transition-delay: 0.41s;}
  .pre-loader-pillar:nth-child(7){transition-delay: 0.46s;}
  .pre-loader-pillar:nth-child(8){transition-delay: 0.52s;}

  .wrapper::before, .wrapper::after{
    display:none;
  }

  [f-c-background="red"]{
    color:var(--color--orange-red) !important;
  }
  [f-c-background="red"]:hover{
    background-color:var(--color--orange-red) !important;
  }
  [f-c-page-bg="tropical-indigo"]:hover{
    color:var(--color--tropical-indigo) !important;
  }
  [f-c-page-bg="uranian-blue"]{
    background-color:var(--color--uranian-blue) !important;
  }
  [f-c-page-bg="uranian-blue"]:hover{
    color:var(--color--uranian-blue) !important;
  }

</style></div>
```

### `curssorcherry w-embed` (/cherry-picked, Cherry Picked template (/cherrypicked/*))

```html
<div class="curssorcherry w-embed"><svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M1.52505 13.1799L13.2792 1.42578M13.2792 1.42578V12.7098M13.2792 1.42578H1.99522" stroke="currentColor" stroke-width="1.35625" stroke-linecap="round" stroke-linejoin="round"/>
</svg></div>
```

### `html-embed-2 w-condition-invisible w-embed w-script` (Cherry Picked template (/cherrypicked/*))

```html
<div class="html-embed-2 w-condition-invisible w-embed w-script"><div id='product-component-1689544559504'></div>
<script type="text/javascript">
/*<![CDATA[*/
(function () {
  var scriptURL = 'https://sdks.shopifycdn.com/buy-button/latest/buy-button-storefront.min.js';
  if (window.ShopifyBuy) {
    if (window.ShopifyBuy.UI) {
      ShopifyBuyInit();
    } else {
      loadScript();
    }
  } else {
    loadScript();
  }
  function loadScript() {
    var script = document.createElement('script');
    script.async = true;
    script.src = scriptURL;
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(script);
    script.onload = ShopifyBuyInit;
  }
  function ShopifyBuyInit() {
    var client = ShopifyBuy.buildClient({
      domain: 'cc00f5.myshopify.com',
      storefrontAccessToken: '6e0625bd99297830b621ce73a940e00c',
    });
    ShopifyBuy.UI.onReady(client).then(function (ui) {
      ui.createComponent('product', {
        id: '8396204015912',
        node: document.getElementById('product-component-1689544559504'),
        moneyFormat: '%24%7B%7Bamount%7D%7D',
        options: {
  "product": {
    "styles": {
      "product": {
        "@media (min-width: 601px)": {
          "max-width": "calc(25% - 20px)",
          "margin-left": "20px",
          "margin-bottom": "50px"
        }
      },
      "button": {
        "font-family": "Garamond, serif",
        "font-size": "14px",
        "padding-top": "15px",
        "padding-bottom": "15px",
        ":hover": {
          "background-color": "#a92024"
        },
        "background-color": "#bc2328",
        ":focus": {
          "background-color": "#a92024"
        },
        "padding-left": "100px",
        "padding-right": "100px"
      },
      "quantityInput": {
        "font-size": "14px",
        "padding-top": "15px",
        "padding-bottom": "15px"
      }
    },
    "buttonDestination": "checkout",
    "contents": {
      "img": false,
      "title": false,
      "price": false
    },
    "text": {
      "button": "Buy now"
    }
  },
  "productSet": {
    "styles": {
      "products": {
        "@media (min-width: 601px)": {
          "margin-left": "-20px"
        }
      }
    }
  },
  "modalProduct": {
    "contents": {
      "img": false,
      "imgWithCarousel": true,
      "button": false,
      "buttonWithQuantity": true
    },
    "styles": {
      "product": {
        "@media (min-width: 601px)": {
          "max-width": "100%",
          "margin-left": "0px",
          "margin-bottom": "0px"
        }
      },
      "button": {
        "font-family": "Garamond, serif",
        "font-size": "14px",
        "padding-top": "15px",
        "padding-bottom": "15px",
        ":hover": {
          "background-color": "#a92024"
        },
        "background-color": "#bc2328",
        ":focus": {
          "background-color": "#a92024"
        },
        "padding-left": "100px",
        "padding-right": "100px"
      },
      "quantityInput": {
        "font-size": "14px",
        "padding-top": "15px",
        "padding-bottom": "15px"
      }
    },
    "text": {
      "button": "Add to cart"
    }
  },
  "option": {},
  "cart": {
    "styles": {
      "button": {
        "font-family": "Garamond, serif",
        "font-size": "14px",
        "padding-top": "15px",
        "padding-bottom": "15px",
        ":hover": {
          "background-color": "#a92024"
        },
        "background-color": "#bc2328",
        ":focus": {
          "background-color": "#a92024"
        }
      }
    },
    "text": {
      "total": "Subtotal",
      "button": "Checkout"
    }
  },
  "toggle": {
    "styles": {
      "toggle": {
        "font-family": "Garamond, serif",
        "background-color": "#bc2328",
        ":hover": {
          "background-color": "#a92024"
        },
        ":focus": {
          "background-color": "#a92024"
        }
      },
      "count": {
        "font-size": "14px"
      }
    }
  }
},
      });
    });
  }
})();
/*]]>*/
</script></div>
```

### `w-embed` (Cherry Picked template (/cherrypicked/*))

```html
<div class="w-embed"><style>
.product-gallery-tab-pane{
aspect-ratio: 1/1;
}
</style></div>
```

### `embed-icon w-embed` (/contact, /fwb, /, /liner-notes, Portfolio template (/portfolios/*), Blog post template (/post/*), /services, /works)

```html
<div class="embed-icon w-embed"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><title>x</title><g stroke-linejoin="round" stroke-linecap="round" stroke-width="1.5" fill="none" stroke="#07123B"><path d="M18 6L6 18"></path><path d="M6 6l12 12"></path></g></svg></div>
```

### `video w-condition-invisible w-dyn-bind-empty w-video w-embed` (Portfolio template (/portfolios/*))

Empty CMS video embed, bound to a field (nothing to restore).

## Not covered

- The `Template` folder's own settings (the API doesn't list folders).
- Embeds on pages not sampled from the published HTML (Trend Report, Thank you, 404, Password, Style Guide): they use the same global components; read them from the Designer before changing them.
