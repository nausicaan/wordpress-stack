FROM nginx:1.27.0

# Install the GNU Compiler Collection
RUN apt-get update && apt-get install -y \
        gcc mono-mcs \
    && rm -rf /var/lib/apt/lists/* \
    && rm  /etc/nginx/conf.d/default.conf \
    # Create the necessary directories
    && mkdir -p /var/cache/nginx/client_temp \
        /var/cache/nginx/proxy_temp \
        /var/cache/nginx/fastcgi_temp \
        /var/cache/nginx/scgi_temp \
        /var/cache/nginx/uwsgi_temp \
        /etc/nginx/sites-available \
        /etc/nginx/sites-enabled \
        /etc/nginx/blocklists \
    # Claim ownership for the NGINX user
    && chown -R nginx:nginx /etc/nginx

# Copy the NGINX configuration files
ADD wordpress.conf /etc/nginx/sites-available
ADD nginx.pid /var/log/nginx
ADD nginx.conf /etc/nginx

# Create the symbolic link
RUN ln -s /etc/nginx/sites-available/wordpress.conf /etc/nginx/sites-enabled/wordpress.conf

# Set the working directory
WORKDIR /data

# Switch to the NGINX user
USER nginx