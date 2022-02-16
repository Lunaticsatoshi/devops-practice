FROM node:16-alpine

WORKDIR /app/

COPY ./test/package.json ./package.json

COPY ./test/package-lock.json ./package-lock.json

RUN npm ci

COPY ./test ./

RUN NODE_OPTIONS=--max_old_space_size=4096 npm run build

FROM nginx:alpine

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY --from=0 /app/build /nginx/html