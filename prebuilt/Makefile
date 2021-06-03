# based on: https://github.com/onnovalkering/brane/blob/master/Makefile

start-instance: \
	create-kind-network \
	start-services \
	format-dfs \
	start-brane

stop-instance: \
	stop-ide \
	stop-brane \
	stop-services

start-services:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-svc.yml up -d

stop-services:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-svc.yml down

start-brane:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-brn.yml up -d

stop-brane:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-brn.yml down

start-ide:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-ide.yml up -d

stop-ide:
	COMPOSE_IGNORE_ORPHANS=1 docker-compose -p brane -f docker-compose-ide.yml down

create-kind-network:
	if [ ! -n "$(shell docker network ls -f name=kind | grep kind)" ]; then \
		docker network create kind; \
	fi;

# JuiceFS
format-dfs:
	docker run --network kind onnovalkering/juicefs \
		format \
		--access-key minio \
		--secret-key minio123 \
		--storage minio \
		--bucket http://minio:9000/data \
		redis \
		brane

# JupyterLab IDE
jupyterlab-token:
	@docker logs brane_brane-ide_1 2>&1 \
	| grep "token=" \
	| tail -1 \
	| sed "s#.*token=##"

