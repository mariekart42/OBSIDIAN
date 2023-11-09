
- start docker application
- run ```npm run db:rm:up```  to remove and create container with postgres
- run ```npm run prisma:dev:deploy``` to migrate changes into prisma database
	- if it returns ```Error: P1001: Can't reach database server at localhost:5434```, just run again (needs time between starting docker and migrating)
- run ```npm run start:dev``` to start the application
- run ```npx prisma studio``` to start browser prisma database (!in root folder)