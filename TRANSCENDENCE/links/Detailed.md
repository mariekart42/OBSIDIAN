

- Setup virtual environment:
	- run ```python3.9 -m venv <choose_venv_name>```
	- run ```source <venv_name>/bin/activate``` to activate venv
-  upgrade pip to the latest version:
	- ```python3.9 -m pip install --upgrade pip```
-  install Django:
	- run ```python3.9 -m pip install Django``` INSIDE of the venv
- create project:
	- run ```django-admin startproject <choose_app_name>``` inside the root folder
- create docker-compose file:
	- ```touch docker-compose.yml```  🔗 [init](docker-compose.yml.md)
- create Dockerfile for backend:
	- ```touch <app_name>/Dockerfile```   🔗 [init](Dockerfile_backend.md)
- create shell script:
	- ```touch script.sh```   🔗 [init](scheise.sh)