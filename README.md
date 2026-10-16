# PhotoCompositor

BusinessDesk image compositor — a single HTML page (`Business_Desk_Image_Compositor.html`) that builds 1920×1080 JPGs from one or more photos, with background removal, colour treatments, and shared logos/backgrounds.

## Logos & backgrounds library

Shared branding images live in [`assets/`](assets/), described by [`assets/manifest.json`](assets/manifest.json). Each image remembers how it should be placed:

```json
{
  "version": 1,
  "items": [
    {
      "id": "stock-and-trade",
      "file": "stock-and-trade.png",
      "name": "Stock & Trade banner",
      "role": "top",
      "fit": "free",
      "anchor": "tc",
      "width": 100,
      "zoom": 100,
      "x": 0,
      "y": 0,
      "opacity": 100
    }
  ]
}
```

| Field     | Values | Meaning |
|-----------|--------|---------|
| `role`    | `top` / `behind` | Drawn above everything (never treated), or behind the photos (shows through cut-outs, treatment applies) |
| `fit`     | `fill` / `free` | Cover the whole frame, or size freely |
| `anchor`  | `tl` `tc` `tr` `ml` `c` `mr` `bl` `bc` `br` | Corner/edge a `free` image is pinned to |
| `width`   | 2–150 | `free` only: width as % of the 1920px frame |
| `zoom`    | 100–300 | `fill` only: zoom % beyond cover |
| `x`, `y`  | number | `free`: pixel offset from the anchor. `fill`: pan, −100 to 100 |
| `opacity` | 0–100 | Layer opacity % |

### Who sees what

The library is always read from the `assets/` folder next to the page, so on the hosted site (GitHub Pages) it just loads. Nobody has to pick a folder.

- **Hosted site, normal URL:** library tiles and **+ Add image** (one-off, not saved) only. No folder or save controls.
- **Opened from disk, or hosted URL with `?edit`** (e.g. `…/Business_Desk_Image_Compositor.html?edit`): adds **Connect folder**, **Save to library** and **Delete** for maintaining the library.

### Adding to the library (maintainers)

1. Open your local copy of the compositor in **Chrome or Edge**.
2. In **Logos & backgrounds**, click **Connect folder** and choose this repo's `assets/` folder. You only do this once per browser.
3. Click **+ Add image**, set placement, give it a name and click **Save to library**. The image and the manifest entry are written into `assets/`.
4. Commit and push `assets/`. GitHub Pages picks it up for everyone.

In other browsers, **Save to library** downloads the image and an updated `manifest.json` instead. Copy both into `assets/`.

You can also add an image by hand: drop it into `assets/` and add an entry to `manifest.json` using the fields above.
