all: {{cookiecutter.report_slug}}.pdf 

KNITR = $(addsuffix .tex, $(basename $(wildcard knitr/*.Rnw)))
KNITRBASE = $(addsuffix .tex, $(basename $(wildcard *.Rnw)))

LATEXMK_VERSION=$(strip $(patsubst Version,,$(shell latexmk -v | grep -oi "version.*")))
ifeq ($(LATEXMK_VERSION),4.24)
	LATEXMK_OPTIONS=-pdflatex=xelatex -latex=xelatex -pdf
else
	LATEXMK_OPTIONS=-xelatex
endif

report.pdf: $(KNITR) $(KNITRBASE) {{cookiecutter.report_slug}}.tex 
	latexmk $(LATEXMK_OPTIONS) {{cookiecutter.report_slug}}.tex

knitr/%.tex: knitr/%.Rnw
	(cd knitr; Rscript -e "library('knitr'); knit('$(<F)')")

%.tex: %.Rnw
	 Rscript -e "library('knitr'); knit('$(<F)')"

clean:
	rm -f  *.pdf *.aux *.log *.out *.backup *.glo *.idx \
	*.fdb_latexmk *.fls *-self.bib *.toc *.snm *.nav \
	*.ilg *-blx.bib *.run.xml *.bbl *.ind *.blg *.bcf

					                                                                  

