FROM ubuntu:12.04

MAINTAINER Diego Gabriel <marcondesdddi@gmail.com>

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y vim git

# Supervisor
RUN apt-get install -y supervisor git
RUN mkdir -p /var/log/supervisor
ADD supervisor/supervisor.conf /etc/supervisor/conf.d/supervisor.conf

# Install sshd
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
ADD ssh/sshd.conf /etc/supervisor/conf.d/sshd.conf

# Set password to 'admin'
RUN printf admin\\nadmin\\n | passwd

# Apache
RUN apt-get install -y apache2
ADD apache/apache2-service.sh /apache2-service.sh
RUN chmod +x /*.sh
ADD apache/apache_default /etc/apache2/sites-available/
ADD apache/apache2.conf /etc/supervisor/conf.d/apache2.conf
# Enable mod_rewrite
RUN a2enmod rewrite

# Install MySQL
RUN apt-get install -y mysql-server mysql-client libmysqlclient-dev php5-mysql
RUN chmod +x /*.sh
ADD mysql/my.cnf /etc/mysql/conf.d/my.cnf
ADD mysql/mysql.conf /etc/supervisor/conf.d/mysql.conf

# Install php
RUN apt-get install -y libapache2-mod-php5 php5 php5-json php5-cli php5-curl curl php5-mcrypt php5-xdebug mcrypt libmcrypt-dev rsync wget
# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/bin --version=1.0.0-alpha8

# Install phpMyAdmin
RUN mysqld & \
	service apache2 start; \
	sleep 5; \
	printf y\\n\\n\\n1\\n | apt-get install -y phpmyadmin; \
	sleep 15; \
	mysqladmin -u root shutdown

RUN sed -i "s#// \$cfg\['Servers'\]\[\$i\]\['AllowNoPassword'\] = TRUE;#\$cfg\['Servers'\]\[\$i\]\['AllowNoPassword'\] = TRUE;#g" /etc/phpmyadmin/config.inc.php 

EXPOSE 22
EXPOSE 80
EXPOSE 3306

VOLUME ["/var/www"]

CMD ["mysqld_safe"]
CMD ["service apache2", "start"]
CMD ["/usr/bin/supervisord", "-n"]
