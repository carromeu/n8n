FROM nginx:latest

RUN apt-get update -y && apt-get install -y apache2-utils && rm -rf /var/lib/apt/lists/*

# Basic auth credentials
ENV BASIC_USERNAME=username
ENV BASIC_PASSWORD=password

# Forward host and forward port as env variables
# google.com is used as a placeholder, to be replaced using environment variables
ENV FORWARD_HOST=google.com
ENV FORWARD_PORT=80

# Nginx config file
WORKDIR /
COPY /docker/nginx/nginx-basic-auth.conf ./

# Startup script
COPY /docker/nginx/configure.sh ./
RUN chmod 0755 ./configure.sh
CMD [ "./configure.sh" ]
