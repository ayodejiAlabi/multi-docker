# Use an existing docker image as base
FROM node:alpine AS builder
#Specify Work Directory to copy files to in the docker container
WORKDIR /usr/applications/clientjs
# Copy only selected the file in the current directory to the docker container
COPY ./package.json ./
# Download and install a dependency
RUN npm install
# Copy all the files in the current directory to the docker container
COPY ./ ./
# build the application directory for production
RUN npm run build

#2nd step to create production enviroment using nginx as web server
# Use an existing docker image as base
FROM nginx
EXPOSE 3000
#copy build file from builder container to the production enviroment
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /usr/applications/clientjs/build /usr/share/nginx/html
