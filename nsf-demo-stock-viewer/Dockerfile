FROM openjdk:8

ENV TZ=Asia/Shanghai LANG=C.UTF-8 LANGUAGE=C.UTF-8 LC_ALL=C.UTF-8

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN mkdir -p /home/nsf-agent

ADD ./nsf-agent.jar /home/nsf-agent/

ADD ./nsf.yml /home/nsf-agent/

RUN mkdir -p /opt/apm
COPY ./skywalking-napm-bin-8.5.0-latest /opt/apm/skywalking-napm-bin-8.5.0-latest

ADD ./target/nsf*.jar /app.jar
ADD ./start.sh /

ENTRYPOINT ["java","-Dserver.port=8080","-Dstock_viewer_url=http://stock-viewer-wanchu", "-Dstock_provider_url=http://stock-provider-wanchu", "-Dstock_advisor_url=http://stock-advisor-wanchu", "-Dnsf.prometheus.enable=true","-javaagent:/home/nsf-agent/nsf-agent.jar=nsf","-javaagent:/opt/apm/skywalking-napm-bin-8.5.0-latest/agent/skywalking-agent.jar","-Dskywalking_config=opt/apm/skywalking-napm-bin-8.5.0-latest/agent/config/agent.config","-jar","/app.jar"]
