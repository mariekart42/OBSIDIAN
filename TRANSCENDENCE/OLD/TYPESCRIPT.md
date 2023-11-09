

[NextJS](https://docs.nestjs.com/first-steps)

- Installation npm:
	- run ```npm i -g @nestjs/cli```
		- Problem to install npm?:
			- If you don't have Permissions to install npm on school macs, you need to change the default path where npm will put all its data
				- Change npm's default directory:
					- run ```mkdir ~/.npm-global```
					- run ```npm config set prefix '~/.npm-global'```
					- run ```export PATH=~/.npm-global/bin:$PATH```
					- run  ```source ~/.zshrc``` (to apply changes)
						- npm data is now stored in:   */Users/mmensing/.npm/*
- Create new project:
	- run ```nest new <project-name>```
- run program options:
	- normal:
		- ```npm run start```
	- 20x faster:
		- ```npm run start -- -b swc```
	- compile live changes:
		- ```npm run start:dev```
	- better error output:
		- ```npm run lint```
	- with prettier:
		- ```npm run format```

- noice ressources:
	- [project with visual explanation](https://git.42l.fr/frdescam/transcendence)

- [Docker set-up:](https://docs.docker.com/compose/gettingstarted/)
	- run ```docker ps``` to check if docker works
	- set up ```docker-compose.yml```  file
	``` 
		version: '3.8'  
			services:  
				marieee:  
				image: postgres:13  
				ports:  
				- "5434:5432"  
				environment:  
				POSTGRES_USER: postgres  
				POSTGRES_PASSWORD: 6969  
				POSTGRES_DB: nest
	```
	- run ```docker compose up <name> -d``` to start the container (name here -> marieee)
	 - run ```docker ps``` again and copy the ```CONTAINER ID```
	- then run ```docker logs <CONTAINER ID>```
		- it should show: ```database system is ready to accept connections```
- [Prisma:](https://www.prisma.io/)
	- *connection between TypeScript code and Database*
	- **Set up:**
		- got to the root of the project (NOT inside src)
		- run ```npm add -D prisma```
			- adds the Prisma CLI (Command Line Interface) as a development dependency to your project
		- and ```npm add @prisma/client```
			- add the Prisma Client package as a dependency to your project
		- run ```npx prisma init```
			- creates all necessary files in the current directory
			- created .env file with ```DATABASE_URL``` string in it
				- eg. ```DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"```
			- set ```DATABASE_URL``` in ```.env``` file:
				- ```DATABASE_URL="postgresql://<POSTGRES_USER>:<POSTGRES_PASSWORD>d@localhost:<ports>/<POSTGRES_DB>?schema=public"```
				- place data from ```docker-compose.yml``` file in there
			- created prisma folder with ```schema.prisma``` file inside
			-  declare Modules in there
				- eg.: 
				```
				model User {
					id Int @id @default(autoincrement())
					email String @unique
					name String?
					posts Post[]
				}
				
				model Post {
					id Int @id @default(autoincrement())
					title String
					content String?
					published Boolean @default(false)
					author User @relation(fields: [authorId], references: [id])
					authorId Int
				}
				```
		- run ```npx prisma --help``` for any help
	- **Migrate:**
		- run ```npx prisma migrate dev```
			- also run for any changes made in prisma schema
			- generated sql in new folder migrations
			- migrations/
			  └─ 20231020154424_init_new_lol/
					└─ migration.sql
			- database now knows about tables we created as models in ```schema.prisma```
		- run ```npx prisma generate``` to automatically add model content into program
		- run ```npx prisma studio``` to open prisma interface in browser
	- **Connect Prisma with Code:**
		- create Folder in src (prisma) with module file
		- pls more here





- Validation:
	- install [Class Validator](https://docs.nestjs.com/techniques/validation) (from NestJS)
		- ```npm i --save class-validator class-transformer```
	- in dto we now can use special decorators provided by class-validator like:
		- ```@IsString(), @IsNotEmpty(), @IsEmail()```
			- will check for these cases and will throw error if not valid
		- -> Business logic code afterwards only runs, if validationPipe is satisfied
- Hash password:
	- received password from user gets hashed -> security reasons
		- ! [bycript](https://www.npmjs.com/package/bcrypt) only handles 72 bytes, we won't use that but [argon2](https://argon2.online/)
	- run ```npm add argon2``` to install argon2
	- import argon2 into code:  ```import * as argon from 'argon2'```
	- generate password hash:
		- ```const hash = argon.hash(dto.password)```
	- save new user to database:
	```
		const user = await this.prisma.user.create({  
			data: {  
				email: dto.email,  
				hash: hash,  
			}  
		})
	```
- scripts json:
	- restart Database:
		1. remove container:
			- ```"db:dev:rm": "docker compose rm <db_name> -f -s -v"```
				- eg. ```docker compose rm marieee -f -s -v```
		2. create container:
			- ```"db:dev:up": "docker compose up <db-name> -d"```
		- concatenate both statements:
			- ```"db:dev:restart": "npm run db:dev:rm && npm run db:dev:up"```
		- run ```npm run db:dev:restart```
		- BUT migrations are not applied yet
		- apply migrations:
		- but now we don't want to create each time a new migration but implement the new content on top of the old one (=migrate)
		- apply migrations:
			- ```"prisma:dev:deploy": "prisma migrate deploy"```
		- concatenate with restart db:
			- ```"db:dev:restart": "npm run db:dev:rm && npm run db:dev:up && npm run prisma:dev:deploy"```
		- ! slow devices may need more time, we only want to deploy if container already restarted == ```sleep 15```
			- sometimes says that port can't be reached, then set the time higher
	- => ```"db:dev:restart": "npm run db:dev:rm && npm run db:dev:up && sleep 15 && npm run prisma:dev:deploy"```
- [Authentication:](https://docs.nestjs.com/security/authentication)
	-  config Module:
		- ```run npm add @nestjs/config```
		-  import it to app.module
	- NestJS uses [Passport](https://www.passportjs.org/)  and [JWT](https://jwt.io/) so we have to install it:
		- ```npm add @nestjs/passport passport```
		- ```npm add @nestjs/jwt passport-jwt```
		- ```npm add -D @types/passport-jwt```
	- import JWTModule to auth.module
	- 




- **Code stuff:**
	- export class:
		-  class that is available in the whole program
	- Constructor:
		- ```constructor(private name_of_Instance: AuthService) { }```
		- constructor inits and creates Instance of AuthService
	- ???:
		- await
		- async
		- Promise
		- interface (something like struct?)
		- class name **implements** name
	-  Controllers:
		- handle incoming HTTP requests and return responses
	-  Services:
		- handle Business Logic like connecting to Database

Nest automatically identifies Content-Type :)

install multer for creating Post requests: ```npm install --save @nestjs/platform-express multer```


- ```@Get('(*)')``` and ```@Get()``` are the same BUT in controller we need ```@Controller('(*)')```




