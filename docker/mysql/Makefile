#!/bin/bash

CONTAINER = developed-platform-db
UID = $(shell id -u)

help: ## Show this help message
	@echo 'usage: make [target]'
	@echo
	@echo 'targets:'
	@egrep '^(.+)\:\ ##\ (.+)' ${MAKEFILE_LIST} | column -t -c 2 -s ':#'

run: ## Start the containers
	U_ID=${UID} docker-compose --env-file ./.env up -d --build

down: ## Stop the containers
	U_ID=${UID} docker-compose --env-file ./.env down

stop: ## Stop the containers
	U_ID=${UID} docker-compose stop

restart: ## Restart the containers
	$(MAKE) stop && $(MAKE) run

build: ## Rebuilds all the containers
	U_ID=${UID} docker-compose --env-file ./.env build

ssh: ## ssh's into the container
	U_ID=${UID} docker exec -it --user ${UID} ${RAB}