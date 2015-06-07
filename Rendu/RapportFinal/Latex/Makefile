# Makefile pour compiler le rapport si jamais Overleaf avait un problème

SHELL=/bin/bash
LATEX=pdflatex
BIBTEX=biber
#BIBTEX=true
GLOSS=makeglossaries
#GLOSS=true
.PHONY: todo all local all-pub pub all-del del quick xref xrefs test clean clear clobber


# All files the report depends on.
REPORT_CST_TEX+=main.tex
REPORT_CST_TEX+=body.tex
REPORT_CST_TEX+=titlepage.tex
# REPORT_CST_TEX+=$(shell find .              -name '*.tex' -print) 
# REPORT_CST_TEX+=$(shell find ../submod/glos -name '*.tex' -print) 
# REPORT_CST_BIB+=$(shell find ../submod/refs -name '*.bib' -print)

# Directory where to export report should be set in the shell.
export PDF_TARGET_DIR?=.

# PDF viewier
export PDF_VIEWER?=xdg-open

# Report comes in three flavors: local, published on a remote dir
# (without date), delivereed on a remote dir (with date).
DATE=$(shell date '+%Y-%m-%d-%Hh%M')
REPORT_LOC=main.pdf
REPORT_PUB=$(PDF_TARGET_DIR)/rapport.pdf
REPORT_DEL=$(basename $(REPORT_PUB))_v$(DATE).pdf

all local: $(REPORT_LOC)

all-pub: $(REPORT_PUB)

all-del: $(REPORT_DEL)

quick: $(REPORT_CST_TEX) $(REPORT_GEN_TEX) $(REPORT_CST_BIB)
	$(LATEX)  $(basename $(REPORT_LOC)).tex
	$(LATEX)  $(basename $(REPORT_LOC)).tex

$(REPORT_LOC) : $(REPORT_CST_TEX) $(REPORT_GEN_TEX) $(REPORT_CST_BIB)
	$(LATEX)  $(basename $(REPORT_LOC)).tex
	$(GLOSS)  $(basename $(REPORT_LOC))
	$(BIBTEX) $(basename $(REPORT_LOC))
	$(LATEX)  $(basename $(REPORT_LOC)).tex
	$(GLOSS)  $(basename $(REPORT_LOC))
	$(BIBTEX) $(basename $(REPORT_LOC))
	$(LATEX)  $(basename $(REPORT_LOC)).tex
	$(LATEX)  $(basename $(REPORT_LOC)).tex

$(REPORT_PUB) pub : $(REPORT_LOC)
	cp $(REPORT_LOC) $(REPORT_PUB)

$(REPORT_DEL) del : $(REPORT_LOC)
	cp $(REPORT_LOC) $(REPORT_DEL)

view: $(REPORT_LOC)
	${PDF_VIEWER} $<

# To expand macros.
%.tex: %.cjt $(PROJECT_CSV_FILES) $(CALJINTEX)
	$(CALJINTEX) --template $< --csv-dir $(PROJECT_CSV_DIR) --output $@  --reporting-quarters $(REPORTING_QUARTERS)




# To check broken cross-refs.
REPORT_LOG=${REPORT_LOC:.pdf=.log}
REPORT_BLG=${REPORT_LOC:.pdf=.blg}
xref xrefs :
	-grep Citation  ${REPORT_LOG} 
	-grep Reference ${REPORT_LOG}
	-grep Label     ${REPORT_LOG}
	-grep "WARN "   ${REPORT_BLG}

# Dummy targets.
test:
	@echo DATE=${DATE}
	@echo REPORT_CST_TEX=${REPORT_CST_TEX}
	@echo PDF_TARGET_DIR=${PDF_TARGET_DIR}
	@echo REPORT_LOC=${REPORT_LOC}
	@echo REPORT_PUB=${REPORT_PUB}
	@echo REPORT_DEL=${REPORT_DEL}

clean clear:
	rm -rf *-blx.bib *run.xml *.aux *.bbl *.blg *.dvi *.toc *.log *.ps *.out *.lot *.lof *.glg *.glo *.gls *.bcf *.xdy *.ist *.vrb *.nav *.snm *~ 

clobber: clean
	rm -rf *.pdf 
