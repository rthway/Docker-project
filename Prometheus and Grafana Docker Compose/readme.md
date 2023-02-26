Here is a sample Docker Compose file that you can use to set up Prometheus and Grafana using Docker:

```
version: '3'

services:
  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus/config:/etc/prometheus
      - ./prometheus/data:/prometheus
    ports:
      - "9090:9090"
  grafana:
    image: grafana/grafana:latest
    volumes:
      - ./grafana/data:/var/lib/grafana
      - ./grafana/config:/etc/grafana
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
```



This Docker Compose file defines two services: Prometheus and Grafana. It specifies the Docker images to use for each service and maps the necessary ports to enable communication between the services. It also defines volumes for storing the configuration files and data for each service.

To use this Docker Compose file, save it to a file (e.g.,  `docker-compose.yml`) and run the following command:

```
docker-compose up
```



This will start the Prometheus and Grafana containers and bring up the monitoring stack. You can then access Grafana by visiting  `http://localhost:3000`  in your web browser.