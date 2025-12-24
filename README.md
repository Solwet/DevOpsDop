# Мониторинг Docker-контейнеров с помощью Grafana и Prometheus


## Этап 1: Подготовка файлов конфигурации
---
1. Создайте новую директорию для проекта

 mkdir -p /GP

  cd /GP
  
---

## Этап 2: Запуск стека мониторинга

nano docker-compose.yml


```yaml
version: '3.8'

services:
  webapp:
    image: nginx:alpine
    container_name: webapp
    ports:
      - "80:80"
    networks:
      - monitor-net

  cadvisor:
    image: gcr.io/cadvisor/cadvisor:v0.47.2
    container_name: cadvisor
    ports:
      - "8080:8080"
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
    privileged: true
    devices:
      - /dev/kmsg
    networks:
      - monitor-net

  prometheus:
    image: prom/prometheus:v2.47.1
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    networks:
      - monitor-net

  grafana:
    image: grafana/grafana:10.1.5
    container_name: grafana
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


nano prometheus.yml


```yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'cadvisor'
    static_configs:
      - targets: ['cadvisor:8080']
```

docker-compose up -d

docker ps


Должны быть видны 4 контейнера: webapp, cadvisor, prometheus, grafana.


---

## Этап 3: Проверка cAdvisor

Открой в браузере:
🔗 http://localhost:8080
Убедись, что:
Видны все запущенные контейнеры (включая webapp, prometheus и т.д.)
Отображаются метрики CPU, памяти, диска

---


## Этап 4: Проверка Prometheus


Открой:
🔗 http://localhost:9090
Перейди: Status → Targets
→ Убедись, что cadvisor имеет статус UP


## Этап 5: Подключение Grafana к Prometheus


Открой:
🔗 http://localhost:3000
Войди:
Логин: admin
Пароль: admin
При первом входе — поменяй пароль (можно оставить admin для теста)
Добавь источник данных:
Configuration → Data Sources → Add data source
Выбери Prometheus
В поле URL введи:
1
http://prometheus:9090


rate(container_cpu_usage_seconds_total{name="webapp"}[5m])


В терминале выполните:


for i in {1..1000}; do curl -s http://localhost > /dev/null; done










    
