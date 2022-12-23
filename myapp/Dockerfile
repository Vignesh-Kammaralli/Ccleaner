#stage 1
FROM node:latest as node
WORKDIR /app
COPY . /app
ENV TOOL_NODE_FLAGS "--max-old-space-size=4096 --optimize_for_size --gc-interval=100"
RUN npm install --force 
RUN npm run build --prod

#stage 2
#FROM nginx:alpine
FROM httpd:2.4
RUN chown www-data:www-data /usr/local/apache2
COPY --from=node /app/.htaccess /usr/local/apache2/htdocs/
COPY --from=node /app/build /usr/local/apache2/htdocs/
RUN rm /usr/local/apache2/conf/httpd.conf
COPY --from=node /app/httpd.conf /usr/local/apache2/conf/
#RUN sed -i '/<Directory \/usr\/local\/apache2\/htdocs\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /usr/local/apache2/conf/httpd.conf
#RUN sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf
RUN cat /usr/local/apache2/conf/httpd.conf