FROM ubuntu:14.04
MAINTAINER Javier Jerónimo <javier@jeronimosuarez.es>

VOLUME ["/var/www/owncloud/data","/var/log/apache2"]

# Apache2
RUN apt-get update
RUN apt-get install -y apache2

# PHP and other owncloud dependencies
RUN apt-get install -y php5 php5-gd php-xml-parser php5-intl php5-sqlite php5-mysql
RUN apt-get install -y smbclient curl libcurl3 php5-curl bzip2 wget vim

# owncloud from tar.bz2
RUN wget -O - http://download.owncloud.org/community/owncloud-5.0.16.tar.bz2 | tar jx -C /var/www/
RUN chown -R www-data:www-data /var/www/owncloud

# Apache sites and modules
ADD ./resources/owncloud.conf /etc/apache2/sites-available/owncloud.conf
RUN a2ensite owncloud
RUN a2enmod rewrite

# Environment to run Apache from executable (foreground)
ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

EXPOSE 80 443

# Moved to Vagrantfile
# CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
