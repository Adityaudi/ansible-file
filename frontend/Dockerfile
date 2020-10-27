FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

ENV VUE_APP_URL='http://3.238.16.39:31805/product'
ENV VUE_APP_URL_HISTORY='http://3.238.16.39:31805/history'
ENV VUE_APP_URL_USERS='http://3.238.16.39:31805/users'
ENV VUE_APP_URL_AUTH='http://3.238.16.39:31805/auth'

RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf

COPY ssl/cert.pem /etc/ssl/certs/cert.pem
COPY ssl/cert.key /etc/ssl/private/cert.key 

COPY --from=build-stage /app/dist /dist/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
