# PHDUIO – Monograph
This LaTeX template is used for article based doctoral theses at the University of Oslo.
For article based theses,
see the template [PHDUIO – Article based thesis](https://github.com/martinhelso/phduio-article-based).

Available on [Overleaf](https://www.overleaf.com/latex/templates/phduio-monograph/wvstjttnywvr).

The main features of the template are:
* Theses at the University of Oslo are printed in the book format 17 x 24 cm.
This is about 81% of an A4 paper.
In `phduio`,
you work directly in the 17 x 24 cm format,
so you do not have to worry about whether the font and figures will be legible after being shrunk for printing.
* It defines a custom title page.

[![Example document](https://i.imgur.com/dGvvQkE.png)](https://www.duo.uio.no/bitstream/handle/10852/81172/PhD-Helsø-2020_rev.pdf)

## Contents
* [Documentation](#documentation)
  * [Title page](#title-page)
    * [Colophon](#colophon)
  * [Screen mode](#screen-mode)
  * [Miscellaneous](#miscellaneous)
* [FAQ](#faq)
* [Contact information](#contact-information)

## Documentation
This text is about the specifics of the template.  
The more general [guide to large documents](https://github.com/martinhelso/Introduction-to-LaTeX/blob/master/large-documents.md)
is also considered part of the documentation.

At the core,
`phduio` consists of `memoir`,
so in addition to what is mentioned here,
you have all the functionality of `memoir`.

### Title page
A custom title page is printed when `\uiotitle` is invoked.
Just like `\maketitle`,
it collects data from `\author` and `\title`.
In addition,
you can add a subtitle using `\subtitle`.
Also,
you must specify your affiliation at the university with `\department` and `\faculty` before calling `\uiotitle`.

Optionally,
other affiliations can be added with `\affiliation`.
Use `\and` or `\AND` to separate the affiliations.
The use of `\and` is intended for separating subdepartments of a single institution:
```latex
\affiliation
{
    Center for Biomedical Computing
    \and
    Simula Research Laboratory
}
```
Whereas `\AND` is intended for separating two different institutions:
```latex
\affiliation
{
    Simula Research Laboratory
    \AND
    Oslo University Hospital
}
```

#### Colophon
If the class option `[colophon]` is used,
`\uiotitle` will also print a colophon page with copyright and printing information.
The colophon collects information from the commands `\author`, `\faculty`, `\dissertationseries` and `\ISSN`
or – if you belong to the Faculty of Medicine – `\ISBN`.

If needed,
the credits for cover design and printing can be changed with `\cover` and `\printinghouse`.

You can request the dissertation series number and ISSN/ISBN
by sending an e-mail to the University Print Centre at [repro@uio.no](mailto:repro@uio.no)
shortly before submitting the thesis.
They are also able to edit in the correct numbers directly into the `.pdf` for you.

### Screen mode
By default,
`phduio` is set up for printing.
If you want a version of the thesis that is more suitable for viewing on a screen,
pass the option `[screen]` to the document class.
This will colour clickable links and make the inner and outer margins equal.

### Miscellaneous
The university's official colours are available under the names `uiored`, `uiogrey` and `uiolink`.
The colon from the university logo can be accessed with `\uiocolon`.

## FAQ
1. **How do I remove labels from the margin?**  
  Use the document class option [`[final]`](https://github.com/martinhelso/Introduction-to-LaTeX/blob/master/large-documents.md#draft-and-final-options):
  ```latex
  \documentclass[final]{phduio}
  ```

2. **How do I compile the bibliography?**  
The file [`phdstyle.sty`](phdstyle.sty) imports the package `biblatex` with the option `[backend = biber]`.
To compile the bibliography,
run `biber` on `main.bcf` or change to `[backend = bibtex]` and run `bibtex`.

3. **How do I change the reference and citation style?**  
The file [`phdstyle.sty`](phdstyle.sty) imports the package `biblatex` with the option `[style = alphabetic]`.
Replace `alphabetic` with another [style name](https://www.overleaf.com/learn/latex/Biblatex_citation_styles).

4. **Why do I get an error saying `giveninits` is undefined?**  
The file [`phdstyle.sty`](phdstyle.sty) imports the package `biblatex` with the option `[giveninits = true]`.
The error indicates that you have installed an old version of `biblatex`.
The best solution is to update your TeX distribution to the latest version.
Alternatively, change `giveninits` to `firstinits`.

5. **Why is `\citet` and `\citep` not working?**  
These commands are not defined in `biblatex`;
their analogues are called `\cite` and `\parencite`,
respectively.
If you use an author-year citation style,
you can define `\citet` and `\citep` to issue their counterparts by adding the following to the preamble:
```latex
\let\citet\cite
\let\citep\parencite
```
If you are using a numerical citation style,
`\citet`behaves differently than `\cite`.
In this case,
add instead the following to the preamble:
```latex
\RequirePackage{xparse}
\NewDocumentCommand{\citet}{oom}
{
    \citeauthor{#3}~%
    \IfValueTF{#1}
    {%
        \IfValueTF{#2}
        {\cite[#1][#2]{#3}}
        {\cite[#1]{#3}}
    }
    {\cite{#3}}
}
\let\citep\parencite
```

6. **How can I use *fragile* macros inside `\title` or `\author`?**  
Add `\protect` before the fragile macro.

7. **Why are some chapters preceded by a blank page?**  
By the formal [layout requirements](https://www.mn.uio.no/english/research/phd/thesis-adjudication/layout/),
chapters should start on a recto page.
A blank page is inserted if this does not occur naturally.

## Contact information
If you need further assistance with the template,
you may send an e-mail to [latexguru@ub.uio.no](mailto:latexguru@ub.uio.no).
