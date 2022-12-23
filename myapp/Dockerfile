#stage 1
FROM node:latest as node
WORKDIR /app
COPY . /app
ENV TOOL_NODE_FLAGS "--max-old-space-size=4096 --optimize_for_size --gc-interval=100"
RUN npm install --force 
RUN npm run build --prod
RUN ls /app/build
#stage 2
#FROM nginx:alpine
FROM httpd:2.4
COPY --from=node /app/.htaccess /usr/local/apache2
COPY --from=node /app/build /usr/local/apache2/htdocs/
