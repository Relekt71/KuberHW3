# Домашнее задание к занятию «Запуск приложений в K8S»

## Выполненные задачи

### Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod

#### 1. Создан Deployment с nginx и multitool
- Использован образ nginx:latest и wbitt/network-multitool:latest
- Порт для multitool изменен на 1180 для избежания конфликта

#### 2. Масштабирование до 2 реплик

kubectl scale deployment nginx-multitool-deploy --replicas=2
text


#### 3. Создан Service для доступа к приложениям
- Service type: ClusterIP
- Порты: 80 (nginx) и 1180 (multitool)

#### 4. Проверка доступа из отдельного Pod
- Создан тестовый Pod с multitool
- Проверен доступ к nginx через curl
- Проверен доступ к multitool через curl

### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

#### 1. Создан Deployment с Init-контейнером
- Init-контейнер на основе busybox ожидает появления Service
- Основной контейнер - nginx

#### 2. Проверка состояния до создания Service
- Под находился в статусе Init:0/1
- Init-контейнер ожидал Service

#### 3. Создание Service и запуск основного контейнера
- После создания Service, Init-контейнер успешно завершился
- Основной контейнер nginx запустился
- Под перешел в статус Running

## Манифесты

- [deployment-task1.yaml](deployment-task1.yaml)
- [service-task1.yaml](service-task1.yaml)
- [test-pod.yaml](test-pod.yaml)
- [deployment-task2.yaml](deployment-task2.yaml)
- [service-task2.yaml](service-task2.yaml)

## Результаты проверки

### Все поды

kubectl get pods
text


### Все сервисы

kubectl get svc
text


### Все деплойменты

kubectl get deployments
text


## Вывод

Домашнее задание успешно выполнено. Все приложения работают, доступ обеспечен, Init-контейнер корректно управляет порядком запуска.
