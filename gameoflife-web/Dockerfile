FROM openjdk:8u151-jdk-alpine3.7

EXPOSE 8070

ENV APP_HOME /usr/src/app

COPY target/gameoflife.war $APP_HOME gameoflife.war

WORKDIR $APP_HOME

ENTRYPOINT exec java -jar gameoflife.war
