# AlexTowbinPhotographyData

Photo titles and order for
[Alex Towbin Photography](https://towbinaj.github.io/AlexTowbinPhotography/).
The site's code lives in
[towbinaj/AlexTowbinPhotography](https://github.com/towbinaj/AlexTowbinPhotography).

This repo is kept separate on purpose: the owner's editing key only has
access to this repo, so it can never change the site's code, its build, or
its secrets. Everything here is public (titles are shown on the site anyway).

## `curation.json`
You don't need to edit it by hand.

Written by the site's editor and the phone editor app (`/edit/`).

```json
{
  "titles":      { "<photo id>": "Title" },
  "order":       ["<photo id>", "..."],
  "collections": [{ "name": "Series", "photos": ["<photo id>", "..."] }],
  "highlights":  ["<photo id>", "..."]
}
```

- `titles`: optional per photo; untitled photos show the date.
- `order`: the main page order. Photos not listed yet come first.
- `collections`: named series, each with its photos in order. A photo is in
  at most one collection.
- `highlights`: photos featured on the main page.

The site reads this file live (changes show within ~5 minutes) and the
nightly build bakes it in. Both treat it as untrusted: titles are cleaned and
title-cased, unknown photo ids are ignored, and nothing is rendered as HTML.
