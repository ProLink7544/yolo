#Build stage
FROM node:16-alpine3.16 as build-stage

WORKDIR /client

COPY package*.json ./

RUN npm install --only=production && \
    npm cache clean --force && \
    rm -rf /tmp/*

COPY . .

RUN npm run build && \
    npm prune --production

# Production stage

FROM node:alpine3.16 as production-stage

WORKDIR /client

COPY --from=build-stage /client/build ./build
COPY --from=build-stage /client/public ./public
COPY --from=build-stage /client/src ./src
COPY --from=build-stage /client/package*.json ./

ENV NODE_ENV=production

EXPOSE 3000

RUN npm prune --production && \
    npm cache clean --force && \
    rm -rf /tmp/*

CMD ["npm","start"]