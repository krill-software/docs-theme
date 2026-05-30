# krill docs-theme

Shared Jekyll remote theme for the per-app docs landing pages at
`krill-software.github.io/<slug>/`. Each app's `docs/index.html`
declares its content in YAML front matter; this theme renders the
same rich layout (nav / hero / features / principles / install /
footer) across every app.

## Consumer setup (per app)

`docs/_config.yml`:

```yaml
remote_theme: krill-software/docs-theme@v1
plugins:
  - jekyll-remote-theme

title: Text Editor          # display name, used in <title>, hero, asset filenames
slug: text-editor           # repo + URL slug
brand: text-editor          # optional override for the "krill / X" nav line
version: 0.1.5              # latest released version
```

`docs/index.html`:

```yaml
---
layout: app
tagline: a calm plain-text editor for Linux
description: A quiet plain-text editor for Linux. Line numbers, fast launch, one file per window — for config tweaks, scratch notes, and reading logs.
eyebrow: A plain-text editor for Linux
heading: "Open it, <em>edit</em> it, save it."
lede: A quiet plain-text editor. Line numbers, fast launch, one file per window — for the config tweak, the scratch TODO, the log you just need to read.
features_heading: Just an editor. A good one.
features:
  - tag: CodeMirror 6
    title: A real editor surface
    blurb: Line numbers, soft wrap…
  # 5 more features
principles_heading: A quiet editor.
principles:
  - strong: Not a code editor.
    span: No syntax highlighting, no language modes.
  # 3 more principles
extension: ".txt"          # registered file extension, shown in install copy
example_file: notes.txt    # example filename shown in install commands
appimage_size: 78 MB        # optional, appears next to "Download AppImage"
---
<!-- Whatever goes here renders inside the .preview-frame in the hero.
     Each app draws its own bespoke mock here. -->
```

## URL conventions baked into the theme

- Download URLs: `https://github.com/krill-software/{{ slug }}/releases/download/v{{ version }}/{{ asset_prefix }}_{{ version }}_amd64.{AppImage,deb}`
- Asset prefix: `title | replace: " ", "."` (Tauri's bundler converts spaces
  in `productName` to dots, so "Text Editor" v0.1.5 → `Text.Editor_0.1.5_*`).

## Releasing a new version of the theme

Tag a SemVer tag (`v1`, `v1.1`, `v2`, …). Consumers pin to a tag via
`remote_theme: krill-software/docs-theme@v1`. Breaking changes bump
the major.

## License

MIT.
