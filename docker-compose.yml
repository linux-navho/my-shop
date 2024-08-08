version: "3"
services:
  
  server:
    build:
      context: .
      dockerfile: Dockerfile 
    command: ["npm", "run", "start:server"]
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.my-shop.rule=Host(`api.navhocreatives.store`)"  # Adjusted router name
      - "traefik.http.routers.my-shop.entrypoints=https"
      - "traefik.http.routers.my-shop.tls=true"
      - "traefik.http.services.my-shop.loadbalancer.server.port=3000"  # Adjusted service name
    networks:
      - external
    volumes:
      - /usr/src/app
    environment:
      DB_HOST: database
      DB_PORT: 5432
      DB_NAME: vendure
      DB_USERNAME: postgres
      DB_PASSWORD: password
 
  worker:
    build:
      context: .
      dockerfile: Dockerfile
    command: ["npm", "run", "start:worker"]
    volumes:
      - /usr/src/app
    environment:
      DB_HOST: database
      DB_PORT: 5432
      DB_NAME: vendure
      DB_USERNAME: postgres
      DB_PASSWORD: password
 
  database:
    image: postgres
    volumes:
      - /var/lib/postgresql/data
    ports:
      - 5432:5432
    environment:
      POSTGRES_PASSWORD: password
      POSTGRES_DB: vendure

networks:
  external:
    external: true