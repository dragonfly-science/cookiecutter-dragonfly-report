KNITR = $(addsuffix .tex, $(basename $(shell find knitr -iname "*.Rnw")))
KNITR_BASE = $(addsuffix .tex, $(basename $(wildcard *.rnw)))
OUTPUT_DIR={{cookiecutter.build_directory}}
TARGET={{cookiecutter.report_slug}}.pdf


#Actually setting a build output target  does not work with the old latexmk
LATEXMK_VERSION=$(strip $(patsubst Version,,$(shell latexmk -v | grep -oi "version.*")))
LATEXMK_OPTIONS=-xelatex -output-directory=$(OUTPUT_DIR)

all: $(TARGET) 

$(TARGET): $(OUTPUT_DIR)/$(TARGET)
	cp $(OUTPUT_DIR)/$(TARGET) $(TARGET)

#We need to fall back to manually calling the programs if using old latexmk
$(OUTPUT_DIR)/$(TARGET): $(TARGET:%.pdf=%.tex) $(OUTPUT_DIR) $(KNITR) $(KNITR_BASE)
ifeq ($(LATEXMK_VERSION),4.24)
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR) $<
	biber --output_directory=$(OUTPUT_DIR) $(<:%.tex=%)
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR) $<
	TEXINPUTS=.///: xelatex -output-directory=$(OUTPUT_DIR)  $<
else
	 latexmk $(LATEXMK_OPTIONS) $<
endif

$(OUTPUT_DIR):
	mkdir -p $(OUTPUT_DIR)
	
#Sweave and knitr have different mechanisms for dealing with R errors. 
#In most cases as Sweave run will fail and return an error if there is an
#error generated in the underlying R code. This error is propogated out and 
#stops the makefile and therefore the entire complation process. In contrast
#knitr will handle most errors and not propogate them out where possible. This 
#means that a much larger number of programs will successfully compile, but will
#have error text in the output pdf, rather than an error message in the compilation
#process. 
knitr/%.tex: knitr/%.{{cookiecutter.file_extension}}
	(cd $(@D); Rscript -e "library(knitr);opts_chunk\$$set(warning=F, message = FALSE,echo=F,results='asis',fig.lp='fig:',fig.path='images/'); knit('$(<F)')")

%.tex: %.{{cookiecutter.file_extension}} $(KNITR)
	Rscript -e "library(knitr); knit('$(<F)',output='$(OUTPUT_DIR)/$(@F)')"

#Sometimes we want to blow away all of the R code output as well as just the latex stuff
superclean: clean
	find knitr -iname "*.tex" -delete
	find knitr -iname "*.pdf" -delete
	find knitr -iname "*.png" -delete
	find knitr -iname "images" -delete

clean:
	rm -rf  $(OUTPUT_DIR) $(TARGET) 

