FROM maven:3.8.5-openjdk-11 as build
WORKDIR /app
COPY . /app
RUN mvn -f /app/pom.xml clean package

FROM openjdk:11-jdk
COPY --from=build /app/target/ssh-0.0.1-SNAPSHOT.jar /app/ssh-0.0.1-SNAPSHOT.jar
COPY --from=build /app/init_container.sh /app/
 
RUN apt-get update -yy \
    && apt-get install -y --no-install-recommends dialog \
    && apt-get install -y --no-install-recommends openssh-server \
    && echo "root:Docker!" | chpasswd \
    && chmod u+x /app/init_container.sh

COPY --from=build /app/sshd_config /etc/ssh/

EXPOSE 8080 2222
ENTRYPOINT [ "/app/init_container.sh" ]