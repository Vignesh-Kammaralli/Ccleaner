#stage 1
FROM node:latest as node
WORKDIR /app
COPY . /app
RUN npm install --force 
RUN npm run build -g increase-memory-limit
#stage 2
FROM nginx:alpine
COPY --from=node /app/dist/myapp /usr/share/nginx/html
