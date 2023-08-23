FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    software-properties-common \
    nginx \
    composer \
    curl \
    nano \
    php8.1-fpm php8.1-bcmath php8.1-cli php8.1-common php8.1-curl php8.1-dev \
    php8.1-fpm php8.1-gd php8.1-imagick php8.1-mbstring php8.1-memcache \
    php8.1-opcache php8.1-pgsql php8.1-pspell php8.1-readline php8.1-snmp \
    php8.1-sqlite3 php8.1-ssh2 php8.1-xml php8.1-xmlrpc php8.1-xsl php8.1-zip \
    python3 python3-pip \
    npm

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require laravel/installer


# Install Python dependencies from requirements.txt
RUN pip3 install -r /var/www/html/python/requirements.txt


# Copy Nginx configuration file
COPY ./default /etc/nginx/sites-enabled/default

# Copy application files to appropriate directories
COPY laravel /var/www/html/laravel
COPY vue/myapp /var/www/html/vue
COPY node /var/www/html/node
COPY python /var/www/html/python

# Expose port 80
EXPOSE 80

# Start Nginx and other services
#CMD service php7.4-fpm start && nginx -g "daemon off;"


CMD ["sh", "-c", "service php7.4-fpm start & cd /var/www/html/node & npm install & node /var/www/html/node/index.js & python3 /var/www/html/python/app.py &  cd /var/www/html/vue/myapp & npm install & npm run serve  & nginx -g 'daemon off;'"]
#CMD ["sh", "-c", "service php7.4-fpm start & cd /var/www/html/node & npm install & node /var/www/html/node/index.js & python3 /var/www/html/python/app.py &  cd /var/www/html/vue/myapp & npm install & npm run serve & npm run build  & nginx -g 'daemon off;'"]

#CMD service php7.4-fpm start & \
 #   cd /var/www/html/node & npm install & node /var/www/html/node/index.js & \
  #  python3 /var/www/html/python/app.py & \
   # cd /var/www/html/vue/myapp & npm install & npm run serve & \
    #nginx -g 'daemon off;'
