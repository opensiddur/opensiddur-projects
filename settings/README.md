# Printed books

Each file here is an exporter settings file for one printed book. Every opensiddur-ai release
builds all of them into PDFs and attaches them to the release.

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

- The release asset is `<book>-<variant>-<tag>.pdf`, e.g. `humash-annual-v0.5.0.pdf`. Names are
  lowercase with `_` between words.

The rest of the format is documented in opensiddur-ai: `opensiddur/exporter/README.md` and
`doc/typography.md`.

Pull requests are checked (`python -m opensiddur.exporter.books --check`): each file must be
in place, parse, match the settings schema, name a project and file that exist, and have an
installed font for every font chain it is typeset with. To build the books locally from an
opensiddur-ai checkout:

```bash
P=<this repository>/project
uv run python -m opensiddur.exporter.refdb --project-directory "$P"
uv run python -m opensiddur.exporter.books --project-directory "$P"            # all books
uv run python -m opensiddur.exporter.books --project-directory "$P" humash     # one book
```
