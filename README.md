# SignPDF
Incorporate an electronic signature into a PDF document using LaTeX.

## Problem Statement

Today's PDF readers and editors make it simple to electronically sign PDF documents. You can create and apply your signature in three primary ways: by typing your name in a cursive style which is then transformed into a signature, by drawing the signature using a mouse, trackpad, or stylus on a touchscreen device, or by inserting an image of your handwritten signature. The typing and drawing methods are effective, ensuring that your signature appears clear and can be scaled significantly without any loss of quality. However, using an image of your signature often results in a jagged, blurry, or smudged appearance when the PDF is zoomed in beyond a certain level. Converting scanned signatures from raster formats like JPGs or PNGs to vector formats such as EPS or PDF does not effectively address this issue.

The objective of this project is to seamlessly integrate an existing electronic handwritten signature into a PDF document while preserving its high quality.

## Approach

We solve this issue by employing LaTeX to add a signature to a PDF. Specifically, we utilize the `pdfoverlay` package to import the PDF you want to sign, and then overlay a signature image on specified pages. The `textpos` package is used to accurately place the signature at desired locations on the page, and the `fgruler` package assists in determining the precise coordinates for the signature placement.

## Working Example

Below is a practical example of how to sign a PDF document using LaTeX. The signed PDF file can be accessed [here](signpdf.pdf). For more details on the implementation, please see [signpdf.tex](signpdf.tex).

```tex
\documentclass[a4paper]{article}

\usepackage{pdfoverlay}
\usepackage[absolute,overlay]{textpos}
\setlength{\TPHorizModule}{1cm}
\setlength{\TPVertModule}{\TPHorizModule}
\textblockorigin{0cm}{0cm}

\pagestyle{empty}

\begin{document}

\pdfoverlaySetPDF{example.pdf}

\begin{textblock}{3}[0.5,0.5](5,24)
\includegraphics[width=3cm]{signature/zhangsan.pdf}
\end{textblock}

\begin{textblock}{3}[0.5,0.5](15,24)
\today
\end{textblock}

\pdfoverlayIncludeToPage{2}

\begin{textblock}{3}[0.5,0.5](11.5,22.5)
\includegraphics[width=3cm]{signature/johnsmith.pdf}
\end{textblock}

\begin{textblock}{2}[0.5,0.5](11.5,24.5)
\includegraphics[width=2cm]{signature/lisi.pdf}
\end{textblock}

\pdfoverlayIncludeToLastPage

\begin{textblock}{3}[0.5,0.5](5,24)
\includegraphics[width=3cm]{signature/signature.pdf}
\end{textblock}

\end{document}
```

## How to Use

* Convert your handwritten signature into a vector-based file. Searching "convert a signature to a vector" online will provide step-by-step instructions on how to do this.
* Ensure you have a recent TeX installation. Install the following packages (later versions may also work):
  - `pdfoverlay` ([latest version](https://github.com/dcpurton/pdfoverlay/releases/latest) for TexLive 2020+, or [version 1.0](https://github.com/dcpurton/pdfoverlay/releases/tag/v1.0) for earlier TexLive versions)
  - `textpos`
  - `fgruler` (optional)

The main file to run is `signpdf.tex`, which includes several other files. For specific details, refer to the comments in the LaTeX sources.

Compile by running `signpdf.tex` through `pdfLaTeX` or `XeLaTeX`.

## Caveat
Links and other PDF annotations in the original PDF file will be lost during the inclusion process due to the nature of PDF handling ([1](https://tex.stackexchange.com/a/337927), [2](https://tex.stackexchange.com/a/26139)). To preserve existing PDF annotations, flatten the PDF first using available workarounds ([3](https://tex.stackexchange.com/a/124361), [4](https://documentation.its.umich.edu/node/1311), [5](https://tex.stackexchange.com/a/218818), [6](https://tex.stackexchange.com/a/443914)). Currently, no perfect solutions exist for preserving hyperlinks in included PDFs. Consider signing specific pages first and then reinserting them into your main PDF using PDF manipulation tools like pdftk, which can concatenate PDF files ([7](http://blog.bharatbhole.com/inserting-pages-from-an-external-pdf-document-within-a-latex-document/)).

## Alternative

For macOS users seeking a more straightforward solution, consider the [Tiny PDF Editor - PDF Signer](https://apps.apple.com/us/app/tiny-pdf-editor-pdf-signer/id445159317) app. This app allows you to add vector digital signatures to PDF documents while maintaining high quality. It is free to download, with a US$4.99 fee to remove the watermark. Please note that I have no affiliation with this app; it is recommended purely based on its functionality.


## License
`SignPDF` is distributed under the LaTeX Project Public License (version 1.3c).
