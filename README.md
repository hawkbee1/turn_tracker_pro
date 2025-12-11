turn tracker pro
Track play time for each players during board games sessions.

This porject is mad with flutter framework. Bot frontend end backend is using dart thanks to the serverpod project
Dev is made completly in docker environement, here is the model for the docker compose file: 

# docker compose --file docker-compose-turn_tracker_pro.yaml up --build --detach
name: turn_tracker_pro

services:
  postgres:
    image: pgvector/pgvector:pg16
    ports:
      - '8090:5432'
    environment:
      POSTGRES_USER: hawkbee
      POSTGRES_DB: turn_tracker_pro
      POSTGRES_PASSWORD: "XXXXXXXXXXXXX"
    restart: always
    tty: true
    volumes:
      - turn_tracker_pro_data:/var/lib/postgresql/data
  redis:
    image: redis:8.4.0
    restart: always
    ports:
      - '8091:6379'
    command: redis-server --requirepass "XXXXXXXXXXXXXXXXXXXXX"
    environment:
      - REDIS_REPLICATION_MODE=master
  flutter:
    image: flutter:3.38.3
    restart: always
    tty: true
volumes:
  turn_tracker_pro_data:

You need to update turn_tracker_pro_server/config/development.yaml and turn_tracker_pro_server/config/passwords.yaml to set your settings correctly

