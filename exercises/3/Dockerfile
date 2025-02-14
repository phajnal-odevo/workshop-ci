FROM php:8.1.31-bookworm

# Install Composer
COPY --from=composer:2.3.4 /usr/bin/composer /usr/local/bin/composer

# Create a non-root user and install dependencies
RUN useradd -G www-data -u 1001 -d /home/devuser devuser && \
    usermod -a -G devuser www-data && \
    mkdir -p /home/devuser/.composer && \
    chown -R devuser:devuser /home/devuser && \
    apt update && \
    apt install -y git unzip zip && \
    rm -rf /var/lib/apt/lists/*

# Switch to the non-root
USER devuser
# Set the working directory
WORKDIR /home/devuser

# Copy the composer.json file and install dependencies
COPY composer.json /home/devuser/composer.json
RUN composer install --prefer-dist --no-interaction
