# HybridMASC

User manual and design notes for HybridMASC, a bottom-up DLP resin printer with a 405 nm laser that writes silver into each cured layer.

**Read it online: https://xmiao8.github.io/HybridMASC/**

- `docs/manual/`: the user manual, one page per topic, with screenshots in `docs/manual/img/`
- `docs/design-and-implementation.md`: how the hardware, firmware and control software are built
- `mkdocs.yml`: site settings and navigation

The site is built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) and published by GitHub Actions (`.github/workflows/docs.yml`) on every push to `main`.

To preview it locally:

```
pip install -r requirements-docs.txt
mkdocs serve
```

The printer's source code is not in this repository yet.
