include LaTeX.mk
# PDFLATEX="pdflatex" # -shell-escape
PDFLATEX_OPTIONS=-shell-escape
ARCHIVE=POLARIS
all: presentation.tex presentation-gz.pdf

%.tex: %.org
	emacs -batch --eval "(setq enable-local-eval t)" --eval "(setq enable-local-variables t)" $^  --funcall org-beamer-export-to-latex
	mv $@ $@.bak
	echo '\def\\raggedright{}' > $@
	cat $@.bak >> $@

%-gz.pdf: %.pdf
	gzprez $<

$(ARCHIVE).tgz:
	tar --xform "s|^|$(ARCHIVE)/|" -zcf $@ `git ls-tree -r master --name-only | grep -v -e '.*-gz.pdf'`
