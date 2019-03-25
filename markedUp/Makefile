.PHONY:  all ac clean pdf diff dev view 

LATEXMK := latexmk

TARGETFILE := oro-cs-seminar.diff

TEXFILES := $(shell find . -name "*.tex")

ROOT_TEXFILE := $(patsubst %.pdf,%.tex,$(TARGETFILE)) # Assume we are looking for a tex file with the same name as TARGETFILE

# Create a PDF, enable synctex, allow pdflatex to spawn more processes, run noninteractively
LMKFLAGS := -pdf -pdflatex="pdflatex" -use-make

UNAME_S := $(shell uname -s)

all: diff pdf

ac: all clean

pdf: $(TARGETFILE)

diff:
	latexdiff ../oro-cs-seminar.tex oro-cs-seminar.jorden.tex > $(TARGETFILE).tex  

# Monitor for changed tex files and rebuild the pdf
dev: $(TEXFILES)
	$(LATEXMK) $(LMKFLAGS) -pvc $(ROOT_TEXFILE)

$(TARGETFILE): $(TEXFILES)
	$(LATEXMK) $(LMKFLAGS) $(ROOT_TEXFILE)

clean:
	$(LATEXMK) -CA
	rm -f $(TARGETFILE).pdfsync
	rm -rf *~ *.tmp
	rm -f *.bbl *.blg *.aux *.end *.fls *.log *.out *.fdb_latexmk *.aux *.glo
	rm -f *.idx *.log *.toc *.ist *.acn *.acr *.alg *.bbl *.blg *.dvi *.glg
	rm -f *.gls *.ilg *.ind *.lof *.lot *.maf *.mtc *.mtc1 *.out *.synctex.gz *.tdo

view:
ifeq ($(UNAME_S),Darwin)
	open $(TARGETFILE).pdf
else
	xdg-open $(TARGETFILE).pdf &
endif

