# Builder stage
FROM node:18-alpine AS builder
WORKDIR /usr/src/app
COPY package.json ./
COPY yarn.lock ./
RUN yarn install
COPY . .
RUN yarn run build

# Runtime stage
FROM nginx:stable-bullseye
COPY --from=builder /usr/src/app/build /usr/share/nginx/html 
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
