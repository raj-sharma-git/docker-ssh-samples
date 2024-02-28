FROM joomla:latest
WORKDIR /app/


COPY ./ /app/

COPY sshd_config /etc/ssh/

# Start and enable SSH
RUN apt-get update \
    && apt-get install -y --no-install-recommends dialog \
    && apt-get install -y --no-install-recommends openssh-server \
    && echo "root:Docker!" | chpasswd \
    && chmod u+x /app/init_container.sh

EXPOSE 8000 2222

RUN service ssh start

#docker run -it -e JOOMLA_DB_HOST=cmsjoomlacustom-server.mysql.database.azure.com -e JOOMLA_DB_PASSWORD=7JR570117FC7E516$ -e JOOMLA_DB_USER=xnfrchfrvc -p 8080:80 joomla  