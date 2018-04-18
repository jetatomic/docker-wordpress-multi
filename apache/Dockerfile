FROM jetatomic/wp-base:apache

##############################################################################################
# PHP upload settings
##############################################################################################

RUN { \
#  		echo 'file_uploads=On'; \
  		echo 'upload_max_filesize=10M'; \
#  		echo 'memory_limit=64M'; \
  		echo 'post_max_size=10M'; \
      echo 'max_execution_time = 600'; \
} > /usr/local/etc/php/conf.d/upload.ini

##############################################################################################
# WORDPRESS Config
##############################################################################################
# ADD ../wordpress/wp-config.php /var/www/html/wp-config.php
# chown wp-config.php to root
# RUN chown root:root /var/www/html/wp-config.php

##############################################################################################
# WORDPRESS Plugins Setup
##############################################################################################
RUN mkdir /plugins

# Add Plugin Lists
ADD ../wordpress/plugins/ /plugins

# Execute each on its own for better caching support
RUN /plugins.sh /plugins/base
RUN /plugins.sh /plugins/security

# Delete Plugins script and folder
RUN rm /plugins.sh && rm /plugins -r

# ADD Local Plugins
# ADD ../plugins/snapshot /var/www/html/wp-content/plugins/snapshot
ADD ../plugins/snapshot /usr/src/wordpress/wp-content/plugins/snapshot

##############################################################################################
# WORDPRESS Themes Setup
##############################################################################################
# ADD ../themes/my-theme /var/www/html/wp-content/themes/my-theme
