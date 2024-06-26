.POSIX:

VERSION = 1.1.0
NAME = lambdapi-mode
# The path to lambdapi built by dune
LAMBDAPI = ../../_build/install/default/bin/lambdapi

EMACS = emacs

SRC =
SRC += lambdapi-abbrev.el
SRC += lambdapi-capf.el
SRC += lambdapi-input.el
SRC += lambdapi-layout.el
SRC += lambdapi-mode.el
SRC += lambdapi-mode-pkg.el
SRC += lambdapi-proofs.el
SRC += lambdapi-smie.el
SRC += lambdapi-vars.el

$(NAME)-$(VERSION).tar: $(SRC)
	mkdir -p "$(NAME)-$(VERSION)"
	cp *.el "$(NAME)-$(VERSION)"
	tar -cf "$(NAME)-$(VERSION)".tar "$(NAME)-$(VERSION)"

.PHONY: install
install:
	@echo "See https://lambdapi.readthedocs.io/en/latest/emacs.html \
	for instructions on how to install the lambdapi mode for Emacs. \
	If you know what you're doing, you can install the development version with" \
	| fmt
	@echo "$$ make dist"
	@echo "and in emacs"
	@echo "M-x package-install-file RET $(NAME)-$(VERSION).tar RET"

.PHONY: dist
dist: $(NAME)-$(VERSION).tar

.PHONY: check
check: dist
	# This rule depends on the layout of dune. It builds the lambdapi
	# binary so that the "sandboxed" emacs can access it.
	cd ../.. && $(MAKE) lambdapi
	./test.sh "$(NAME)" "$(VERSION)" "$(LAMBDAPI)"

.PHONY: clean
clean:
	rm -f "$(NAME)-$(VERSION)".tar
	rm -rf "$(NAME)-$(VERSION)"
