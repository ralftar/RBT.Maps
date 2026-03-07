# maps.rbt.no

One link that opens the right maps app, on any device.

## The problem

There is no standard for opening a map location natively. Android uses `geo:` intents, iOS and macOS intercept Apple Maps links, while on desktop Google Maps in the browser is the go-to. Pick one format and every other platform breaks.

Building detection into each project adds complexity — often a plain link is all you need.

## The fix

One URL that handles detection. Add `?q=` with a place, coordinates, or a query — done.

```
https://maps.rbt.no/?q=Hornindalsvatnet
```

### Platform behavior

| Platform | Redirects to |
|---|---|
| Android | Native maps app via `geo:` intent |
| iOS / macOS / iPadOS | Apple Maps |
| Windows / Linux | Google Maps (web) |
| In-app browsers | Tries native, falls back to Google Maps |

### Examples

```
https://maps.rbt.no/?q=Hornindalsvatnet
https://maps.rbt.no/?q=59.9139,10.7522
https://maps.rbt.no/?q=pizza+oslo
```

## How it works

The visitor's platform is detected client-side via user agent. The page immediately redirects to the appropriate maps URL using `location.replace()` — no history entry is pushed, so the back button returns to the previous page.

For in-app browsers (Facebook, Instagram, TikTok, etc.) and Android without a maps app installed, a 2-second fallback redirects to Google Maps web.

iPadOS 13+ reports as "Macintosh" in the user agent string and lands in the macOS branch — correct, since Apple Maps is the target for both.

## Privacy

No cookies. No data stored. IP addresses are processed for the HTTP connection but not logged. Visitor stats are anonymized.

## Hosting

Deployed to GitHub Pages via [GitHub Actions](.github/workflows/publish.yaml). Custom domain configured via [CNAME](CNAME).

## License

[MIT](LICENSE)
