# for build stage
FROM node:16-slim AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . ./

RUN npm run build

# For production environment
FROM nginx:stable AS prod

LABEL maintainer="Piscki F. Pratama <pisckipratama@gmail.com>"

## setup container
WORKDIR /app
ENV TZ=Asia/Jakarta

## copy configuration and html
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

## startup container
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]