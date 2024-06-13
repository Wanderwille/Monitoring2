# Домашнее задание к занятию 14 «Средство визуализации Grafana» - Подус Сергей

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.


# Ответ: 

# 1. 

![Скриншот 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/Monitoring2/zad%201.png)

# 2. 

- утилизация CPU для nodeexporter (в процентах, 100-idle);
```bash
100 - (avg by (instance) (rate(node_cpu_seconds_total{job="nodeexporter",mode="idle"}[1m])) * 100)
```
- CPULA 1/5/15;
```bash
avg by (instance)(rate(node_load1{}[1m]))
avg by (instance)(rate(node_load5{}[1m]))
avg by (instance)(rate(node_load15{}[1m])) 
```
- количество свободной оперативной памяти;
```bash
avg(node_memory_MemFree_bytes{instance="nodeexporter:9100",job="nodeexporter"})
avg(node_memory_MemAvailable_bytes{instance="nodeexporter:9100", job="nodeexporter"})
```
- количество места на файловой системе.
```bash
node_filesystem_free_bytes{fstype="ext4",instance="nodeexporter:9100",job="nodeexporter"}
```

![Скриншот 2](https://github.com/Wanderwille/scrinshot/blob/scrin2/Monitoring2/zad2-2.png)

# 3. 

![Скриншот 3](https://github.com/Wanderwille/scrinshot/blob/scrin2/Monitoring2/zad3-1.png)

![Скриншот 4](https://github.com/Wanderwille/scrinshot/blob/scrin2/Monitoring2/zad3.png)

# 4. 

Файл с Дашбордом: 

https://github.com/Wanderwille/file/blob/main/dashboard.json

