# Makefile for building TeX documents with pdflatex and cleaning aux files

# Tools and options
PDFLATEX := pdflatex
LATEX_OPTS := -interaction=nonstopmode -halt-on-error

# All TeX sources in the current directory (exclude editor backups)
TEX_SRCS := $(filter-out %~,$(wildcard *.tex))
PDFS := $(TEX_SRCS:.tex=.pdf)

# Default: build all PDFs
all: $(PDFS)

# Pattern rule: build each PDF with two passes for cross-references
%.pdf: %.tex
	@echo "==> Compiling $<"
	@$(PDFLATEX) $(LATEX_OPTS) $< >/dev/null
	@$(PDFLATEX) $(LATEX_OPTS) $< >/dev/null
	@echo "==> Done: $@"

# Convenience targets to build specific documents (optional)
main: main.pdf
notes: Notes.pdf
distnotes: Notes_On_Distribution.pdf

# Remove LaTeX auxiliary files
clean:
	@echo "==> Cleaning auxiliary files"
	@rm -f *.aux *.log *.out *.toc *.snm *.nav *.fls *.fdb_latexmk *.synctex.gz \
	      *.lof *.lot *.bbl *.blg *.dvi

# Remove aux files + generated PDFs
distclean: clean
	@echo "==> Removing generated PDFs"
	@rm -f $(PDFS)

.PHONY: all clean distclean main notes distnotes
