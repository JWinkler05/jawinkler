FROM ubuntu:16.04
# MAINTAINER John Winkler <JWinkler05@gmail.com>
# Utilized code from Atymchuk, check his file out @ www.github.com/atymchuk/joomla-lamp/

ENV DEBIAN_FRONTEND noninteractive
ENV JOOMLA_VERSION 3.5.1
ENV JOOMLA_ARCHIVE Joomla_3.5.1-Stable-Full_Package.tar.gz

# makes nano or vim run without error
ENV TERM xterm
ENV TIMEZONE America/New_York

RUN apt-get -y update

RUN echo $TIMEZONE > /etc/timezone
RUN dpkg-reconfigure tzdata

RUN apt-get -y update
RUN apt-get -y install apache2
RUN apt-get install -y nano
RUN apt-get install -y wget
RUN apt-get install -y curl
RUN apt-get install -y php7.0
RUN apt-get install -y libapache2-mod-php7.0
RUN apt-get install -y php7.0-cli
RUN apt-get install -y php7.0-common
RUN apt-get install -y php7.0-mysql
RUN apt-get install -y php7.0-mcrypt
RUN apt-get install -y php7.0-json
RUN apt-get install -y php7.0-curl
RUN apt-get install -y php-pear
RUN pecl install channel://pecl.php.net/ssh2-1.0

# mysql-server \

# Download joomla and put it in the default apache web root
RUN rm -rf /var/www/html && mkdir -p /var/www/html
RUN wget https://github.com/joomla/joomla-cms/releases/download/$JOOMLA_VERSION/$JOOMLA_ARCHIVE -O - | tar -zxf - -C /var/www/html

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Give the ownership to the apache2 user
RUN chown -R www-data:www-data /var/www

# Note: expires is for caching
RUN a2enmod rewrite headers expires ssl proxy proxy_http > /dev/null

# Put default htaccess in place
RUN mv /var/www/html/htaccess.txt /var/www/html/.htaccess

# Export the ports
EXPOSE 80 443

# Use supervisord to start apache / mysql
# COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/bin/bash", "-c", "source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOREGROUND"]
