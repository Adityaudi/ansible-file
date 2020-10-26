FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

ENV VUE_APP_URL='http://184.72.88.25/product'
ENV VUE_APP_URL_HISTORY='http://184.72.88.25/history'
ENV VUE_APP_URL_USERS='http://184.72.88.25/users'
ENV VUE_APP_URL_AUTH='http://184.72.88.25/auth'

RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf

COPY ssl/cert.pem /etc/ssl/certs/cert.pem
COPY ssl/cert.key /etc/ssl/private/cert.key 

COPY --from=build-stage /app/dist /dist/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
