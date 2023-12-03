# gpt4all-api

Docker image: https://hub.docker.com/repository/docker/thanhtung100397/gpt4all_api

Docker compose
```
version: "3.8"

services:
  gpt4all_api:
    image: thanhtung100397/gpt4all_api:latest
    container_name: gpt4all_api
    restart: always #restart on error (usually code compilation from save during bad state)
    ports:
      - "4891:4891"
    env_file:
      - .env
    environment:
      - APP_ENVIRONMENT=dev
      - WEB_CONCURRENCY=2
      - LOGLEVEL=debug
      - PORT=4891
      - model=${MODEL_BIN} # using variable from .env file
      - inference_mode=cpu
    volumes:
      - './gpt4all_api/app:/app'
      - './gpt4all_api/models:/models' # models are mounted in the container
    command: ["/start-reload.sh"]
```

.env
```
# Add your GGUF compatible model LLM here. ie: MODEL_BIN="mistral-7b-instruct-v0.1.Q4_0", rename file ".env"
# Make sure this LLM matches the model you placed inside the models folder
MODEL_BIN="gpt4all-falcon-q4_0.gguf"
```
