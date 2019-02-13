FROM bsmithio/jmeter-base
LABEL maintainer="Brandon Smith <brandon@bsmith.la>"

EXPOSE 1099 50000

ENTRYPOINT $JMETER_HOME/bin/jmeter-server \
                        -Dserver.rmi.localport=50000 \
                        -Dserver_port=1099 \
                        -Djava.rmi.server.hostname=$LOCALIP
