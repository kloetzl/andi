ACLOCAL_AMFLAGS = ${ACLOCAL_FLAGS} -I m4
AM_DISTCHECK_CONFIGURE_FLAGS="--enable-unit-tests"

.PHONY: all

SUBDIRS = . libs opt src docs
DIST_SUBDIRS = . libs opt src docs test

# Conditionally build the tests
if BUILD_TESTS

SUBDIRS+= test

AM_TESTS_ENVIRONMENT= \
	RANDOM_SEED='@SEED@' ; export RANDOM_SEED ;

XFAIL_TESTS=
TESTS = $(XFAIL_TESTS) test/nan.sh test/low_homo.sh test/test_esa test/test_seq test/test_extra.sh test/test_random.sh test/test_join.sh test/test_process

$(TESTS): src/andi

endif # BUILD_TESTS


dist_noinst_DATA = ChangeLog README.md
dist_pdf_DATA = andi-manual.pdf
dist_noinst_SCRIPTS= scripts/maf2phy.awk scripts/vmatch.sh scripts/_andi

# Recreate the changelog, when the version string changes.
ChangeLog: configure.ac
	echo "Missing Git" > ChangeLog;
	if test -d $(srcdir)/.git; then \
		which git && git log --stat --date=short --abbrev-commit | grep --invert-match '^ [[:alnum:].]' | git stripspace > ChangeLog; \
	fi

.PHONY: code-docs
code-docs:
	cd docs && $(MAKE) code-docs;
