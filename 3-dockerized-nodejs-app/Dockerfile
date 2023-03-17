FROM node:16-alpine

LABEL maintainer="Piscki F. Pratama <pisckipratama@gmail.com>"

WORKDIR /app
RUN chown node:node /app

# define ENV
RUN apk update && apk add tzdata --no-cache
ENV TZ=Asia/Jakarta
ENV NODE_ENV=production

# Build Application
COPY package*.json ./
RUN npm install
COPY --chown=node:node . ./

# setup container
USER node
EXPOSE 3000
CMD [ "node", "./bin/www" ]
