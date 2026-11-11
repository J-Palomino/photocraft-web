# photocraft-web (Odoo build)

Builds the [storytold/photocraft](https://github.com/storytold/photocraft) web bundle that the Odoo module
`mint_craft_office` (J-Palomino/odoo-custom-modules) serves, with one patch:

- **`patches/v0.16.0/js-api.patch`**: adds `window.photocraft`, the desktop control server's JSON methods for the
  page (`request`, `execute`, `commands`, `inspect`, `openFile`, `captureDownloads`, `files`, `readFile`), ported
  from VectorCraft's `apps/vectorcraft-web/src/api.rs`. PhotoCraft 0.16.0's web build has the control
  dispatcher compiled in but no way for the page to reach it. The Craft Office AI assistant drives PhotoCraft through it.

Pins live in `odoo-build.env`; pushing a change to it (or to `patches/**`) on `odoo-build` runs
`.github/workflows/odoo-build.yml`, which checks out the upstream tag, applies the patch, builds with upstream's
own `packaging/web/package.sh`, and publishes a release with `photocraft-web-<version>.zip` + `.sha256`.

To upgrade: bump `UPSTREAM_TAG`, `CRAFT_FONTS_REF` (from upstream's `.github/workflows/release.yml` at that tag) and
`RELEASE_TAG`; rebase the patch if it no longer applies; push; then update the pin in `mint_craft_office/bundles.txt`.

PhotoCraft is MIT OR Apache-2.0 (see the LICENSE and NOTICE files inside the zip). Same pattern as
[J-Palomino/vectorcraft-web](https://github.com/J-Palomino/vectorcraft-web).
