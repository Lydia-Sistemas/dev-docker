ARG NODE_VERSION=18.14.2
ARG NODE_APP_DIR= ""
FROM node:${NODE_VERSION}-alpine

RUN npm install -g npm@latest

COPY ./start.sh /start.sh

RUN chmod -x /start.sh

CMD [ "tail", "-f", "/dev/null" ]

EXPOSE 3000