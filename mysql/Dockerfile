FROM mysql:5.7
COPY ./my.cnf /etc/mysql/conf.d/

ENV MYSQL_DATABASE=cg_apiserver \
    MYSQL_ROOT_PASSWORD=root

ADD ./init.sql /docker-entrypoint-initdb.d

EXPOSE 3306
