NAME = posos-challenge
USER = appuser
PWD = $(shell pwd)
UID = $(shell id -u)
GID = $(shell id -g)


.PHONY: test
test:
	UID=$(UID) GID=$(GID) docker-compose build
	UID=$(UID) GID=$(GID) docker-compose up
	UID=$(UID) GID=$(GID) docker-compose down

.PHONY: build_exp
build_exp:
	docker build -f Dockerfile --tag $(NAME)_exp\
		--build-arg uid=$(UID)\
		--build-arg gid=$(GID)\
		.

.PHONY: exp
exp: build_exp clean_exp
	docker run --rm\
	        --name=$(NAME)_exp\
	        -v $(PWD):/app\
			-p 8888:8888\
	        $(NAME)_exp:latest

.PHONY: clean_exp
clean_exp:
	docker rm -f $(NAME)_exp 2> /dev/null || true