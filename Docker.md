Dockerfile.dev: (docker build -f Dockerfile.dev)
FROM node:alpine 
WORKDIR '/app'
COPY package.json
RUN nmp install
COPY . . 
CMD ["npm", "run", "start"]

docker-compose.yml:
version: '3'
services:
    web:
        build: 
          context: . 
          dockerfile: Dockerfile.dev 
        ports:
          - "3000:3000"
        volumes:
          - /app/node_modules
          - .:/app
