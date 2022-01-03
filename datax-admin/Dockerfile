FROM harryczqp/jdk1.8:alpine
ENV JAR_PATH="datax-admin.jar"
ENV ENV="PRO"
ENV PORT="8080"
ENV DB_HOST="mysql"
ENV DB_PORT="3306"
ENV DB_USERNAME="root"
ENV DB_PASSWORD="123456"
ENV DB_DATABASE="datax_web"
ENV MAIL_USERNAME=""
ENV MAIL_PASSWORD=""
ENV LOG_DATA_PATH="/opt"

ENV JAVA_CMD_DEV="java   -Dspring.profiles.active=dev "
ENV JAVA_CMD_TEST="java    -XX:+PrintGCDetails -XX:+PrintGC -XX:+UseG1GC -Xloggc:gc.log -Dspring.profiles.active=dev  "
ENV JAVA_CMD_PRO="java  -XX:-OmitStackTraceInFastThrow -Dspring.profiles.active=pro "
EXPOSE 8080
WORKDIR /opt/
ADD ./target/datax-admin-2.1.2.jar /opt/datax-admin.jar

ENTRYPOINT [ "tini", "--", "/bin/sh", "-c", "if [ ${ENV} = 'PRO' ] ; then $JAVA_CMD_PRO $JAVA_OPTS   -jar /opt/${JAR_PATH}; elif [ ${ENV} = 'DEV' ] ; then $JAVA_CMD_DEV $JAVA_OPTS   -jar /opt/${JAR_PATH}; else  $JAVA_CMD_TEST  $JAVA_OPTS   -jar /opt/${JAR_PATH} ;fi"]
