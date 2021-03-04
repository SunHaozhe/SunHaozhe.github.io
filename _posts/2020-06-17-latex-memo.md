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

# Line spacing and margins 

Change line spacing for the whole document:

```latex
\renewcommand{\baselinestretch}{1.0}
```

Change margins:

```latex
\usepackage[left=0.75in,top=0.6in,right=0.75in,bottom=0.6in]{geometry}
```

[Microsoft engineers](http://www.metricationmatters.com/docs/PageBordersInchesORmillimetres.pdf) set the defaults for an A4 page (210 mm x 297 mm) at 1 inch (25.4 mm) top and bottom, with 1 and a 1/4 inch (31.7 mm) on each side. 

# Citations

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

# 1-column abstract in 2-column document


[https://www.texfaq.org/FAQ-onecolabs](https://www.texfaq.org/FAQ-onecolabs)

```latex
\documentclass[twocolumn]{article}


...


\begin{document}

% 1-column abstract in 2-column document 
\twocolumn[
  \begin{@twocolumnfalse}
    \maketitle
    \begin{abstract}
    Blablabla
    \end{abstract}
  \end{@twocolumnfalse}
]


%\section{Introduction}

\end{document}
```

Be careful when using long equations that would span across two columns. 

# Positioning of Figures

![figure_position_specifiers](/assets/images/blog/figure_position_specifiers.png)


In order to placing a figure spanning the two columns of a `twocolumn` document, we need to use the starred version of the `{figure*}` environment to enable the figure occupy the two columns. Example:

```latex
\begin{figure*}[h]
    \centering
    \includegraphics[width=0.8\linewidth]{Figures/xxx.png}
    \caption{}
    \label{fig:xxx}
\end{figure*}
```

`{figure*}` should not be used together with `[H]`. 


# Table

In order to make a table with 3 rows and 4 columns:

```latex
\usepackage{adjustbox}


\begin{table}[h]
	\centering
	\begin{adjustbox}{}
	\begin{tabular}{|c|c|c|c|}
	\hline
     &  &  &  \\
    \hline
     &  &  &  \\
    \hline
     &  &  &  \\
    \hline
    \end{tabular}
	\end{adjustbox}
	\caption{}
	\label{tab:}
\end{table}
```

If the above table has too many columns that do not correctly fit the page width, one can use `\begin{adjustbox}{width=\linewidth}`

The signification of the parameters of `\begin{tabular}`:

* `l`	left-justified column
* `c`	centered column
* `r`	right-justified column
* `|`	vertical line
* `||`	double vertical line
* `|||` triple vertical line


Once in the `tabular` environment, `&` is column separator, `\\` is start new row, `\hline` is horizontal line.


`\checkmark` and `$\times$` can be used for binary information. 

```latex
\usepackage{makecell}

% bold table headers, maybe optional  
\renewcommand\theadfont{\bf} 
```

`\makecell{A \\B \\C}` can be used to break lines in table cells. `\thead{A \\B \\C}` additionally makes the text bold. 








