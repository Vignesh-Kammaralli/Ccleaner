#stage 1
FROM node:latest as node
WORKDIR /app
COPY . /app
ENV TOOL_NODE_FLAGS "--max-old-space-size=4096 --optimize_for_size --gc-interval=100"
RUN npm install --force 
RUN npm install -g npm@9.2.0
RUN npm run build --prod
#stage 2
FROM nginx:alpine
COPY --from=node /app/dist/myapp /usr/share/nginx/html
