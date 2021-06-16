FROM httpd:2.4.29-alpine
RUN apk update; \
    apk upgrade;
RUN echo "Include /usr/local/apache2/conf/webapp.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf
