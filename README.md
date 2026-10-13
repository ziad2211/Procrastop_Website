# Procrastop website

The marketing, help and legal site for [Procrastop](https://apps.apple.com/app/id6818837590),
a one-time purchase iPhone to-do list. Static HTML, CSS and one small script,
served by GitHub Pages. No build step and no dependencies.

## Pages

Seven, and only seven. Anything that does not fit one of them does not belong
on the site.

| File | Purpose |
| --- | --- |
| `index.html` | The marketing home page |
| `guide.html` | How to use the app, for people who have it |
| `faq.html` | Short answers to the common questions |
| `troubleshoot.html` | What to do when something is not working |
| `support.html` | How to get help, and what to include |
| `privacy.html` | Privacy Policy, required by the App Store |
| `terms.html` | Terms of Use |

Every page carries the same header, navigation and footer. Adding a page means
adding it to the `.nav-links` list and the `.footer-links` list on all of them,
and to `sitemap.xml`.

## What goes on the site, and what does not

The site exists to introduce the product, help people use it, and carry the
legal and support information a launch needs. It is deliberately **not** a
complete account of how the app works.

Before adding anything, check that it is something a visitor actually needs.
Do not publish exact intervals, counts, thresholds, queue behaviour or the
internal rules behind a feature. Name a feature and say what it gives you, not
how it does it.

## Editing

Shared values live in one place, `assets/config.js`: the app name, developer
name, support email, App Store URL, the released version, the colour and the
"last updated" date that the legal pages print. Change them there and every
page follows. `version` must match `version` in the app's `app.json`.

Everything else is plain HTML. `assets/styles.css` holds the whole design, and
`assets/site.js` fills in the config values, drives the mobile navigation menu
and fades sections in as they scroll into view.

## Screenshots

`assets/screenshots/` holds real captures from the app running on an iPhone
simulator, not mockups. They are 603 × 1311, half of the device's native
resolution, which is what the layout is sized for.

Three of them, deliberately: `app-list.png` and `app-pressure.png` on the home
page, both reused on the Guide alongside `guide-swipe.png`. `app-list.png` is
also the social card image.

The Guide's "Add your first task" section has no screenshot on purpose. Both
ways of adding a task put the whole creation flow on screen at once, which is
more of the app's workings than the site should publish, so that section is
text only.

Replace them when the UI changes, keeping the same aspect ratio so the layout
holds. Watch for captures that show stale defaults: the timeframe ranges in the
section headings come from settings, so a screenshot taken on an old install
can disagree with what a new one shows.

A clean capture: reinstall the app on the simulator so it starts on the shipped
defaults, load demo data from Settings → About → Load Sample Tasks (dev builds
only), set a tidy status bar with
`xcrun simctl status_bar <udid> override --time 9:41 --batteryState discharging --batteryLevel 100 --wifiBars 3 --cellularBars 4`,
screenshot with `xcrun simctl io <udid> screenshot`, halve it with
`sips -Z 1311`, then `xcrun simctl status_bar <udid> clear`.

## Universal Links

`.well-known/apple-app-site-association` claims
`/Procrastop_LandingPage/?title=…&due=…` for the app, so a shared-task link
opens Procrastop when it is installed and falls back to this site when it is
not. The path has to match the one in the app's `src/lib/share.ts` and the
`applinks:` entry in its entitlements. The feature that produces those links is
currently switched off in the app, so nothing on the site mentions it, but the
file is kept in step with the code.

## Accuracy

Every claim on this site was written against the app's source. If a feature is
renamed, removed or disabled in the app, update the copy here too. The Guide,
the FAQ and the Troubleshoot page are the ones that drift first.

## Local preview

```bash
python3 -m http.server 8099
```

Then open <http://127.0.0.1:8099/>. Opening the files directly with `file://`
works too, but relative asset paths behave differently, so the server is more
faithful to GitHub Pages.

## Credits

- **Development:** Ziad Ismail

The footer credit on every page is driven by `credits` in `assets/config.js`.
The copyright line beside it is separate and names the publisher.
