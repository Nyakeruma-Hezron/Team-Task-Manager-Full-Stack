# redis/Dockerfile
FROM redis:7-alpine

# Copy our custom configuration file into the container
COPY redis.conf /usr/local/etc/redis/redis.conf

# Start Redis using our custom config
CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]