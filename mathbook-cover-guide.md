# Mathbook covers

The shared class is installed at `/home/archie/texmf/tex/latex/misc/mathbook.cls`.
There is one cover layout: an ivory page, serif title, italic subtitle, copper accent,
optional artwork, and a small footer. Cover text is typeset by LaTeX; artwork remains
editable in SVG and is exported to vector PDF with Inkscape.

```latex
\documentclass{mathbook}

\coversetup{
  title = {Lie Groups,\\Lie Algebras},
  subtitle = {and Representations},
  image = {cover-art.pdf},
  author = {Archie}
}

\begin{document}
\makecover
\frontmatter
\tableofcontents
\mainmatter
% Chapters...
\end{document}
```

Only the title is required. Omit `image`, `subtitle`, or `author` to leave them out.
The date is hidden unless explicitly supplied with `date = {\today}` or another
value in `\coversetup`; the ordinary `\date` command does not control this cover.
The title supports deliberate line breaks with `\\`.

## Optional settings

| Key | Default | Purpose |
| --- | --- | --- |
| `series` | `MATHEMATICS / STUDY NOTES` | Small header; set to `{}` to hide |
| `background` | `mathbookcoverpaper` | Any defined xcolor color or expression |
| `ink` | `mathbookcoverink` | Title and rule color |
| `accent` | `mathbookcoveraccent` | Short accent rule color |
| `title-size` | `42pt` | Title font size |
| `title-leading` | `48pt` | Title line spacing |
| `overlay` | `0` | White overlay on the artwork only, from 0 to 1 |
| `date` | empty | Optional footer at the right |

For an unusually long title, reduce both `title-size` and `title-leading`.
Artwork is centered in the lower part of the page, preserves its aspect ratio,
and fits within 86% of the page width and 40% of its height. Export artwork with a
tight page boundary and no embedded cover title. Transparent backgrounds work best.

```bash
inkscape cover-art.svg --export-type=pdf --export-filename=cover-art.pdf
latexmk -pdf main.tex
```

The old `\covertitletext{...}` and `\coverimage{...}` commands still set the title
and artwork. They now use this same layout; there are no legacy or full-page modes.
Images in existing notes are treated as artwork rather than stretched backgrounds.

The Lie algebra notes use `LieAlgebra/cover-art.svg` and its PDF export.
The earlier complete `cover.svg` and `cover.pdf` are retained as editable design
artifacts, but are not used by the shared layout.

## Shared interior style

The installed class now also uses matching Palatino-style text and mathematics,
navy chapter headings, copper theorem accents, quiet running headers, and
smaller captions. Existing environment commands and numbering are preserved.

The class directory `/home/archie/texmf/tex/latex/misc` is now a Git repository.
Its first commit saves the original classes. The dated pre-redesign backup is
`mathbook.cls.before-interior-2026-11-17.bak` in that same directory.
The README there includes a restore command and a reusable sample document.

A rendered sample is available as `mathbook-style-preview.pdf` beside this guide.
