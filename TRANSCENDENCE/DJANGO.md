


```When working with Docker and Python projects like Django, it's a good practice to use both virtual environments and Docker containers```


- 🚀   **Structure:**   __[here](Structure.md)__  🔗

- 🚀   **SetUp:**
	-   Detailed   __[here](Detailed.md)__  🔗
	-   Quick   __[here](Quick.md)__  🔗

- 🚀   **Admin:**
	- create super-user:
		- run ```python3.9 backend/manage.py createsuperuser```
		- fill out requested fields
	- modify ```backend/admin.py``` file:
		- import created modules	:
			- ```from .models import <new_module>, <new_Module>, ...```
		- register created modules:
			- ```admin.site.register(<new_module>)```
			- ```admin.site.register(<new_module>)```




- create app inside of parentfolder ```backend```:
	- ```python3.9 manage.py startapp <choose_app_name>```



- tool ajax!!
	- allows to get stuff from database in realtime


- create superuser





- database stuff:
	- making migrations:
		- run ```python3.9 manage.py makemigrations``` to init Django models into database files




- starting server in python:
	  ```python3.9 -m http.server 9000```
