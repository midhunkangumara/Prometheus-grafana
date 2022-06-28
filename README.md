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


6. Conf file 



                   # my global config
          global:
            scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
            evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
            # scrape_timeout is set to the global default (10s).
          
          # Alertmanager configuration
          #alerting:
          #  alertmanagers:
           #   - static_configs:
           #       - targets:
                    # - alertmanager:9093
          
          # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
          #rule_files:
            # - "first_rules.yml"
            # - "second_rules.yml"
          
          # A scrape configuration containing exactly one endpoint to scrape:
          # Here it's Prometheus itself.
          scrape_configs:
            # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
            - job_name: "prometheus"
          
              # metrics_path defaults to '/metrics'
              # scheme defaults to 'http'.
          
              static_configs:
                - targets: ["localhost:9090"]


   * we are monitering prometheus itself
    * copy uid of prometheus for runing prometeus container

7. running prometheus container

       $  docker run --name myprom -d -p 9090:9090 --user 997:997 --net=host -v /etc/prometheus:/etc/prometheus -v /data/prometheus:/data/prometheus     prom/prometheus --config.file="/etc/prometheus/prometheus.yml" --storage.tsdb.path="data/prometheus"


