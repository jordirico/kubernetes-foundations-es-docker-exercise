FROM mysql:8.3.0

RUN chown -R mysql:root /var/lib/mysql/

ARG MYSQL_ROOT_PASSWORD
ENV MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD

COPY ./mysqldb-init.sql /docker-entrypoint-initdb.d/

EXPOSE 3306