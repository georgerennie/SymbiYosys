test:

.PHONY: test clean refresh help

help:
	@cat make/help.txt

export SBY_WORKDIR_GITIGNORE=1
export SBY_MAIN=$(realpath $(dir $(firstword $(MAKEFILE_LIST)))/../sbysrc/sby.py)

make/rules/collect.mk: make/collect_tests.py
	python3 make/collect_tests.py

make/rules/test/%.mk:
	python3 make/test_rules.py $<

ifneq (help,$(MAKECMDGOALS))

# This should run every time but only trigger anything depending on it whenever
# the script overwrites make/rules/found_tools. This doesn't really match how
# make targets usually work, so we manually shell out here.

FIND_TOOLS := $(shell python3 make/required_tools.py || echo error)

ifneq (,$(findstring error,$(FIND_TOOLS)))
$(error could not run 'python3 make/required_tools.py')
endif

ifneq (,$(FIND_TOOLS))
$(warning $(FIND_TOOLS))
endif

include make/rules/collect.mk

endif
