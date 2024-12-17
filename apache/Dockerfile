FROM httpd:2.4

COPY ./httpd.conf /usr/local/apache2/conf/extra/apache.vhost.conf

# Activer les modules proxy et proxy_fcgi
RUN sed -i \
    -e '/#LoadModule proxy_module/s/^#//g' \
    -e '/#LoadModule proxy_fcgi_module/s/^#//g' \
    /usr/local/apache2/conf/httpd.conf

RUN echo "Include /usr/local/apache2/conf/extra/apache.vhost.conf" >> /usr/local/apache2/conf/httpd.conf