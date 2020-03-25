# Use the official Python image.
# https://hub.docker.com/_/python
FROM python:3.8.1-slim-buster

# Copy local code to the container image.
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY . ./

# Install production dependencies.
RUN apt-get update \
 && apt-get install -y gcc default-libmysqlclient-dev \
 && pip install -r requirements.txt \
 && pip install flask gunicorn

# Run the web service on container startup. Here we use the gunicorn
# webserver, with one worker process and 8 threads.
# For environments with multiple CPU cores, increase the number of workers
# to be equal to the cores available.
CMD exec gunicorn --bind :8080 --workers 1 --threads 8 main:app
