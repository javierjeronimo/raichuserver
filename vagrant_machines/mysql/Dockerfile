FROM ubuntu:trusty
MAINTAINER Fernando Mayo <fernando@tutum.co>, Feng Honglin <hfeng@tutum.co>

# Install packages
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server pwgen

# Remove pre-installed database
RUN rm -rf /var/lib/mysql/*

# Add MySQL configuration
ADD vendor/tutum-docker-mysql/my.cnf /etc/mysql/conf.d/my.cnf
ADD vendor/tutum-docker-mysql/mysqld_charset.cnf /etc/mysql/conf.d/mysqld_charset.cnf

# Add MySQL scripts
ADD vendor/tutum-docker-mysql/create_mysql_admin_user.sh /create_mysql_admin_user.sh
ADD vendor/tutum-docker-mysql/import_sql.sh /import_sql.sh
ADD vendor/tutum-docker-mysql/run.sh /run.sh
RUN chmod 755 /*.sh

# Add VOLUMEs to allow backup of config and databases
VOLUME  ["/var/lib/mysql"]

EXPOSE 3306

CMD ["/run.sh"]
