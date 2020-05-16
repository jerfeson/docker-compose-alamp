FROM mysql:5.7

RUN echo "[mysqld]" >> /etc/mysql/my.cnf
RUN echo "sql_mode = STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION" >> /etc/mysql/my.cnf
RUN echo "max_allowed_packet=9000M" >> /etc/mysql/my.cnf
RUN echo "wait_timeout = 99999" >> /etc/mysql/my.cnf
RUN echo "interactive_timeout = 99999" >> /etc/mysql/my.cnf