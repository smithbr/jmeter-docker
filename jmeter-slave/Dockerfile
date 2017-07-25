FROM bsmithaxs/jmeter-base
MAINTAINER Brandon Smith <bsmith@axs.com>

EXPOSE 1099 50000

ENTRYPOINT $JMETER_HOME/bin/jmeter-server \
                        -Dserver.rmi.localport=50000 \
                        -Dserver_port=1099 \
                        -Djava.rmi.server.hostname=1.1.0.0
