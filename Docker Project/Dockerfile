## BUILD PHASE
# Base image
FROM node:alpine as builder

# Switch workdir to '/usr/app'
WORKDIR '/usr/app'

# Copy package.json into the container
COPY ./package.json .

# Install all the deps
RUN npm install

# Copy the rest of the files into the container
COPY . .

# Build the production files
CMD ["npm", "run", "build"]

## RUN PHASE
# Base image
FROM node:alpine

# Switch workdir to '/usr/app'
WORKDIR '/usr/app'

# Copy package.json into the container
COPY package.json ./

# Install all the deps
RUN npm install

# Copy over the production files to the nginx webroot
COPY --from=builder /usr/app/dist .

# Run server
CMD ["node", "server.js"]