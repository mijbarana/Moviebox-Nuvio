# MovieBox Nuvio Plugin

A Nuvio provider package adapted from the supplied `moviebox.js` file.

## Files

- `manifest.json` — Nuvio repository manifest with one MovieBox scraper entry.
- `providers/moviebox.js` — bundled single-file provider exported as `module.exports = { getStreams }`.

## Dependency / runtime compatibility

- Uses `require("crypto-js")`, which is listed as an available module in the Nuvio plugin provider template/runtime documentation. No separate `npm install` is needed inside Nuvio.
- Uses the runtime's global `fetch`, `URL`, `Set`, and `console`; it does not import Node built-ins or use `Buffer`/`process`.
- Async logic is already compiled to promise/generator helpers; there are no raw `async function` or `await` tokens required by the runtime.
- `getStreams(tmdbId, mediaType, season, episode)` returns an array and now catches top-level provider errors, returning `[]` on failure.

## Install from GitHub

1. Upload this folder's contents to a public GitHub repository (keep `manifest.json` at the repository root and `providers/moviebox.js` at this exact path).
2. In Nuvio, open **Settings → Plugins** and add the raw URL for your repository's `manifest.json`, for example:
   `https://raw.githubusercontent.com/USERNAME/REPOSITORY/refs/heads/main/manifest.json`
3. Refresh the plugin list and enable MovieBox.
4. Test playback in Nuvio. API endpoints and third-party source behavior can change, so a successful syntax check does not guarantee live streams will always resolve.

## Notes

- This provider queries TMDB and MovieBox endpoints; it is not a generic GitHub JSON fetcher.
- The source includes a TMDB API key and MovieBox request-signing constants. Treat the repository as public code: client-side keys/constants are visible to anyone who can read the provider. If you did not create or control those credentials, verify you are permitted to redistribute them.
- Use only content and sources you are authorized to access.
