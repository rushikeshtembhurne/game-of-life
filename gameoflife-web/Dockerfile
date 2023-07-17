FROM tomcat:8-jre8

EXPOSE 8070

RUN rm -rf /usr/local/tomcat/webapps/*

COPY gameoflife-web/target/gameoflife.war /usr/local/tomcat/webapps/ROOT.war

CMD ["catalina.sh", "run"]
