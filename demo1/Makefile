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
install: namespace secrets application
	@echo "finished setup"

.PHONY: namespace
namespace:
	@echo "Generating Namespace"
	@kubectl apply -f ./demo1-namspace.yaml
	@echo "...done"

.PHONY: secrets
secrets:
	@echo "Generating Secrets"
	@kubectl create secret generic mysql-pass --from-file=demo1/password.txt --namespace demo1
	@echo "...done"

.PHONY: application
application:
	@echo "Deploying application"
	@kubectl apply -f ./volumes/. -R --record
	@kubectl apply -f ./mysql/. -R --record
	@kubectl apply -f ./wordpress/. -R --record
	@echo "...done"

.PHONY: clean
clean:
	@echo "Cleaning Deployment"
	@kubectl delete namespace demo1
	@echo "...done"