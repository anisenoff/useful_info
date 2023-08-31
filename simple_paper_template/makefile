.SUFFIXES: .dvi .ps

PAPER = paper
LATEX = latex
PDFLATEX = pdflatex -file-line-error -interaction=nonstopmode
PDFLATEX = pdflatex -file-line-error 
TEXFILES = *.tex
BIBFILE = misc/*.bib
OTHERFILE := $(wildcard sections/*.tex)
MISCFILE := $(wildcard misc/*.tex)

default: $(PAPER).pdf

$(PAPER).dvi: $(TEXFILES) $(BIBFILE) $(OTHERFILE) makefile
	$(LATEX) $(PAPER)
	bibtex $(PAPER)
	$(LATEX) $(PAPER)
	$(LATEX) $(PAPER)

$(PAPER).pdf: $(TEXFILES) $(BIBFILE) $(OTHERFILE) $(MISCFILE) makefile
	$(PDFLATEX) $(PAPER)
	bibtex $(PAPER)
	$(PDFLATEX) $(PAPER)
	$(PDFLATEX) $(PAPER)

$(PAPER).ps: $(PAPER).dvi
	dvips -P cmz -t letter -o $(PAPER).ps $(PAPER).dvi

final:	$(PAPER).pdf $(PAPER).ps
	cp $(PAPER).pdf final.pdf
	cp $(PAPER).ps final.ps

dvi: $(PAPER).dvi

ps: $(PAPER).ps

pdf: $(PAPER).pdf

preview: $(PAPER).dvi
	xdvi $(PAPER).dvi &

prevps: $(PAPER).ps
	ghostview $(PAPER).ps &

sendps: $(PAPER).ps
	sz $(PAPER).ps

sendpdf: $(PAPER).pdf
	sz $(PAPER).pdf

print: $(PAPER).ps
	lpr -Pmax $(PAPER).ps

clean:
	rm -fr *.ps *.dvi *.aux *.bbl *.blg *.log *.lof *.lot *.out *.toc $(PAPER).pdf *~ *.ent *.fdb_latexmk *.fls *.synctex.gz

wc:
	wc -w $(TEXFILES)

ispell:
	ispell -b -t $(TEXFILES)
