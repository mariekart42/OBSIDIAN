




- Install Python: !python3
	- run ```export PATH="/Users/mmensing/Library/Python/3.9/bin:$PATH"```
		- sets up path for python dependencies
	- run ```python3 -m pip install --upgrade pip setuptools``` 
		- update pip and setuptools
-  Create & init virtual environment: 
	- run ```python3 -m venv .<env_name>```
		- creates a virtual environment for python with name ```env_name```
	- run ```. .<env_name>/bin/activate```
		- activates the environment
	- run ```pip install django```
		- installs Django into created virtual environment
	- run ```pip install djangorestframework```
- Create Django Project:
	- run ```django-admin startproject <project_name> .```
		- start new project -> creates folder in current dir
- run ```python manage.py runserver``` to start the server
- run ```python manage.py migrate``` to migrate changes database
- open ```http://127.0.0.1:8000/admin/``` in browser to see database content
- run ```python manage.py createsuperuser``` to create admin user
- create ```models.py``` file and add the fields needed, to apply them to database, first
- run ```python manage.py makemigrations <project_name>``` to create the migrations, then
- run ```python manage.py migrate``` to apply the migrations
- create file ```admin.py``` in app directory and import the created module





- normal:
	- run ```. .myEnv/bin/activate``` each time starting project/open new terminal!

 ![[Bildschirmfoto 2023-11-03 um 5.16.57 PM.png]]