all: build

build:
	@docker build --rm=false --tag=${USER}/activiti6 .

test:
	build
	@docker run --name='activiti6' \
	-it \
	--rm \
	-p 8080:8080 \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $$(which docker):/bin/docker \
	${USER}/activiti6

run:
	@docker run --name='activiti6' \
        -d \
	-p 8080:8080 \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $$(which docker):/bin/docker \
	${USER}/activiti6

prod:
	@docker run --name='activiti6' \
        -d \
	-p 8080:8080 \
        --link activiti-mysql:mysql \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $$(which docker):/bin/docker \
	${USER}/activiti6

logs:
	@docker logs -f activiti6
