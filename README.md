# Мониторинг Docker-контейнеров с помощью Grafana и Prometheus


## Этап 1: Подготовка файлов конфигурации
---
1. Создайте новую директорию для проекта

<img width="313" height="54" alt="image" src="https://github.com/user-attachments/assets/9aed1f50-2a98-40a4-ab69-4864763030eb" />

---

2. Внутри создайте файл `docker-compose.yml` с определением всех сервисов (webapp, cadvisor, prometheus, grafana)
    - Убедитесь, что все контейнеры находятся в одной Docker-сети
    - Укажите правильные маппинги портов для каждого сервиса


---

## Этап 2: Запуск стека мониторинга
1. Запустите все контейнеры с помощью docker-compose

<img width="1459" height="655" alt="image" src="https://github.com/user-attachments/assets/2969366e-1a88-41c8-b526-5c28cde3a69e" />

2. Проверьте, что все контейнеры работают (используйте команду `docker ps`)

<img width="1471" height="333" alt="image" src="https://github.com/user-attachments/assets/6ea111dc-af2a-417a-b9a7-c44a690a50a0" />

3. Убедитесь, что нет ошибок запуска (проверьте логи контейнеров при необходимости)

---

## Этап 3: Проверка cAdvisor

<img width="1836" height="950" alt="image" src="https://github.com/user-attachments/assets/32f02936-a07d-41ff-9a22-85722db0f18b" />


<img width="1565" height="858" alt="image" src="https://github.com/user-attachments/assets/2904f187-97eb-433e-a37d-37bcd7a585ce" />

---

## Этап 4: Проверка Prometheus


<img width="1915" height="670" alt="image" src="https://github.com/user-attachments/assets/eed8063b-a8f6-45ef-85d4-a625d9171163" />

---

## Этап 5: Подключение Grafana к Prometheus

<img width="1890" height="882" alt="image" src="https://github.com/user-attachments/assets/b9434224-9bbe-4d10-b802-025e5d40b862" />


<img width="1770" height="809" alt="image" src="https://github.com/user-attachments/assets/ad5a38c7-a1e1-4175-8fbd-4f285df883af" />










    
