# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line.
SPHINXOPTS    =
SPHINXBUILD  := `sh -c '[ -e /usr/bin/sphinx-build-3 ] && echo sphinx-build-3 || echo sphinx-build'`
SPHINXPROJ    = Flatpak
SOURCEDIR     = ../docs
BUILDDIR      = ../docs/_build

SPHINXINTL    = sphinx-intl
PO_LINGUAS    = $(shell grep -v "^\#" ./LINGUAS)
LANGS         = 

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
	@echo ""
	@echo "Extra target:"
	@echo "  update-po   to generate POT and update PO files for target languages"
	@echo ""
	@echo "Hint: Use LANGS variable to build docs for a single language."
	@echo "  e.g.  make html LANGS=fr"

# Generate POT and update PO files for target languages
update-po:
	@make -C $(SOURCEDIR) gettext SPHINXOPTS=
	@OPTS=; \
	for l in $(LANGS); do \
		OPTS="$${OPTS} -l $${l}"; \
	done; \
	$(SPHINXINTL) update -d . -p $(BUILDDIR)/gettext $${OPTS}

.PHONY: help update-po Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	for l in $(LANGS); do \
		echo "Building documentation in '$${l}' ..."; \
		$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)/$${l}" -D language="$${l}" $(SPHINXOPTS) $(O); \
	done
