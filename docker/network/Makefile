#!/bin/bash

CONTAINER = platform-network-machine-es
UID = $(shell id -u)

help: ## Show this help message
	@echo 'usage: make [target]'
	@echo
	@echo 'targets:'
	@egrep '^(.+)\:\ ##\ (.+)' ${MAKEFILE_LIST} | column -t -c 2 -s ':#'

run: ## Start the containers
	U_ID=${UID} docker-compose up -d

stop: ## Stop the containers
	U_ID=${UID} docker-compose stop

down: ## Stop the containers
	U_ID=${UID} docker-compose down

restart: ## Restart the containers
	$(MAKE) stop && $(MAKE) run

build: ## Rebuilds all the containers
	U_ID=${UID} docker-compose build

ssh: ## ssh's into the container
	U_ID=${UID} docker exec -it --user ${UID} ${CONTAINER} bash