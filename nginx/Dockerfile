# nginx/Dockerfile
FROM nginx:alpine

# Remove the default config and add our custom proxy config
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]