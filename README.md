# jmeter-docker

Docker images for JMeter 3.2 master and slave configurations

## On a local machine

### Bring up slaves

```bash
sudo docker run -dit --name slave01 bsmithaxs/jmeter-slave /bin/bash
sudo docker run -dit --name slave02 bsmithaxs/jmeter-slave /bin/bash
sudo docker run -dit --name slave03 bsmithaxs/jmeter-slave /bin/bash
```

### Bring up master

```bash
sudo docker run -dit --name master bsmithaxs/jmeter-master /bin/bash
```

### Check if they're all running

```bash
sudo docker ps -a
```

### Get all of their IP addresses

```bash
sudo docker inspect --format '{{ .Name }} => {{ .NetworkSettings.IPAddress }}' $(sudo docker ps -a -q)
```

### Put a sample test plan in the master container

```bash
sudo docker exec -i master sh -c 'cat > /home/jmeter/apache-jmeter-3.2/bin/test.jmx' < test.jmx
```

### Go inside the master container

```bash
sudo docker exec -it master /bin/bash
```

### Run the sample test plan

```bash
/home/jmeter/apache-jmeter-3.2/bin/jmeter -n -t /home/jmeter/apache-jmeter-3.2/bin/test.jmx -Djava.rmi.server.hostname=(master ip) -Dclient.rmi.localport=60000 -R(slave01 IP),(slave02 IP),(slave03 IP)
```

## On AWS instances

### Create AWS instances with the following security groups:

```bash
Port=22         Protocol=tcp    Source=0.0.0.0/0
Port=1099       Protocol=tcp    Source=0.0.0.0/0
Port=50000      Protocol=tcp    Source=0.0.0.0/0
Port=60000      Protocol=tcp    Source=0.0.0.0/0
```

### Install docker on the instances

`...`

### On the slave instance(s), do

```bash
sudo docker run -dit --name slave01 -e LOCALIP='(slave01 IP)' -p 1099:1099 -p 50000:50000 bsmithaxs/jmeter-slave /bin/bash
sudo docker run -dit --name slave02 -e LOCALIP='(slave02 IP)' -p 1099:1099 -p 50000:50000 bsmithaxs/jmeter-slave /bin/bash
sudo docker run -dit --name slave03 -e LOCALIP='(slave03 IP)' -p 1099:1099 -p 50000:50000 bsmithaxs/jmeter-slave /bin/bash
```

### On the master instance, do

```bash
sudo docker run -dit --name master -p 60000:60000 bsmithaxs/jmeter-master /bin/bash
```

### On master, run the test

```bash
./jmeter -n -t docker-test.jmx -Djava.rmi.server.hostname=(master IP) -Dclient.rmi.localport=60000 -R(slave01 IP),(slave02 IP),(slave03 IP)
```
