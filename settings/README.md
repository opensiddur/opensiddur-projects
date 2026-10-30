# Books

Each file here is an exporter settings file for one book. On the first of each month this
repository is tagged with the date, `vYYYYMMDD`, and every book is built as an electronic book
(HTML) and a printed one (PDF), with the latest opensiddur-processor release, and attached to that
release (`.github/workflows/release.yml`). A month with nothing new, no commits here and no new
opensiddur-processor release, makes no release.

```
settings/
  <book>/
    <variant>.yaml
```

- One subdirectory per book. The variants in it are different settings for the same book: an
  annual and a triennial humash, a Haggadah with and without the translation. A file anywhere
  else is an error.
- Each file names the root file it compiles with `book:`, and says what it makes and how it
  differs from the other variants with `description:`:

  ```yaml
  description: >
    The whole humash for the annual cycle, Hebrew facing English.
  book:
    project: humash        # a directory under project/
    file_name: index.xml   # relative to that project
    title: Humash (annual cycle)   # optional
  priority:
    ...
  ```

- Each file says which opensiddur-processor versions build it, as PEP 440 writes them:
  ```yaml
  requires_processor: ">=0.7.0"
  ```
  An older processor refuses the settings instead of building a broken book, and the books
  release, built with the latest processor release, leaves the book out until a release meets
  it. Raise it when the book starts using a setting or a fix that is not yet released. Main
  between releases is the development of the next release, and meets that release's
  requirement.
- A book is built in both forms unless its `formats:` says otherwise. A book read only on a
  device lists just the electronic one:

  ```yaml
  formats: [html]   # html, pdf, or both (the default)
  ```

- The release assets are `<book>-<variant>-<tag>.html` and `.pdf`, e.g.
  `humash-annual-v20261101.pdf`. Names are lowercase with `_` between words.

The rest of the format is documented in opensiddur-processor: `opensiddur/exporter/README.md` and
`doc/typography.md`.

Pull requests are checked (`python -m opensiddur.exporter.books --check`): each file must be
in place, parse, match the settings schema (with `book:` and `requires_processor:`), name a project and file that exist, and have an
installed font for every font chain it is typeset with. To build the books locally from an
opensiddur-processor checkout:

```bash
P=<this repository>/project
uv run python -m opensiddur.exporter.refdb --project-directory "$P"
uv run python -m opensiddur.exporter.books --project-directory "$P"            # all books
uv run python -m opensiddur.exporter.books --project-directory "$P" humash     # one book
```

To make a books release now, or to rebuild one (see opensiddur-processor's `RELEASE_PROCEDURE.md`):

```bash
gh workflow run release.yml -R opensiddur/opensiddur-projects                     # if anything is new
gh workflow run release.yml -R opensiddur/opensiddur-projects -f force=true       # regardless
gh workflow run release.yml -R opensiddur/opensiddur-projects -f tag=v20261101    # rebuild it
gh workflow run release.yml -R opensiddur/opensiddur-projects -f tag=v20261101 -f book=humash/annual
```
