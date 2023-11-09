
- create 3 container for:
	- maria db:
		- build image:
			- run ```docker build -t <image_name> .``` in the MariaDB folder to build image
				- ```docker build``` -> build a docker image
				- ```-t <image_name>``` -> -t lets you tag a name
				- ```.``` -> docker takes all files and subdirectories
		- create container:
			- run ```docker run -d --name <container_name> -p 3306:3306 <image_name>```
				- ```docker run``` -> run new container
				- ```-d``` -> runs container in *detached* mode -> runs in the background and prints container ID
				- ```--name <container_name>``` -> allows to specify the containers name
				- ```-p 3306:3306```-> -p maps a port from the host to the container (here 3306)
	- wordpress
	- nginx


ok lol start with ngnix, then connect this with wordpress and then with mariad


- containerize nginx:
	- set Dockerfile:
		- structure local:```
			NGINX/ 
			├── Dockerfile 
			├── conf/ 
			│     └── nginx.conf 
			└── tools/
			│     └── html/ 
			│			  └── index.html```
		- create two directories INSIDE of the container:
			- ```RUN mkdir -p /etc/nginx/conf.d```
			- ```RUN mkdir -p /usr/share/nginx/html```
		- now we copy the local config file and index file into the crated folder in the container
			- ```COPY ./conf/nginx.conf /etc/nginx/conf.d/default.conf```
				- copies local ```./conf/nginx.conf``` file into ```/etc/nginx/conf.d/defailt.conf```
			- ```COPY ./tools/html /usr/share/nginx/html```
				- copies local ```./tools/html``` folder into ```/usr/share/nginx/html```
	- create image:
		- ```docker build -t <image_name> ./NGINX``` -> image_name gets assigned here
		- run ```docker images``` it should show the created image:
			- eg. ```lol-test-ngnix-image  latest  fdc9e27ce805  2 minutes ago  187MB```
		- you can remove images you don't need anymore with:
			- ```docker rmi IMAGE_ID``` (run ```docker images``` to get IMAGE_ID)
	- create container:
		- run ```docker run -d --name <container_name> -p 127.0.01:443:443 <image_name>```
			-  ```docker run``` -> new container
			- ```-d``` -> container runs in *detached* mode -> runs in the background and prints container ID
			- ```--name <container_name>``` -> allows to specify the containers name
			- ```-p 127.0.0.1:443:443```-> -p maps a port from the host to the container (here 443)
	- create self assigned certificate: grr???
		- ```openssl req -x509 -nodes -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365```
			- created key: ```key.pem```
			- and certificate ```cert.pem``` valid for 365 days
	- create volume for it:
		- ```docker volume create nginx-certs```
	- copy key and certificate to volume *nginx_certs*:
		- ```docker run --rm -v nginx-certs:/certs -w /certs \ -v /path/to/local/certs:/local-certs \ alpine sh -c "cp /local-certs/* ."```



- run bash inside the container:
	- run ```docker ps```


- show all images:
	- ```docker images```
- delete image:
	- ```docker rmi IMAGE_ID```

- show all containers:
	- ```docker ps```
- delete container:
	- ```docker rm CONTAINER_ID```
- stop container:
	- ```docker stop IMAGE_ID```