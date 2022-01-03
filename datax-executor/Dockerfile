FROM harryczqp/jdk1.8:alpine
ENV JAR_PATH="datax-executor.jar"
ENV ENV="PRO"
ENV PORT="8081"
ENV ADDRESSES="http://localhost:8080"
ENV LOG_DATA_PATH="/opt"
ENV JSON_PATH="/opt/datax/modules/datax-executor/json"
ENV PYTHON_PATH="/opt/datax/bin/datax.py"

ENV JAVA_CMD_DEV="java   -Dspring.profiles.active=dev "
ENV JAVA_CMD_TEST="java    -XX:+PrintGCDetails -XX:+PrintGC -XX:+UseG1GC -Xloggc:gc.log -Dspring.profiles.active=dev  "
ENV JAVA_CMD_PRO="java  -XX:-OmitStackTraceInFastThrow -Dspring.profiles.active=pro "
EXPOSE 8081
WORKDIR /opt/
ADD ./target/datax-executor-2.1.2.jar /opt/datax-executor.jar
#ADD ./datax.tar.gz /opt/datax.tar.gz

RUN apk add python3 tar &&\
    ln -s /usr/bin/python3 /usr/bin/python
RUN wget http://datax-opensource.oss-cn-hangzhou.aliyuncs.com/datax.tar.gz &&\
    tar -xvf datax.tar.gz &&\
    rm -f datax.tar.gz



ENTRYPOINT [ "tini", "--", "/bin/sh", "-c", "if [ ${ENV} = 'PRO' ] ; then $JAVA_CMD_PRO $JAVA_OPTS   -jar /opt/${JAR_PATH}; elif [ ${ENV} = 'DEV' ] ; then $JAVA_CMD_DEV $JAVA_OPTS   -jar /opt/${JAR_PATH}; else  $JAVA_CMD_TEST  $JAVA_OPTS   -jar /opt/${JAR_PATH} ;fi"]
