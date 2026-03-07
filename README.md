# map.rbt.no

A universal map link that opens the native maps app on any device.

There is no standard for opening a map location natively — Android uses `geo:` intents, iOS and macOS intercept Apple Maps links, and desktop has no native app at all. Pick one format and every other platform breaks.

**map.rbt.no** solves this with a single URL that detects the platform and redirects accordingly.

## Usage

```
https://map.rbt.no/?q=Eiffel+Tower,+Paris
```

Add `?q=` with a place name, coordinates, or a search query.

### Platform behavior

| Platform | Redirects to |
|---|---|
| Android | Native maps app via `geo:` intent |
| iOS | Apple Maps |
| macOS / iPadOS | Apple Maps |
| Windows / Linux | Google Maps (web) |
| In-app browsers | Tries native, falls back to Google Maps |

## Self-hosting

```bash
docker build -t rbt-map .
docker run -p 8080:80 rbt-map
```

## License

[Beer-ware](https://en.wikipedia.org/wiki/Beerware) — see the source for details.
