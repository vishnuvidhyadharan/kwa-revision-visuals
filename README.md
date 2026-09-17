# KWA revision visuals

Rendered revision infographics for the IQLearn exam-prep app, and the manifest
the app reads to find them.

**This repository is public on purpose, and holds derived artifacts only.**
Every PNG here is generated from revision notes that live in a separate private
repository, reviewed there before publishing. Nothing in this repo is a
question, an answer, an explanation, or a source note.

## Why it exists separately

The app cannot fetch images from the private bank repository, and a GitHub
token shipped inside an APK is recoverable with `unzip` — it would unlock the
question banks. So the images live here instead, reachable with no credential
at all, and the app downloads a section's pages the first time a learner opens
them.

## Never give this repo a remote into the bank repo

Not a submodule, not a second remote, not a subtree. The separation is the
security boundary. Publishing is one-way, by `tools/publish_visuals.py` in the
private repo.

## Layout

```
manifest.json          every bank and section, each page's size and sha256
<bank>/                e.g. cseb_deo/
  module-01-section-1-p1.png
```

## Tags are how corrections propagate

The app reads through jsDelivr, pinned to a tag:

```
https://cdn.jsdelivr.net/gh/<owner>/kwa-revision-visuals@v1/cseb_deo/module-01-section-1-p1.png
```

jsDelivr caches a tag immutably. A corrected page pushed under the **old** tag
never reaches a learner — bump the tag and the app's `VISUAL_STORE_TAG`
together.
