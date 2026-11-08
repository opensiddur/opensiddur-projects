# Preview works

`preview-he` and `preview-en` are entirely synthetic CC0 fixtures for the hosted
builder. Their short names are intentional UI fixtures. No historical attribution
is implied by their invented people, bibliography, edition, or approval notice.

Every piece of visible text is the name of the typography style that sets it, so a
reader can see which setting changes what. The English work uses the names the
Builder shows (`heading1`, `title main`, `list label`, `highlight italic`); the
Hebrew work uses Hebrew translations of the same names, pointed so that line
spacing is exercised. Where a passage must be longer than the name, for example a
paragraph that has to wrap to show indentation, alignment and line spacing, the
name is repeated. Text follows the language of its element: the Hebrew alternative
title in the English work, for instance, is the Hebrew name.

Some styles name text the exporter generates rather than text in these files: the
translated heading (made from the two columns' different headings), verse and
chapter numbers, note marks, line numbers, the distribution and back-page notices,
and the section separator. Verse and chapter numbers stay numbers.

Each work has an independent title page and preface, unpaired passages, and an
external transclusion of a shared URN in `parallel.xml`. Both files share paragraph
and section boundaries so parallel columns, pairs and facing pages can be compared.

The fixture covers four heading levels, paragraph alignment/spacing, numbered and
unnumbered lists, poetry, every kind of highlight (italic, bold, small capitals,
superscript, large, small), inline instructions/editorial notes, stand-off
commentary, abbreviations and misprints (one form of each shows, chosen by the
`readings` settings), qere/ketiv, alternative readings, references, foreign
phrases in the other language, verse/chapter/parsha/aliyah/citation markers,
separators, and pointed Hebrew. Conditional examples cover minyan, Shabbat, and
the first day of Rosh Hodesh. Title-page/preface conditions expose the paratext
settings. Credits, CC0 licensing, and an invented bibliography exercise the
generated colophon and source list.

The compiler generates page numbers, running heads, line numbers, contents and
layout from the reader's settings. Not every calendar/custom choice changes every
passage: these compact works exercise representative conditions, not an entire
prayerbook's inventory of liturgical alternatives.

Hosted previews substitute these two sources for text, translation and annotation
priorities while preserving the other settings. Full builds use the reader's
selected project and sources. Both preview works can also be built directly using
the example YAML files under `settings/`.
