An example app that shows how to build a ML app with FastAPI and Docker.

The starter file is [model.py](model.py) with a model from Hugging Face: https://huggingface.co/dandelin/vilt-b32-finetuned-vqa
Further this file is modified into the file containing the function for calling the pipeline

The final app is in [main.py](main.py) and final model code is in [model.py](model.py).

Below are the steps to use Docker:

## Steps to Setup Docker and VS Code

STEP: Run `docker init`

```
docker init
```

STEP: Select Python image and use this command during docker init
```
CMD uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

STEP: Remove `-slim` and add this to Dockerfile (Needed to install transformers)

```
# Install Rust compiler
RUN curl https://sh.rustup.rs -sSf | bash -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"
```

STEP: Remove the custom user from the Dockerfile to simplify, because HF needs write permissions to download and save the model.

STEP: Add volume to `compose.yaml`:

```
    volumes:
      - .:/app
```

STEP Run `docker compose up --build`

STEP: Attach VS Code to running container

## Examples

- file: dogs.jpg
  
  text: How many dogs are there?

- file: car.jpg

  text: What is the car doing?

- file: elephants.jpg

  text: What are the elephants doing ?