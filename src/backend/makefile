VENV = env
VIRTUAL_ENV := $(abspath ${VENV})

VENV := $(VIRTUAL_ENV)/bin/python


run:
	clear
	$(VENV) manage.py runserver
run-lan:
	$(VENV) manage.py runserver 192.168.8.101:8000

migrations:
	clear
	$(VENV) manage.py makemigrations

migrate:
	clear
	$(VENV) manage.py migrate

test:
	clear
	$(VENV) manage.py test

superuser:
	clear
	$(VENV) python manage.py createsuperuser

shell:
	clear
	$(VENV) python manage.py shell

createcharges:
	$(VENV) python manage.py createcharges


req:
	$(VENV) pip freeze > requirements.txt

celery-run:
	clear
	celery -A backend worker -l INFO

celery-beat-run:
	celery -A backend beat -l info --scheduler django_celery_beat.schedulers:DatabaseScheduler

celery-beat:
	celery -A backend worker --beat --scheduler django --loglevel=info

redis-server:
	redis-server

fix-redis-server:
	ulimit -n 10032
	redis-cli shutdown
	killall redis-server; redis-server

docker:
	systemctl start docker
	systemctl enable docker
	systemctl status docker.service

startdocker:
	sudo systemctl unmask docker
	systemctl start docker
	systemctl status docker

docker-build:
	docker-compose build

docker-up:
	docker-compose up

docker-bash:
	docker exec -it django_container /bin/bash

docker-shell:
	docker exec -it django_backend sh

docker-stop:
	docker stop $(docker ps -a -q)
	docker rm $(docker ps -a -q)

docker-remove-all:
	docker rm $(docker ps -a -f status=exited -q)
