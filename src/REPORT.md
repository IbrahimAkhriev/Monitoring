# Monitoring System Report

## Part 1. Получение метрик и логов

### Цель
Настроить сбор метрик и логов приложения с использованием Prometheus и Loki в Docker Swarm.

---

### Используемая инфраструктура
- Docker Swarm (из предыдущего проекта)
- Отдельный стек мониторинга

---

### Сбор метрик приложения
Для приложения были добавлены метрики с использованием библиотеки **Micrometer**:

- Количество отправленных сообщений в RabbitMQ  
- Количество обработанных сообщений в RabbitMQ  
- Количество бронирований  
- Количество запросов к Gateway  
- Количество запросов на авторизацию пользователей  

📸 *Скриншот: метрики приложения (`/metrics`)*
![alt text](<screen/Screenshot from 2026-01-06 21-19-55.png>)
![alt text](<screen/Screenshot from 2026-01-06 21-19-56.png>)
![alt text](<screen/Screenshot from 2026-01-14 13-07-24.png>)

### Сбор логов приложения
Для сбора логов был использован **Loki**.  
Логи приложений отправляются в Loki и доступны для просмотра через Grafana.

📸 *Скриншот: логи приложения в Loki*
![alt text](<screen/Screenshot from 2026-01-16 19-03-13.png>)
---

### Стек мониторинга
В Docker Swarm был развернут отдельный стек мониторинга, включающий следующие сервисы:

- Prometheus Server  
- Loki  
- node_exporter  
- cAdvisor  
- blackbox_exporter  

Prometheus доступен через браузер на порту **9090**.

📸 *Скриншот: Prometheus Web UI (порт 9090)*
![alt text](<screen/Screenshot from 2025-12-31 20-34-13.png>)
---

## Part 2. Визуализация

### Развертывание Grafana
Grafana была развернута как отдельный сервис в стеке мониторинга Docker Swarm.

📸 *Скриншот: Grafana Web UI*

---

### Дашборд Grafana

#### Инфраструктура
- Количество нод  
![alt text](<screen/  Kolich Node.png>)
- Количество контейнеров  
![alt text](<screen/Kol Kont.png>)
- Количество стеков  
![alt text](<screen/Kol stekov.png>)
- Использование CPU по сервисам  

- Использование CPU по ядрам и узлам  
![alt text](<screen/Cpu po yadram.png>)
- Используемая RAM  
![alt text](<screen/Zatracheno RAM.png>)
- Доступная и занятая память  
![alt text](<screen/Zanyzta pamyzt.png>)
![alt text](<screen/Dostupno pamytai.png>)
- Количество CPU  
![alt text](<screen/Kol CPU.png>)
📸 *Скриншот: инфраструктурные метрики*

---

#### Доступность сервисов
- Доступность `google.com` (blackbox_exporter)
![alt text](<screen/Proba blax.png>)

---
- Количество запросов к Gateway  
![alt text](<screen/Screenshot from 2026-01-14 13-07-24.png>)
- Количество запросов на авторизацию пользователей  

---

#### Логи приложения
Логи приложения отображаются в Grafana с использованием Loki.

📸 *Скриншот: логи приложения в Grafana*
![alt text](<screen/Screenshot from 2026-01-16 19-03-13.png>)
---

## Part 3. Отслеживание критических событий

### Развертывание Alertmanager
Alertmanager был развернут как отдельный сервис в стеке мониторинга Docker Swarm и подключен к Prometheus.

📸 *Скриншот: Alertmanager Web UI*
![alt text](<screen/Screenshot from 2026-01-18 22-49-50.png>)
---

### Настроенные алерты
- Доступная память меньше **100 МБ**  
- Использование RAM больше **1 ГБ**  
- Использование CPU сервисом превышает **10%**  


### Оповещения
Alertmanager настроен на отправку уведомлений:

- Email  

📸 *Скриншот: email-уведомление*  
![alt text](<screen/Screenshot from 2026-01-18 22-01-02.png>)

---

## Вывод
Была развернута система мониторинга и оповещений в Docker Swarm, обеспечивающая сбор метрик, логов, визуализацию состояния системы и уведомления о критических событиях.
