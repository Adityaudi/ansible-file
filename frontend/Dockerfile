FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf

ENV VUE_APP_URL='http://3.92.189.20/product'
ENV VUE_APP_URL_HISTORY='http://3.92.189.20/history'
ENV VUE_APP_URL_USERS='http://3.92.189.20/users'
ENV VUE_APP_URL_AUTH='http://3.92.189.20/auth'

COPY --from=build-stage /app/dist /dist/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
