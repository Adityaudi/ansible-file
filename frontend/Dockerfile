FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/nginx.conf

COPY cert.key /etc/ssl/certs/cert.pem
COPY cert.pem /etc/ssl/private/cert.key 

COPY --from=build-stage /app/dist /dist/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
