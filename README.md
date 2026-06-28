migrated to new location: https://codeberg.org/shackspace/shackspace-glossar

# shackspace-Glossar

Hier entsteht das shackspace-Glossar.
Es dient der Einführung neuer Mitglieder in die Abläufe und Gepflogenheiten des "shack" (Hackerspace in Stuttgart).

Jedes Stichwort erhält einen Kurztext, geschrieben in Markdown.
Daraus kann später ein komplettes Dokument als HTML, Wiki, PDF, EPUB oder was-auch-immer entstehen.

Manche Stichworte sind noch leer.
Regelmässige Besucher und Nutzer des shack sind herzlich eingeladen, beim weiteren Befüllen der Lücken mitzuhelfen.

## Vorschau

Wie das fertige Produkt mal aussehen könnte, ist anhand der verfügbaren Vorschau-Dokumente zu erahnen:

* [Vorschau-Dokumente: PDF, HTML, EPUB](https://github.com/shackspace/shackspace-glossar/tree/master/vorschau-beispiele)


## Aktueller Stand

Derzeitiger Stand des Projekts: ca. 19% fertig.

![*Das shackspace-Glossar ist zu ca. 19% fertig.*](images/glossary-progress-big.png "*Das shackspace-Glossar ist zu ca. 19% fertig.*")

## Pandoc-Installation

Die finalen Dokumente werden wir mit Hilfe von [`pandoc`](http://pandoc/org/) erzeugen.

Empfehlung: Installation von Pandoc über `cabal` (das Haskell-System zur distributions-unabhängigen Paket-Verwaltung).

```.bash
cabal update
cabal install cabal-install
export PATH=${HOME}/.cabal/bin:${PATH}
cabal install pandoc pandoc-citeproc pandoc-csv2table
```

Obige Vorgehensweise installiert die neuesten Versionen nach `${HOME}/.cabal/`.
Sie lässt die System-eigenen Pakete in Ruhe und fasst sie nicht an.

## Kommandos zum Erzeugen von EPUB, HTML, PDF und DokuWiki

Dies ist der erste "quick'n'dirty" Wurf. Später wird das ein Makefile erledigen.

```.bash
cd markdown

# EPUB3 erzeugen (noch ohne spezifisches CSS-Stylsheet) 
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar.epub          \
    --to=epub3                                                      \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
    --epub-chapter-level=1                                          \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd

# HTML5 erzeugen (noch ohne spezifisches CSS-Stylsheet) 
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar.html          \
    --to=html5                                                      \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
    --standalone                                                    \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd

# HTML5 erzeugen (mit "ein wenig" CSS) 
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar-mit-css.html  \
    --to=html5                                                      \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
    --standalone                                                    \
    --css=../resources/symlink.css                                  \
    --css=../resources/table.css                                    \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd

# DokuWiki erzeugen
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar.dokuwiki      \
    --to=dokuwiki                                                   \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd

# PDF erzeugen (A4, Porträt)
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar-A4.pdf        \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
    --chapters                                                      \
    --highlight-style=espresso                                      \
    --latex-engine=xelatex                                          \
    -H ../resources/setmainfont-sourcesansprolight.tex              \
    -V geometry:"margin=2cm, paperwidth=595pt, paperheight=842pt"   \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd

# PDF erzeugen (A5, Landscape)
pandoc                                                              \
    --output=../vorschau-beispiele/shackspace-glossar-A5q.pdf       \
    --toc                                                           \
    --base-header-level=1                                           \
    --indented-code-classes=bash                                    \
    --chapters                                                      \
    --highlight-style=espresso                                      \
    --latex-engine=xelatex                                          \
    -V geometry:"margin=1cm, paperwidth=595pt, paperheight=421pt"   \
    -V fontsize:10pt                                                \
    -V classoption=onecolumn                                        \
    -V linkcolor=blue                                               \
      00-titel-shack.md                                             \
      01-index.md                                                   \
      02-index-mit.md                                               \
      03-index-ohne.md                                              \
      *.mmd
```

