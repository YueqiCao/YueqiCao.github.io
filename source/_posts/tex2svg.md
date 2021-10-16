---
title: tex2svg
date: 2021-05-31 13:22:04
tags: 
- Latex
- Linux
categories: 
- CS
---

When I want to save a bunch of tex equations/symbols as svg files I find there is no efficient software to fulfill this goal. But I find the interesting [pipeline](https://xiaoxiang.io/5aab4864f26b75000111c679/) which is implemented on a Linux system.   The following is what I did on my CentOS7 server.

### Install Latex

Login in as **root**. Then install texlive using the following two commands

```linux
yum install texlive-latex
yum install texmaker
```

Check your pdflatex version using 

```linux
pdflatex --version
```
### Install pdfcrop

[pdfcrop](https://github.com/ho-tex/pdfcrop) is written by perl. First install perl on CentOS

```linux
yum install perl 
```
Check the perl version using

```linux
perl -v
```

Then download or clone the pdfcrop repository

```linux
git clone https://github.com/ho-tex/pdfcrop.git
```

cd to the directory where you can see the perl file. Run with a test pdf using 

```linux
perl pdfcrop.pl test.pdf
```

The output is named as 

```linux
test-crop.pdf
```

### Install poppler 

The original pipeline uses [pdf2svg](https://github.com/dawbarton/pdf2svg) which requires [poppler](https://poppler.freedesktop.org/) and [cairo](https://www.cairographics.org/) of high version. Installing dependencies on CentOS7 is a terrible struggle. The simplest way is to use pdftocairo which is contained in poppler-utils. 

```linux
yum install poppler-utils
```

Then run with a test pdf

```linux
pdftocairo test.pdf output.svg -svg
```

### Pack the pipeline

Write a bash script to pack all steps together.

```linux
#!/bin/bash

vim test.tex
pdflatex test.tex
perl pdfcrop.pl test.pdf
pdftocairo test-crop.pdf output.svg -svg
rm test.* test-crop.pdf
```



