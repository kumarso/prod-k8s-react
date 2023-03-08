FROM node:16-alpine AS builder

WORKDIR '/app'

COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
# copy from different phase
# /usr/share/ngnix/html by default servers the content in nginx
COPY ./nginx/default.conf /etc//nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
# default command of nginx image is start nginx so no need t0 start ngnix