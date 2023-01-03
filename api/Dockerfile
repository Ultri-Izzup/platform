# Use Node v18
FROM node:18 as base

# Create API app directory in container
WORKDIR /usr/src/api

FROM base as prereq

# Install global NPM packages
RUN npm install npm@latest fastify-cli -g

# Copy the api specific package info to the Docker image
COPY package*.json ./

# Run npm install on the image
RUN npm install --quiet --unsafe-perm --no-progress --no-audit --only=production

FROM prereq as development

RUN npm install --quiet --unsafe-perm --no-progress --no-audit --only=development

# Expose the default Fastify port, 3000.
EXPOSE 3000

# We start Fastify from the docker-compose file.
# We volume map the API app files for Fastify in the docker-compose file.
