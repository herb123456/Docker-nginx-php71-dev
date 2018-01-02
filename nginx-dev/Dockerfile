
FROM centos:7
LABEL Name="nginx-dev" Version=0.0.1 maintainer="Herb <herb123456@gmail.com>"

# update yum base repo to hinet
RUN mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.back
ADD config/yum/CentOS-Base.repo /etc/yum.repos.d/

# install nginx
ADD config/yum/nginx.repo /etc/yum.repos.d/
RUN yum -y update && yum -y install epel-release wget
RUN yum -y install nginx

# Add nginx user and group
# RUN 

# copy nginx config
ADD config/nginx/nginx.conf /etc/nginx/

RUN mkdir -p /etc/nginx/sites-available \
 && mkdir -p /etc/nginx/sites-enabled
ADD config/nginx/sites-available/index.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/index.conf /etc/nginx/sites-enabled/index.conf
RUN mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.back

# copy xhgui config
ADD config/nginx/sites-available/xhgui.conf /etc/nginx/sites-available
RUN ln -s /etc/nginx/sites-available/xhgui.conf /etc/nginx/sites-enabled/xhgui.conf

# copy info.php
# RUN mkdir -p /var/www/html
# ADD info.php /var/www/html/

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log
    
EXPOSE 80

# install remi repo
# RUN wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm -O /remi-release-7.rpm
# RUN rpm -Uvh /remi-release-7.rpm

# RUN yum-config-manager --enable remi-php71
# RUN yum -y update

# # Add oracle client
# RUN yum -y install libaio-0.3.109-13.el7.x86_64
# ADD oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm /
# RUN rpm -Uvh /oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm

# # add ldconfig
# ADD config/php-fpm/oci8_ld.conf /etc/ld.so.conf.d
# RUN ldconfig

# # install php71
# RUN yum -y install php71 \
#                    php71-php-cli.x86_64 \
#                    php71-php-common.x86_64  \
#                    php71-php-fpm.x86_64  \
#                    php71-php-gd.x86_64 \
#                    php71-php-intl.x86_64 \
#                    php71-php-json.x86_64 \
#                    php71-php-mbstring.x86_64 \
#                    php71-php-mcrypt.x86_64 \
#                    php71-php-mysqlnd.x86_64 \
#                    php71-php-pdo.x86_64 \
#                    php71-php-pear.noarch \
#                    php71-php-pecl-apcu.x86_64 \
#                    php71-php-pecl-igbinary.x86_64 \
#                    php71-php-pecl-memcache.x86_64 \
#                    php71-php-pecl-memcached.x86_64 \
#                    php71-php-pecl-mongodb.x86_64 \
#                    php71-php-pecl-redis.x86_64 \
#                    php71-php-pecl-yaml.x86_64 \
#                    php71-php-soap.x86_64 \
#                    php71-php-tidy.x86_64 \
#                    php71-php-xml.x86_64 \
#                    php71-php-xmlrpc.x86_64 \
#                    php71-php-pecl-zip.x86_64 \
#                    php71-zephir.noarch \
#                    php71-php-phalcon3.x86_64 \
#                    php71-php-pgsql.x86_64 \
#                    php71-php-phpiredis.x86_64 \
#                    php71-php-pecl-varnish.x86_64 \
#                    php71-php-pecl-xdebug.x86_64 \
#                    php71-php-pecl-redis.x86_64 \
#                    php71-php-pecl-mongodb.x86_64 \
#                    php71-php-pecl-memcached.x86_64 \
#                    php71-php-pecl-memcache.x86_64 \
#                    php71-php-pecl-gearman.x86_64 \
#                    php71-php-pecl-couchbase2.x86_64 \
#                    php71-php-oci8.x86_64 \
#                    php71-php-pecl-apcu.x86_64 \
#                    php71-php-bcmath.x86_64 \
#                    php71-php-devel.x86_64

# RUN source /opt/remi/php71/enable \
#     && php -v

# # install composer
# RUN /opt/remi/php71/root/bin/php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# RUN /opt/remi/php71/root/bin/php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
# RUN /opt/remi/php71/root/bin/php composer-setup.php --install-dir=/usr/bin --filename=composer
# RUN /opt/remi/php71/root/bin/php -r "unlink('composer-setup.php');"

# # copy php-fpm config
# ADD config/php-fpm/php-fpm.conf /etc/opt/remi/php71/
# ADD config/php-fpm/php-fpm.d/www.conf /etc/opt/remi/php71/php-fpm.d/

# # install xhprof
# RUN yum -y install git gcc g++ file-5.11-33.el7.x86_64
# RUN git clone https://github.com/longxinH/xhprof.git /xhprof
# RUN cd /xhprof/extension \
#     && /opt/remi/php71/root/usr/bin/phpize \
#     && ./configure --with-php-config=/opt/remi/php71/root/usr/bin/php-config \
#     && make \
#     && make install
# ADD config/php-fpm/20-xhprof.ini /etc/opt/remi/php71/php.d

# # install xhgui
# RUN yum install -y mongodb-server openssl-devel
# RUN mkdir -p /data/mongodb
# RUN git clone https://github.com/perftools/xhgui.git /var/www/xhgui
# RUN source /opt/remi/php71/enable \
#     && cd /var/www/xhgui \
#     && composer install \
#     && chmod 0777 cache
# ADD config/xhgui/config.php /var/www/xhgui/config
# RUN chown -R nginx:nginx /var/www/xhgui
# ADD config/nginx/sites-available/xhgui.conf /etc/nginx/sites-available
# RUN ln -s /etc/nginx/sites-available/xhgui.conf /etc/nginx/sites-enabled/xhgui.conf

# Installing supervisor
RUN yum install -y python-setuptools
RUN easy_install pip
RUN pip install supervisor
# Adding the configuration file of the Supervisor
ADD config/supervisord/supervisord.conf /etc/

CMD ["nginx", "-g", "daemon off;"]
# RUN apt-get -y update && apt-get install -y fortunes
# CMD /usr/games/fortune -a | cowsay

# Executing supervisord
# CMD ["supervisord", "-n"]