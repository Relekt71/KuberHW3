# Домашнее задание 1.3

## Задание 1. Deployment с nginx и multitool

### Результаты:
-  Создан Deployment с nginx и multitool
-  Масштабирован до 2 реплик
-  Создан Service для доступа
-  Проверен доступ из отдельного Pod

### Скриншоты:
1. Поды после масштабирования - <img width="635" height="104" alt="изображение" src="https://github.com/user-attachments/assets/88f9c0f7-6c9a-4437-bf0c-50cf8cfae99e" />
2. Сервисы - <img width="754" height="95" alt="изображение" src="https://github.com/user-attachments/assets/155269a6-e309-4d16-b43f-daa684c38f49" />
3. Доступ к nginx - <img width="561" height="74" alt="изображение" src="https://github.com/user-attachments/assets/561fb00f-f53c-4953-8ec9-922f7642300e" />
4. Доступ к multitool - <img width="963" height="481" alt="изображение" src="https://github.com/user-attachments/assets/81e24fb1-6c41-403a-bed5-25b8b58c1fea" />

## Задание 2. Deployment с Init-контейнером

### Результаты:
-  Создан Deployment с Init-контейнером
-  Init-контейнер ожидает Service
-  После создания Service основной контейнер запустился

### Скриншоты:
5. Логи Init-контейнера - <img width="1062" height="62" alt="изображение" src="https://github.com/user-attachments/assets/ab2e6323-f33f-4370-822f-e30281d9accb" />
6. Под до создания Service (Init) - <img width="766" height="184" alt="изображение" src="https://github.com/user-attachments/assets/8722e286-b90d-40de-b70e-8a8bfc625781" />
7. Под после создания Service (Running) - <img width="766" height="184" alt="изображение" src="https://github.com/user-attachments/assets/68c7e196-a95b-49e5-88e3-dbf1d21c476f" />
8. Доступ к nginx через Service 2 - <img width="888" height="481" alt="изображение" src="https://github.com/user-attachments/assets/8cc2b29f-88fe-412c-afc7-39df3c295e5e" />

## Манифесты
- [deployment-task1.yaml](deployment-task1.yaml)
- [service-task1.yaml](service-task1.yaml)
- [test-pod.yaml](test-pod.yaml)
- [deployment-task2.yaml](deployment-task2.yaml)
- [service-task2.yaml](service-task2.yaml)

## Итоговая проверка

### Все поды:

kubectl get pods

    NAME                                      READY   STATUS    RESTARTS   AGE
    nginx-multitool-deploy-6bd7465f5f-7vjh4   2/2     Running   0          31m
    nginx-multitool-deploy-6bd7465f5f-x2cd5   2/2     Running   0          28m
    nginx-with-init-576b96668c-tj7lm          1/1     Running   0          20m
    test-multitool-pod                        1/1     Running   0          29m


### Все сервисы:

kubectl get svc

    NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)           AGE
    kubernetes                ClusterIP   10.152.183.1     <none>        443/TCP           41m
    nginx-multitool-service   ClusterIP   10.152.183.137   <none>        80/TCP,1180/TCP   32m
    nginx-service             ClusterIP   10.152.183.173   <none>        80/TCP            25m

### Все деплойменты:

kubectl get deployments

    NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
    nginx-multitool-deploy   2/2     2            2           32m
    nginx-with-init          1/1     1            1           22m
