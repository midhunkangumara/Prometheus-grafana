# Prometheus-grafana

### WORK-FLOW
![Screenshot from 2022-06-28 12-08-09](https://user-images.githubusercontent.com/104076975/176113926-f4e1b269-25dc-4f06-8a8c-e07d4dde7527.png)

### PROMETHEUS SETUP

[We are using prometheus container]
  
  1. Update apt
  
           $ sudo apt update
           
 2. Add a user named prometheus
 
           $ useradd -rs /bin/false prometheus
           
 3. Create conf. folder and file for prometheus
 
          $ mkdir /etc/prometheus
          $ touch /etc/prometheus/prometheus.yml
          
 4. Create data storing location for prometheus
 
          $ mkdir -p /data/prometheus
          
5. changing ownership
 
          $ chown prometheus:prometheus /data/prometheus/
          $ chown prometheus:prometheus /etc/prometheus/*

