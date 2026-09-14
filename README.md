# testWebsites

This repository contains sample websites to use for testing. Each site is a single, self-contained
HTML file (inline CSS + JS, no build step) served directly by GitHub Pages from the `main` branch root.

## Live sites

| Site | Vertical | Live URL | Source |
| --- | --- | --- | --- |
| TravelHub | Travel booking | [travelhub.html](https://nitaradhakrishnan.github.io/testWebsites/travelhub.html) | [`travelhub.html`](travelhub.html) |
| GadgetGrid | Electronics retail | [gadgetgrid.html](https://nitaradhakrishnan.github.io/testWebsites/gadgetgrid.html) | [`gadgetgrid.html`](gadgetgrid.html) |
| TravelHub Sign In | Travel booking | [signin.html](https://nitaradhakrishnan.github.io/testWebsites/signin.html) | [`signin.html`](signin.html) |
| GadgetGrid Sign In | Electronics retail | [signin.html?site=gadgetgrid](https://nitaradhakrishnan.github.io/testWebsites/signin.html?site=gadgetgrid) | [`signin.html`](signin.html) |

## What each site gives you

Both sites expose the same set of testable interactions, so a tag or measurement setup can be
validated against either one:

- Page view on load
- Site search (query + category)
- Product / listing view (title click)
- Add to cart, buy now
- Cart line-item removal with running subtotal
- Checkout and order placement
- Account sign-up and sign-in
- Newsletter subscribe
- Support / contact form submission
- Cookie consent banner with Accept and Decline wired to the consent library

Neither site collects address or payment details. Checkout is two buttons that fire notifications —
there is no payment form to fill in. The only text inputs on either page are search, newsletter email,
sign-up (name / email / password) and the support form (name / email / reference / message).

Both sites use an `anon_customer_id` first-party cookie as a pseudonymous browser identifier.
Separate `th_session_id` and `gg_session_id` cookies represent their demo sign-in sessions.
Signing in preserves the anonymous ID, while signing out removes that site's session and rotates
the anonymous ID.

## Tag configuration

Both pages load the AAT script and register a tag ID near the bottom of the file:

```js
amzn('setRegion', 'NA');
amzn('setStage', 'beta');
amzn('addTag', '<tag-id>');
amzn('trackEvent', 'PageView');
```

`gadgetgrid.html` currently reuses the same tag ID as `travelhub.html` so it works out of the box.
Swap it for your own tag ID if you want this site's traffic reported separately.

## Adding a new test site

1. Copy an existing HTML file and rename it, for example `cp gadgetgrid.html mysite.html`.
2. Keep everything in the one file — no external CSS, JS, or assets. That keeps each site
   independently reviewable and avoids cross-site breakage.
3. Update the tag ID if your test needs its own reporting.
4. Add a row to the Live sites table above.
5. Open a pull request against `main`.

Once merged, GitHub Pages publishes it at
`https://nitaradhakrishnan.github.io/testWebsites/<filename>.html` within a minute or two.

## Notes

- Never commit real personal data, credentials, or production tag IDs. These pages are public.
- Pages is configured to deploy from the root of `main`, so anything merged to `main` goes live.
