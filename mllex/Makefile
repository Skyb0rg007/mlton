## Copyright (C) 2009,2013,2018-2019 Matthew Fluet.
 # Copyright (C) 1999-2006 Henry Cejtin, Matthew Fluet, Suresh
 #    Jagannathan, and Stephen Weeks.
 # Copyright (C) 1997-2000 NEC Research Institute.
 #
 # MLton is released under a HPND-style license.
 # See the file MLton-LICENSE for details.
 ##

ROOT := ..
include $(ROOT)/Makefile.config

######################################################################

NAME := mllex

all:	$(NAME)

$(NAME): $(NAME).mlb $(shell "$(RUN_MLTON)" -stop f $(NAME).mlb)
	@echo 'Compiling $(NAME)'
	"$(RUN_MLTON)" @MLton $(RUN_MLTON_RUNTIME_ARGS) -- $(RUN_MLTON_COMPILE_ARGS) -target $(TARGET) $(NAME).mlb

.PHONY: clean
clean:
	$(SRC)/bin/clean


PDFLATEX := pdflatex

lexgen.pdf: lexgen.tex
	$(PDFLATEX) lexgen.tex
	$(PDFLATEX) lexgen.tex
	$(PDFLATEX) lexgen.tex

mllex.pdf: lexgen.pdf
	cp lexgen.pdf mllex.pdf

DOCS :=
ifneq ($(shell which $(PDFLATEX) 2> /dev/null),)
DOCS += mllex.pdf
endif

.PHONY: docs
docs: $(DOCS)


.PHONY: test
test: $(NAME)
	cp -p ../mlton/front-end/ml.lex .			\
	$(NAME) ml.lex &&					\
	$(DIFF) ml.lex.sml ../mlton/front-end/ml.lex.sml	\
	rm -f ml.lex ml.lex.sml
