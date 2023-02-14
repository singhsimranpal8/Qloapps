FROM ubuntu:20.04
ARG DEBIAN_FRONTEND=noninteractive
WORKDIR /var/www/html
RUN apt-get update && apt install apache2 curl -y && apt -y install software-properties-common && add-apt-repository ppa:ondrej/php && apt-get update && apt -y install php8.1 && apt-get install -y php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath libapache2-mod-php8.1 php8.1-intl php8.1-soap libmcrypt-dev && a2enmod php8.1 && a2enmod rewrite
RUN apt install php8.1-cli unzip -y 
COPY qloapp.conf /etc/apache2/sites-available/
RUN a2ensite qloapp.conf
RUN apt-get update -y && apt-get install software-properties-common supervisor git -y
RUN sed -i 's/memory_limit = 128M/memory_limit = 256M/g' /etc/php/8.1/apache2/php.ini && sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 100M/g' /etc/php/8.1/apache2/php.ini && sed -i 's/max_execution_time = 30/max_execution_time = 360/g' /etc/php/8.1/apache2/php.ini && rm -rf /etc/apache2/sites-available/000-default.conf && rm -rf /etc/apache2/sites-available/default-ssl.conf && rm -f /etc/apache2/sites-enabled/000-default.conf
RUN git clone -b v1.5.2 https://github.com/webkul/hotelcommerce
COPY supervisor.conf /etc/supervisor/conf.d/
RUN chown -R www-data:www-data /var/www/html/
EXPOSE 80
ENTRYPOINT ["/usr/bin/supervisord"]
