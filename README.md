# Prometheus and Grafana for monitoring Docker

## **About**

Docker環境向けのPrometheusモニタリング＋Grafana可視化

## **Inside Package**
* prometheus
* grafana
* nginxexporter
* phpexporter
* mysqlexporter
* web nginx:latest
* app php:7.3-fpm
* db  mysql:5.7

## **How to use**

1. clone the repository
```
$ git clone https://github.com/siwai0208/docker-template-laravel
```

2. convert prometheus.yml file (Your-Host-IP) to x.x.x.x
```
  - job_name: 'nginx'
    static_configs:
    - targets: ['(Your-Host-IP):9113']
  - job_name: 'php-fpm'
    static_configs:
    - targets: ['(Your-Host-IP):9253']
  - job_name: 'mysql'
    static_configs:
    - targets: ['(Your-Host-IP):9104']
```

3. chown grafana directory
```
$  sudo chown -R 472:472 grafana
```

4. up docker-compose
```
$ docker-compose up
```

5. confirm container status by docker-compose ps
```
$ docker-compose ps
prometheus_app_1             docker-php-entrypoint php-fpm    Up      9000/tcp
prometheus_grafana_1         /run.sh                          Up      0.0.0.0:3000->3000/tcp
prometheus_mysql_1           docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp, 33060/tcp
prometheus_mysqlexporter_1   /bin/mysqld_exporter             Up      0.0.0.0:9104->9104/tcp
prometheus_nginxexporter_1   /usr/bin/exporter                Up      0.0.0.0:9113->9113/tcp
prometheus_phpexporter_1     /php-fpm_exporter server         Up      0.0.0.0:9253->9253/tcp
prometheus_prometheus_1      /bin/prometheus --config.f ...   Up      0.0.0.0:9090->9090/tcp
prometheus_web_1             /docker-entrypoint.sh ngin ...   Up      0.0.0.0:8000->80/tcp
```

6. Access web browser

Prometheus: x.x.x.x:9090
![prometheus](https://user-images.githubusercontent.com/53518005/103404532-7c6ab180-4b86-11eb-9d70-9f346cedd2cd.PNG)

<br>

Grafana: x.x.x.x:3000 (default login username : admin password : admin)
![grafana](https://user-images.githubusercontent.com/53518005/103404535-7ffe3880-4b86-11eb-8bd3-7e89c89ff742.PNG)

<br>

Dashboard Sample on Grafana
![grafana](https://user-images.githubusercontent.com/53518005/103404541-84c2ec80-4b86-11eb-85f7-a243841637d5.PNG)

7. (Option) Continue to setup laravel application, see [Here](https://github.com/siwai0208/food-app)