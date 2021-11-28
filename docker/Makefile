#!/bin/bash

OS := $(shell uname)

ifeq ($(OS),Darwin)
	UID = $(shell id -u)
else ifeq ($(OS),Linux)
	UID = $(shell id -u)
else
	UID = 1000
endif

help: ## Show this help message
	@echo 'usage: make [target]'
	@echo
	@echo 'targets:'
	@egrep '^(.+)\:\ ##\ (.+)' ${MAKEFILE_LIST} | column -t -c 2 -s ':#'

run: ## Start the containers
	U_ID=${UID} docker-compose -f ./network/docker-compose.yml up -d --build
	U_ID=${UID} docker-compose -f ./mysql/docker-compose.yml --env-file ./mysql/.env up -d --build
	U_ID=${UID} docker-compose -f ./rabbitmq/docker-compose.yml up -d --build
	U_ID=${UID} docker-compose -f ./webserver-api/docker-compose.yml up -d --build

down: ## Down the containers
	U_ID=${UID} docker-compose -f ./webserver-api/docker-compose.yml down
	U_ID=${UID} docker-compose -f ./rabbitmq/docker-compose.yml down
	U_ID=${UID} docker-compose -f ./mysql/docker-compose.yml --env-file ./mysql/.env down
	U_ID=${UID} docker-compose -f ./network/docker-compose.yml down
