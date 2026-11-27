# AlexTowbinPhotographyData

Photo titles, order, collections and other choices for
[Alex Towbin Photography](https://photo.alextowbin.com/).
The site's code lives in
[towbinaj/AlexTowbinPhotography](https://github.com/towbinaj/AlexTowbinPhotography).

This repo is kept separate on purpose: the owner's editing key only has
access to this repo, so it can never change the site's code, its build, or
its secrets. Everything here is public (it only holds what the site shows
anyway, plus which photos are hidden).

## `curation.json`
You don't need to edit it by hand. The phone editor app
(https://photo.alextowbin.com/edit/) writes it; every save is a commit here.

```json
{
  "titles":      { "<photo id>": "Title" },
  "order":       ["<photo id>", "..."],
  "collections": [{ "name": "Series", "photos": ["<photo id>", "..."] }],
  "highlights":  ["<photo id>", "..."],
  "tags":        ["Street", "..."],
  "photo_tags":  { "<photo id>": ["Street", "..."] },
  "locations":   { "<photo id>": { "level": "city", "gid": 261745, "city": "Heraklion",
                                   "region": "Crete", "country": "Greece", "cc": "GR" } },
  "hidden":      ["<photo id>", "..."],
  "published":   ["<photo id>", "..."],
  "drafts_from": "2026-11-18T16:45:00Z",
  "on_work":     ["<photo id>", "..."],
  "off_work":    ["<photo id>", "..."],
  "no_place":    ["<photo id>", "..."]
}
```

- `titles`: optional per photo; untitled photos show the date.
- `order`: the **Work page** order. Photos not listed yet come first.
- `collections`: named series, each with its photos in order (the first is
  the cover on the Collections page). A photo is in at most one collection.
- `highlights`: the **Home page** photos and slideshow, in this order.
- `tags`: the tag library. `photo_tags` may only use names from it. Tags
  are private: used for search-engine keywords, not shown on the page.
- `locations`: one place per photo, at **town/island**, **region** (state)
  or **country** level only, from the GeoNames list built into the editor
  (`gid` is the GeoNames id). Never coordinates.
- **Show on site** (`hidden` / `published` / `drafts_from`): photos added to
  the album from `drafts_from` until 2026-11-26 started hidden until
  released (`published`). Since then the site is **site-first**: new photos
  show right away. `hidden` pulls a photo back. Hidden photos are left off
  the site but are not private (their image files still exist).
- **Automatic places:** photos whose file has GPS get their nearest town or
  island automatically (worked out by the site's build; the coordinates are
  never stored). A place in `locations` always wins; `no_place` lists photos
  whose location was removed, so they get no automatic place either.
- **On Work page** (`on_work` / `off_work`): photos added after 2026-11-26
  are off the Work page's full list until ticked (`on_work`); `off_work`
  takes a photo off. Photos off Work still show in their collection, as
  highlights and on their share pages.

The site reads this file live (changes show within ~5 minutes) and every
build (hourly when GitHub has capacity, or **Publish now** in the editor)
bakes it in. Both treat it as untrusted: titles are cleaned and title-cased,
unknown photo ids are ignored, and nothing is rendered as HTML.
