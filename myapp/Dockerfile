#stage 1
FROM node:latest as node
WORKDIR /app
COPY . /app
RUN npm install --force 
ENV TOOL_NODE_FLAGS "--max-old-space-size=4096 --optimize_for_size --gc-interval=100"
RUN npm run build 
#stage 2
FROM nginx:alpine
COPY --from=node /app/dist/myapp /usr/share/nginx/html
