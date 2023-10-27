Fixing Overleaf Wordcount: https://www.overleaf.com/learn/how-to/Is_there_a_way_to_run_a_word_count_that_doesn%27t_include_LaTeX_commands%3F

Get the code for the fixing the front errors (breach)



## Notes on survey formatting
```\noindent \textit{The section headings were not visible to participants. Answer choices are shown in bullets below each question. Answer responses with the text ``Other'' included a free response box for participants to explain their answer.}```

 ```\noindent \textbf{Q1:}```

```
\begin{itemize}[noitemsep,topsep=0pt]
    \item Yes
    \item No
    \item Don't know
\end{itemize}
```

```\textit{(free response field)}```

```\noindent \textit{Question was only shown if participant selected ``No'' or ``Don't know'' in response to Q1}```

```\textit{(participants could select multiple options)}```

## Tables

### Multiple Rows in a Table Cell
* Nested Tabular
* Short stack
* p column style with \newline


### Multicol/row

```
\usepackage{multirow}
\multirow{ 2}{*}{Text}
```

### Random Symbols
*Quotations* ``` \`\`quote'' ```  or ``` \`quote' ``` use grave \` for left quote and ' for right quote

*e.g.* ``` e\,g\,. ```

~ is just a space that won't allow a line break. Use in situations like ```5~cats``` ```text~\cite{citation}``` or ```Section~\ref{sec:}


### New commands
todo

### Citations and Refs
todo


### Useful Packages
\usepackage{balance} % Balance references
\usepackage{xspace} % Spacing
\usepackage{hyperref} % Hyperlinks
\usepackage{cite} % Citations
\usepackage{array} % Pretty tables
\usepackage{verbatim} % block comments

