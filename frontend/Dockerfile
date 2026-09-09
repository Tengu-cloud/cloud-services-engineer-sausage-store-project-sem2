# build
FROM node:14.21-alpine AS builder
RUN apk add --no-cache python3 make g++ \
    && ln -sf python3 /usr/bin/python
WORKDIR /usr/src/app
COPY package.json package-lock.json ./
RUN npm install --legacy-peer-deps
COPY . .
RUN npm run build -- --prod

# release
FROM nginx:1.21.6-alpine
COPY --from=builder /usr/src/app/dist/frontend /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
