# Use official Apache HTTPD base image
FROM httpd:2.4

# Remove default HTML files (optional, for cleanliness)
RUN rm -rf /usr/local/apache2/htdocs/*

# Copy your custom HTML folder to Apache's web directory
COPY week_11/html /usr/local/apache2/htdocs/