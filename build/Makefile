# Meta targets
.PHONY: clean test runtest
.SILENT:

# Source directory names
SOURCE_DIRS=$(shell find -L . -type d)

# Basic GNAT flag setup
GNATLINKFLAGS=
GNATBINDFLAGS=
GNATMAKEFLAGS=

GNATMAKEFLAGS+=-d # Display progress
GNATMAKEFLAGS+=-eL # Follow symbolic links
GNATMAKEFLAGS+=-F # Use full pathnames (simplifies vim :make)
GNATMAKEFLAGS+=-gnatU # Tag errors with "error:"
GNATMAKEFLAGS+=-gnatVa # Enable validity checking
GNATMAKEFLAGS+=-gnatef # Use full pathnames in errors too
GNATMAKEFLAGS+=-gnaty4aAbcdefhiklL12mM80noprSstux # Mandate style guide
# Style flags are:
# 4 - Proper indentation with tabs set at 4 spaces
# a - Proper attribute casing
# A - Clear array attributes (no index on 1D, full index on nD)
# b - No blanks at the end of statements
# c - Comments don't suck
# d - No DOS EOLs
# e - Ends/Exits must have labels
# f - No form feeds or vtabs
# h - No TAB characters
# i - If then layout must be decent
# k - All lowercase keywords
# l - Proper layout
# L12 - Can't nest deeper than 12 levels of nesting
# m - Sufficiently short lines
# M80 - Maximum line length is 80 characters
# n - Standard types are appropriately cased
# o - Subprograms are in alphabetical order
# p - Proper pragma casing
# r - Identifiers must stay the same case
# S - No statements on the same line as then or else
# s - Everything has a spec
# t - Super picky token spacing
# u - No unnecessary blank lines
# x - No extra parenthesis (especially if (x) style)

INCLUDE_DIRS=$(patsubst %,-I%,$(SOURCE_DIRS))

GNATMAKE=gnatmake
GNATLINK=--GNATLINK="gnatlink $(GNATLINKFLAGS)"
GNATBIND=--GNATBIND="gnatbind $(GNATBINDFLAGS)"
GNATOPTS=$(GNATLINK) $(GNATBIND) $(GNATMAKEFLAGS)

################################################################################
# TARGETS                                                                      #
################################################################################

# Test Executable
TEST_SRC=test/main.adb
TEST_EXE=../bin/test.out
test : $(TEST_EXE)

$(TEST_EXE) : force_make
	$(GNATMAKE) $(TEST_SRC) -D. $(INCLUDE_DIRS) -o $@ $(GNATMAKEFLAGS)

runtest :
	$(TEST_EXE)


################################################################################
# METATARGETS                                                                  #
################################################################################

clean :
	-rm -f *.ali
	-rm -f *.o
	-rm -f *.gcno
	-rm -f *.gcda

force_make:
	true
