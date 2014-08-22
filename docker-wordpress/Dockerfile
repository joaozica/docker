FROM lamp-full
MAINTAINER Diego Gabriel <marcondesdddi@gmail.com>

# Create app/ folder
RUN mkdir -p /app

# Download latest version of Wordpress into /app
RUN rm -fr /app && git clone --depth=1 https://github.com/WordPress/WordPress.git /app

# Configure Wordpress to connect to local DB
ADD wp-config.php /app/wp-config.php

# Modify permissions to allow plugin upload
RUN chmod -R 777 /app/wp-content

# Add database setup script
ADD create_mysql_admin_user.sh /create_mysql_admin_user.sh
ADD create_db.sh /create_db.sh
ADD run.sh /run.sh
RUN chmod 755 /*.sh

# Configure to enable .htaccess
ADD wordpress.conf /etc/apache2/sites-available/apache_default
RUN ln -s /etc/apache2/sites-available/apache_default /etc/apache2/sites-enabled/
RUN a2enmod rewrite

EXPOSE 80 3306 22
CMD ["/run.sh"]
