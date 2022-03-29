# ----
FROM node:16-alpine3.15 AS BUILD_IMAGE

WORKDIR /usr/src/build-app

RUN apk add --no-cache git=2.34.1-r0

RUN git clone https://github.com/BitCannaCommunity/cosmos-faucet.git . && \
    git reset --hard cc2fad2d1a2d1e2aea6d9fcf30311af864704d7a && \
    npm install

# ----
FROM node:16-alpine3.15

WORKDIR /usr/src/app

COPY --from=BUILD_IMAGE /usr/src/build-app/ ./

EXPOSE 8000

CMD ["node", "--experimental-modules", "--es-module-specifier-resolution=node", "app.js"]
