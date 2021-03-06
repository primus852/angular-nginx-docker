#############
### build ###
#############

# base image
FROM node:12.8.1 as build

# install chrome for protractor tests
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -yq google-chrome-stable bash

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY apps/frontend/package.json /app/package.json
RUN npm install
RUN npm install -g @angular/cli

# add app
COPY apps/frontend /app

# run tests
# RUN ng test --watch=false --browsers=ChromeHeadlessNoSandbox
# RUN ng e2e --port 4202

# generate build
RUN ng build --output-path=dist --prod=true

############
### prod ###
############

# base image
FROM nginx:1.19.6-alpine

# copy artifact build from the 'build environment'
COPY --from=build /app/dist /usr/share/nginx/html

RUN chown nginx:nginx /usr/share/nginx/html/*

# expose port 80
EXPOSE 80

# run nginx
CMD ["nginx", "-g", "daemon off;"]
