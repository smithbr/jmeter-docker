FROM ubuntu
MAINTAINER Brandon Smith <bsmith@axs.com>

RUN apt-get update && \
    apt-get install -y \
    default-jre \
    curl

RUN useradd -ms /bin/bash jmeter
USER jmeter
WORKDIR /home/jmeter

RUN curl https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-3.2.tgz > \
        /home/jmeter/apache-jmeter-3.2.tgz && \
    tar -xvzf /home/jmeter/apache-jmeter-3.2.tgz && \
    rm /home/jmeter/apache-jmeter-3.2.tgz

ENV JMETER_HOME /home/jmeter/apache-jmeter-3.2/
ENV PATH $JMETER_HOME/bin:$PATH

RUN curl -L https://jmeter-plugins.org/get/ > \
        $JMETER_HOME/lib/ext/plugins-manager.jar && \
    curl -L http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/2.0/cmdrunner-2.0.jar > \
        $JMETER_HOME/lib/cmdrunner-2.0.jar && \
    java -cp $JMETER_HOME/lib/ext/plugins-manager.jar \
        org.jmeterplugins.repository.PluginManagerCMDInstaller

# jpgc-casutg = https://jmeter-plugins.org/wiki/ConcurrencyThreadGroup/
# jpgc-tst = https://jmeter-plugins.org/wiki/ThroughputShapingTimer/
# jpgc-ffw = https://jmeter-plugins.org/wiki/FlexibleFileWriter/
# jpgc-csl = https://jmeter-plugins.org/wiki/ConsoleStatusLogger/
# jpgc-autostop = https://jmeter-plugins.org/wiki/AutoStop/
# jpgc-functions = https://jmeter-plugins.org/wiki/Functions/
# jpgc-dummy = https://jmeter-plugins.org/wiki/DummySampler/
# jpgc-json = https://jmeter-plugins.org/wiki/JSONPathExtractor/
# jpgc-sense = https://github.com/Blazemeter/jmeter-bzm-plugins/blob/master/sense-uploader/BlazemeterPlugin.md
RUN $JMETER_HOME/bin/PluginsManagerCMD.sh install \
        jpgc-casutg,jpgc-tst,jpgc-ffw,jpgc-csl,jpgc-autostop,jpgc-functions,jpgc-dummy,jpgc-json,jpgc-sense

RUN $JMETER_HOME/bin/PluginsManagerCMD.sh status
