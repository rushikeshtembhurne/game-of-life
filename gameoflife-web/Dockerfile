FROM openjdk:8u151-jdk-alpine3.7

EXPOSE 8070

ENV APP_HOME /usr/src/app

COPY target/gameoflife.warr $APP_HOME/app.jar

WORKDIR $APP_HOME

CMD ["catalina.sh", "run"]
