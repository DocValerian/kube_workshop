# -------------------------------------------------
# general best practice make flags - see http://clarkgrubb.com/makefile-style-guide
# -------------------------------------------------
MAKEFLAGS += --warn-undefined-variables
SHELL := bash
.SHELLFLAGS := -e -o pipefail -c
.DEFAULT_GOAL := all
.DELETE_ON_ERROR:
.SUFFIXES:

# -------------------------------------------------
# MAKE all
# -------------------------------------------------

.PHONY: all
all:
	@echo "Demo Makefile"
	@echo ""
	@echo "Possible Targets:"
	@less Makefile | grep .PHONY[:] | cut -f2 -d ' ' | xargs -n1 -r echo " - "

# -------------------------------------------------
# MAKE build targets
# -------------------------------------------------


.PHONY: install
install: namespace application
	@echo "finished setup"

.PHONY: namespace
namespace:
	@echo "Generating Namespace"
	@kubectl apply -f ./demo2-namespace.yaml
	@echo "...done"


.PHONY: application
application:
	@echo "Deploying application"
	@kubectl apply -f ./cassandra-ds.yaml --record
	@echo "...done"