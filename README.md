# port_exporter
Port exporter is a prometheus exporter, checks that a port is open or close for a remote host.
You can use one of the port_exporter.py files up to your Linux distribution.

Dependencies the server that you are planning to run port_exporter on:

- It should have python 3 or above
- It should have installed nc tool. 
    To install it on Linux Distributions can be yum install nmap-ncat -y.
- It should have prometheus_client python module



How To run:
Fill the config.json file for your target hosts and ports as shown in config.json file with suitable format of python dictionaries of lists.

port_exporter expose prometheus metrics on 9001 port. If you want to change this port, just replace your port in the port_exporter.py file as shown in below.

start_http_server(9001)


Then run the port_exporter as below;

python3.4 port_exporter.py


Add port_exporter job to prometheus.yml file

  - job_name: 'port_exporter'  
    static_configs:
      - targets: ['your_hostname_or_ip_that_runs_port_exporter.py:9001']
      
      
Metrics:

port_check : Checks if the port is available on remote host that is listed in config.json
      
      
