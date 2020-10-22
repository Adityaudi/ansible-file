FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

ENV VUE_APP_URL='http://18.234.201.208/product'
ENV VUE_APP_URL_HISTORY='http://18.234.201.208/history'
ENV VUE_APP_URL_USERS='http://18.234.201.208/users'
ENV VUE_APP_URL_AUTH='http://18.234.201.208/auth'

RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build-stage /app/dist /dist/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
