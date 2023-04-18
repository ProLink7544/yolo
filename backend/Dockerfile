FROM node:13.12.0-alpine

RUN mkdir /backend

WORKDIR /backend

COPY . .

RUN npm install

EXPOSE 5000

CMD ["npm","start"]