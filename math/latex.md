|||||
|--- |--- |--- |--- |
|\documentclass|[ 12pt, twocolumn ]|{article}|Enviroment|
|\begin||[!]=Float [t]=top||
|\begin|Itemize||•Items with \item … \tag{*}|
|\begin|Enumerate||1.\item|
|\begin|Equation||By default is Centered|
|\begin|Verbatim||Ignore all commands|
|\begin|Align|&|Aligning together - & under each other  *need amsmath SAMPLE:  \begin{align*} X&=1 &Y=2|
|\begin|Gather*||For star(*) need {amsmath} (NO NEED $$)|
|\begin|Table|||
||Eqnarray*||For star(*) need {amsmath} (NO NEED $$)|
|\begin|Quotation||Text Mode|
|\begin|Flushleft||All Align To left|
|\begin|Center||Make it center|
|\begin|Tabular|{|r|l|}  for Aligning Columns|& for sectioning and \\ for next line \hline  for bordering|
|\begin|Array|{rll}|Sample : \left(\begin{array} a&b\\c&d\end{array}\right)|
|\begin|pmatrix||Making body is like sample in array (previous)|
|\begin|Split|Use & for aligning|Multiline|
|\begin|Figure [h]||\begin{figure} \includegraphics{Images/capture} \caption{Info about Pic}|
|\begin{displaymath}\xymatrix||||
|\label{Figure}||||
|\quad   \qquad||||
|\lr||{TEX}|TEX Left to right|
|\LaTeX2e|||Micro|
|\usepackage||{ Xepersian Amsmath Amssymb Amsthm Fancyhdr setspace [all]{xy} geometry }|Last Package|
|$\pi$|||Math|
|\settextfont|[Scale=1]|{Font}||
|\setdigitfont|[Scale=1]|{Font}||
|\vspace \hspace||||
|\[ Sin\] OR $$ Sin $$|||Math + Center Alignment|
|\( Sin \)|||Math + Left Alignment|
|\author \title||{Shahriar}|Author of Article  ** Inside preamble|
|\maketitle & \makeindex|||** Inside Body|
|\maketableofcontent|||Content Index ** Inside Body|
|\section||{1st section}||
|$\cdots$ $\ldots$||||
|\mathbb||{R}|Real Numbers |R, NEED {amssymb}|
|\caption||{TableNameText}|Table Name with Table Number|
|$\it graphicx$||||
|\includegraphics|[width=0.15\textwidth]|{example-image-1x1}|IMAGE ** \usepackage{graphicx}|
|\label||||
|\tableofcontents|||FEHREST|
|\printindex|||Printing index - NAMAYE|
|\index|||For linking to Index|
|\include||{file}||
|\chapter|||•FEHREST|
|\opening \closing \signature \address|||*Need Letter Document Type *Inside \begin{letter}|
|\pagestyle{fancy} \fancyhf{} \pagestyle{headings} \pagestyle{empty}|||*need fancyhdr package PAGE HEADER via Chapter Name|
|\pagenumbering{arabic}||||
|\addcontentsline{}||||
|\textbf{}|\textit{}|\textrm{}|\texttt|
|\ $ % ^ & _  # { }|Need \$|*\backslash|\\  == \n|
|\LTRfootnote{ … note}|\RTLfootnote{…note}|Foot print||
|\frac{a}{b}|||a\b|
|\infty|||Infinity|
|~||\sim  for ~ character|Blank Space|
|\lim_{0 \to 2}|||LIMIT|
|\binom{n}{k}||||
|\cdots (center)|\ldots (Horizontal)     \vdots (vertical)|\ddots  (diagonal)|…   (3 dots)|
|\prod_{i=1}^{n}  I \sum_{}^{}||||
|$\begin{bmatrix}|||$\begin{bmatrix} A&b&c\\d&e&f \end{bmatrix}$|
|\right|_{x=0}||||
|||||
