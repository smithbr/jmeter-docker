FROM bsmithaxs/jmeter-base
MAINTAINER Brandon Smith <bsmith@axs.com>

RUN apt-get -y install maven

RUN curl apache-maven-3.5.0-bin.tar.gz > \
        /home/jmeter/apache-maven-3.5.0-bin.tar.gz && \
    tar -xvzf /home/jmeter/apache-maven-3.5.0-bin.tar.gz && \
    rm /home/jmeter/apache-maven-3.5.0-bin.tar.gz

ENV M2_HOME=/home/jmeter/apache-maven-3.5.0/
ENV PATH $M2_HOME/bin:$PATH

EXPOSE 60000
