FROM amazonlinux:2018.03

#Comments
#   groupinstall "Development Tools" is necessary for xdebug

# update amazon software repo
RUN yum -y update && yum -y install shadow-utils yum-utils\
    && yum-config-manager --enable remi-php56 && yum -y update

#configure time zone
RUN ln -f -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

#Intall utilites
RUN yum -y install vim wget git && yum -y groupinstall "Development Tools"

#Install apache
RUN yum install -y httpd24 httpd24-tools mod24_ssl
#Auto start service
RUN chkconfig httpd on
RUN service httpd start

#Install php
RUN yum install -y php56 php56-devel php56-cli php56-common php56-gd php56-intl php56-jsonc php-pear\
    php56-mbstring php56-mcrypt php56-mysqlnd php56-pdo php56-pecl-redis php56-soap php56-xml php56-xmlrpc

#Configurações adicionais do php
RUN echo 'include_path = ".:/usr/local/etc/php/"' >> /etc/php.ini

#Install XDebug
RUN pecl install xdebug-2.5.5

#Configuration XDebug
RUN echo 'zend_extension=/usr/lib64/php/5.6/modules/xdebug.so' >> /etc/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Quality tools
RUN USERNAME=$('whoami') && composer global require squizlabs/php_codesniffer=*  phpcompatibility/php-compatibility=* \
       friendsofphp/php-cs-fixer=* phpmd/phpmd=* \
    && export PATH=/$USERNAME/.composer/vendor/bin:$PATH \
    && phpcs --config-set installed_paths /$USERNAME/.composer/vendor/phpcompatibility/php-compatibility/ \
    && phpcs -i


EXPOSE  80

ENTRYPOINT ["/usr/sbin/httpd","-D","FOREGROUND"]