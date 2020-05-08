# SignPDF
Add an electronic signature to a PDF document using LaTeX

## Problem Statement

You can easily get your PDF documents electronically signed with all kinds of PDF readers and editors that are available today. To sign a PDF document, you can create and use your signature in one of three ways: type your name in cursive format and have it converted to a signature, draw the signature using your mouse, trackpad, or a stylus if you're using a touchscreen device, or insert an image of your handwritten signature. Type and draw work perfectly, your signature will be clearly displayed and you can enlarge the signed PDFs exponentially without pixelation or distortion. Unfortunately, if you use an image as signature, your signature in a singed PDF will look jagged, blurry or dirty when magnified more than 10 or so times. Simply converting scanned signature from raster images like JPGs and PNGs to scalable vector graphics like EPS and PDF files doesn't help solve the problem. 

The goal of this work is to easily add an existing electronic handwritten signature file to a PDF document while maintaining high quality.

## Approach

We address this problem by using LaTeX to sign a PDF document. Specifically, we use `pdfoverlay` package to import the PDF file you wish to sign, then overlay signature image on specified pages. We use `textpos` package to facilitate placement of signature at desired positions on the page and use `fgruler` package to help you work out the coordinates where you want to insert a signature.

## Working Example

A working example of signing a PDF document with LaTeX is given below. Signed PDF file can be found [here](signpdf.pdf). Please refer to [signpdf.tex](signpdf.tex) for more details on how it works.

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

## How to use

* You'll need to create a vector-based version of your signature file. Simply google, "convert a signature to a vector" and you'll get step by step instructions on how to vectorize your own signature.

* You'll need to have a reasonably recent TeX installation. The following packages should be installed (newer versions should also work):
  - `pdfoverlay` (version 1.1 for TexLive 2020, or version 1.0 for earlier TexLive versions)
  - `textpos`
  - `fgruler` (optional)

The main file is `signpdf.tex`, from which a number of other files are included. Take a look at the comments in the LaTeX sources for some more specific pointers.

To compile, simply run `signpdf.tex` through `XeLaTeX`.

## License
`SignPDF` is licensed under the LaTeX Project Public License (version 1.3c).
