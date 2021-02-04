---
layout: post
category: Misc   
title: Latex memo 
tagline: by SunHaozhe
tags: 
  - memo
mathjax: true
comments: true
published: true
---

Change line spacing for the whole document:

```latex
\renewcommand{\baselinestretch}{1.0}
```

Change margins:

```latex
\usepackage[left=0.75in,top=0.6in,right=0.75in,bottom=0.6in]{geometry}
```

[Microsoft engineers](http://www.metricationmatters.com/docs/PageBordersInchesORmillimetres.pdf) set the defaults for an A4 page (210 mm x 297 mm) at 1 inch (25.4 mm) top and bottom, with 1 and a 1/4 inch (31.7 mm) on each side. 

## Citations

Easily switch between (number) and (number+author) in the same document. Year is not shown. With `plainnat`, the number is different from `unsrt`, the ordering of citation numbers are not determined by the order of appearance. 

```latex
\usepackage[numbers]{natbib}
\bibliographystyle{plainnat}
% Hyperlinks bib references.
% This should be used together with \bibliographystyle{plainnat}
\usepackage{hyperref}  

\cite{} % citation with number
\citet{} % citation with number and author
```








