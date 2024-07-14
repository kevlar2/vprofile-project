FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/kevlar2/vprofile-project.git
RUN cd vprofile-project && git checkout containers && mvn install

FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="KevinO"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/*.war /usr/local/tomcat/webapps/ROOT.war
RUN chmod +x /usr/local/tomcat/bin/catalina.sh

EXPOSE 8080
CMD ["catalina.sh", "run"]