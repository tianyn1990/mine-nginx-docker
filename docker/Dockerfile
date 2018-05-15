FROM nginx:1.14

COPY src/html /usr/share/nginx/html/
COPY src/nginx /etc/nginx

#WORKDIR /etc/nginx

#RUN apt-get update
#RUN apt-get install openssl

EXPOSE 80/tcp
EXPOSE 443/tcp

CMD nginx
