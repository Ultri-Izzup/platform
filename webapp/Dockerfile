# Use Node v18
FROM node:18 as base

# Create API app directory in container
WORKDIR /usr/src/webapp

FROM base as prereq

# Install global NPM packages
RUN npm install npm@latest @quasar/cli -g

# Copy the api specific package info to the Docker image
COPY package*.json ./
COPY quasar.config.js ./
COPY postcss.config.js ./
COPY jsconfig.json ./
COPY index.html ./
COPY .npmrc ./
COPY .gitignore ./
COPY .eslintrc.js ./
COPY .eslintignore ./
COPY .editorconfig ./

# Run npm install on the image
RUN npm install --quiet --unsafe-perm --no-progress --no-audit --only=production

FROM prereq as development

RUN npm install --quiet --unsafe-perm --no-progress --no-audit --only=development

# Expose the default Quasar port, 9000.
EXPOSE 9000

# We start Quasar dev from the docker-compose file.
# We volume map the Quasar app files in the docker-compose file.
