
```
version: '3'

services:
  postgres:
    image: postgres:latest
    environment:
      POSTGRES_DB: mmensing
      POSTGRES_USER: mmensing
      POSTGRES_PASSWORD: 0000
    ports:
      - "5432:5432"
    networks:
      - your_network_name

  django:
    build:
      context: .
      dockerfile: backend/Dockerfile
    ports:
      - "8000:8000"
    depends_on:
      - postgres
    networks:
      - your_network_name

networks:
  your_network_name:
    driver: bridge
```
