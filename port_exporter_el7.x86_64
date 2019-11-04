from prometheus_client import start_http_server, Gauge
import sys
import subprocess
import time


port_check_metric = Gauge('port_check','Check if port is working',["port","host"])

targets = eval(open("/opt/prometheus-exporters/port_exporter/config.json").read())

if __name__ == "__main__":
    start_http_server(9001)

    while True:
        for host, ports in targets.items():
            for port in ports:
                cmd="nc -vz " + host + " " + port +  " 2>&1 | grep Connected > /dev/null && echo 1 || echo 0"
                result=subprocess.check_output(cmd, shell=True, universal_newlines=True)
                result=result.strip()
                #print('Result is : ')
                #print(result)

                if result == "1" :
                    port_check_metric.labels(port=port,host=host).set(1)
                else:
                    port_check_metric.labels(port=port,host=host).set(0)

        time.sleep(120)
