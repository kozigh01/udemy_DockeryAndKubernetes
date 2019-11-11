# the first phase
FROM node:alpine as builder

WORKDIR /app

COPY ./package.json .
RUN npm install

COPY . .
RUN npm run build


# the second phase
FROM nginx
COPY --from=builder /app/build /usr/share/nginx/html
# default command for nginx image is to strat nginx

