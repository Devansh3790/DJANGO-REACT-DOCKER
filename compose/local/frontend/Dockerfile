# base image
FROM node:11.4.0-alpine

RUN apk update \
  && apk add --no-cache bash

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY ./frontend/package.json \
    ./frontend/package-lock.json /app/
RUN npm install --silent
RUN npm install react-scripts@3.0.1  --silent --prefix /app

# Copy app files.
COPY ./frontend/ /app

# start app
COPY ./compose/local/frontend/start /start
RUN sed -i 's/\r//' /start
RUN chmod +x /start

# set working directory
WORKDIR /app