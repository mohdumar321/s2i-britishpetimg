FROM centos/s2i-base-centos7


MAINTAINER atos india private ltd
EXPOSE 8000
ENV PHP_VERSION=5.6 \
PATH=$PATH:/opt/rh/rh-php56/root/usr/bin
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm


RUN curl 'https://setup.ius.io/' -o setup-ius.sh && \
bash setup-ius.sh
RUN yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus \
php56-fpm nginx  
RUN yum -y install php56w \
php-adodb \
php56w-opcache \
php56w-common \ 
php56w-json \
php56w-dba \
php56w-fpm \
php56w-cli \
nginx \
php56w-devel \
php56w-gd \
php56w-mbstring \
php56w-ldap \
php56w-odbc \
php56w-intl \
php56w-pdo \
php56w-phpdbg \
php56w-pear \
php56w-xml \
php56w- soap \
php56w-fpm-nginx \
libaio

RUN yum clean all -y
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

COPY ./contrib/ /opt/app-root
RUN cp /opt/app-root/etc/conf.d/php-fpm/pool.conf /etc/php-fpm.d/www.conf
RUN cp /opt/app-root/etc/conf.d/php-fpm/fpm.conf /etc/php-fpm.conf
RUN cp /opt/app-root/etc/conf.d/php-fpm/pools/rosi.conf /etc/php-fpm.d/rosi.conf
RUN cp /opt/app-root/etc/conf.d/php-fpm/pools/rosi-webservice.conf /etc/php-fpm.d/rosi-webservice.conf
RUN cp /opt/app-root/etc/conf.d/php-fpm/pools/cacti.conf /etc/php-fpm.d/cacti.conf
RUN cp /opt/app-root/etc/conf.d/php-fpm/pools/lm.conf /etc/php-fpm.d/lm.conf


RUN cp /opt/app-root/etc/conf.d/php/php.ini /etc/php.d/php.ini
RUN cp /opt/app-root/etc/conf.d/php/php-batch.ini /etc/php.d/php-batch.ini
RUN cp /opt/app-root/etc/conf.d/php/oci8.ini /etc/php.d/30-oci8.ini
RUN mkdir /tmp/sessions && \
mkdir -p /var/lib/nginx && \
mkdir -p /var/log/nginx && \
touch /var/log/nginx/error.log && \
touch /var/log/nginx/access.log && \
chown -R 1001:0 /var/log/nginx && \
chown -R 1001:0 /var/lib/nginx && \
chown -R 1001:0 /opt/app-root /tmp/sessions && \
chmod -R a+rwx /tmp/sessions && \
chmod -R a+rwx /var/log/nginx && \
chmod -R a+rwx /var/lib/nginx && \
chmod -R ug+rwx /var/log/nginx && \
chmod -R ug+rwx /var/lib/nginx && \
chmod -R ug+rwx /opt/app-root && \
#chmod -R a+rwx /opt/app-root/services.sh \
#chmod -R a+rwx /opt/app-root
chmod -R a+rwx /opt/app-root/services.sh


# -----------------------------------------------------------------------------
# Install Oracle drivers
#
# Oracle clients need to be downloaded in oracle path
# -----------------------------------------------------------------------------
#RUN mkdir -p /opt/app-root/etc/oracle/11.2/client64/lib/
#RUN cp /opt/app-root/etc/conf.d/oracle/libclntsh.so.11.1.gz /opt/app-root/etc/oracle/11.2/client64/lib/
#RUN gunzip /opt/app-root/etc/oracle/11.2/client64/lib/libclntsh.so.11.1.gz
#RUN cp /opt/app-root/etc/conf.d/oracle/libnnz11.so.gz /opt/app-root/etc/oracle/11.2/client64/lib/
#RUN gunzip /opt/app-root/etc/oracle/11.2/client64/lib/libnnz11.so.gz
#RUN cp /opt/app-root/etc/conf.d/oracle/libocci.so.11.1.gz /opt/app-root/etc/oracle/11.2/client64/lib/
#RUN gunzip /opt/app-root/etc/oracle/11.2/client64/lib/libocci.so.11.1.gz
#RUN ln -s /opt/app-root/etc/oracle/11.2/client64/lib/libclntsh.so.11.1 /opt/app-root/etc/oracle/11.2/client64/lib/libclntsh.so
#RUN ln -s /opt/app-root/etc/oracle/11.2/client64/lib/libocci.so.11.1 /opt/app-root/etc/oracle/11.2/client64/lib/libocci.so
#RUN echo "/opt/app-root/etc/oracle/11.2/client64/lib" > /etc/ld.so.conf.d/oracle.conf
#RUN ldconfig

#RUN cp /opt/app-root/etc/conf.d/oracle/oci8.so /etc/php-fpm.conf
#RUN echo "extension=oci8.so" > /etc/php-fpm.d/oci8.ini

#RUN cp /opt/app-root/etc/conf.d/oracle/pdo_oci.so /etc/php-fpm.conf
#RUN echo "extension=pdo_oci.so" > /etc/php-fpm.d/pdo_oci.ini

# Oracle instantclient
RUN cp /opt/app-root/etc/conf.d/oracle/instantclient-basic-linux.x64-11.2.0.4.0.zip /usr/local/instantclient-basic-linux.x64-11.2.0.4.0.zip
RUN cp /opt/app-root/etc/conf.d/oracle/instantclient-sdk-linux.x64-11.2.0.4.0.zip /usr/local/instantclient-sdk-linux.x64-11.2.0.4.0.zip
RUN cp /opt/app-root/etc/conf.d/oracle/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip /usr/local/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip

RUN yum install -y unzip
#mkdir -p /etc/local /etc/bin
RUN unzip /usr/local/instantclient-basic-linux.x64-11.2.0.4.0.zip -d /usr/local
RUN unzip /usr/local/instantclient-sdk-linux.x64-11.2.0.4.0.zip -d /usr/local
RUN unzip /usr/local/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip -d /usr/local
RUN ln -s /usr/local/instantclient_11_2 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.11.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus


RUN echo 'instantclient,/usr/local/instantclient' | pecl install -f oci8-2.0.11

RUN echo 'extension=oci8.so' > /etc/php.ini

RUN yum clean all -y
USER 1001
CMD $STI_SCRIPTS_PATH/usage
