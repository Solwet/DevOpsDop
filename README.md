# Мониторинг Docker-контейнеров с помощью Grafana и Prometheus


## Этап 1: Подготовка файлов конфигурации
---
1. Создайте новую директорию для проекта

mkdir monitoring-stack
cd monitoring-stack
---

## Этап 2: Запуск стека мониторинга

nano docker-compose.yml


```yaml
version: '3.8'

services:
  webapp:
    image: nginx:alpine
    ports:
      - "80:80"
    networks:
      - monitor-net

  cadvisor:
    image: gcr.io/cadvisor/cadvisor:v0.47.2
    ports:
      - "8080:8080"
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
      - /dev/disk/:/dev/disk:ro
    privileged: true
    devices:
      - /dev/kmsg
    networks:
      - monitor-net

  prometheus:
    image: prom/prometheus:v2.47.1
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
    networks:
      - monitor-net

  grafana:
    image: grafana/grafana:10.1.5
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    networks:
      - monitor-net

networks:
  monitor-net:
    driver: bridge
```

---

## Этап 3: Проверка cAdvisor



## Этап 4: Проверка Prometheus



## Этап 5: Подключение Grafana к Prometheus











    
