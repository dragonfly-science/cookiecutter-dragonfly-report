OUTPUT_DIR={{cookiecutter.build_directory}}
TARGET={{cookiecutter.report_slug}}.pdf
KNITR = $(addsuffix .tex, $(basename $(shell find knitr -iname "*.Rnw")))
KNITR_BASE = $(addprefix $(OUTPUT_DIR)/, $(addsuffix .tex, $(basename $(wildcard *.rnw))))

all: $(TARGET) 

$(TARGET): $(OUTPUT_DIR)/$(TARGET)
	cp $(OUTPUT_DIR)/$(TARGET) $(TARGET)

#We need to fall back to manually calling the programs if using old latexmk
$(OUTPUT_DIR)/$(TARGET): $(TARGET:%.pdf=%.tex) $(OUTPUT_DIR) $(KNITR) $(KNITR_BASE)
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR) $<
	biber --output_directory=$(OUTPUT_DIR) $(<:%.tex=%)
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR) $<
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR)  $<

$(OUTPUT_DIR):
	mkdir -p $(OUTPUT_DIR)
	
knitr/%.tex: knitr/%.{{cookiecutter.file_extension}}
	(cd $(@D); Rscript --vanilla -e "library(knitr);opts_chunk\$$set(warning=F, message = FALSE,echo=F,results='asis',fig.lp='fig:',fig.path='images/'); knit('$(<F)')")

$(OUTPUT_DIR)/%.tex: %.{{cookiecutter.file_extension}} $(KNITR)
	Rscript --vanilla -e "library(knitr);opts_chunk\$$set(warning=F, message = FALSE,echo=F,results='asis',fig.lp='fig:',fig.path='images/'); knit('$(<F)',output='$(OUTPUT_DIR)/$(@F)')"

#Sometimes we want to blow away all of the R code output as well as just the latex stuff
superclean: clean
	find knitr -iname "*.tex" -delete
	find knitr -iname "*.pdf" -delete
	find knitr -iname "*.png" -delete
	find knitr -iname "images" -delete

clean:
	rm -rf  $(OUTPUT_DIR) $(TARGET) 

