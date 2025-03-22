# Cluster

Цей репозиторій містить інструкції та конфігурації для налаштування Kubernetes кластера за допомогою Minikube та VirtualBox.

## Встановлення

Для налаштування кластера на вашому комп'ютері, вам потрібно виконати кілька кроків:

1. Встановіть необхідні інструменти:

    - **VirtualBox**: Завантажте та встановіть з [офіційного сайту VirtualBox](https://www.virtualbox.org/).
    - **kubectl**: Завантажте та встановіть з [офіційного сайту Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
    - **Minikube**: Завантажте та встановіть з [офіційного сайту Minikube](https://minikube.sigs.k8s.io/docs/).

2. Додатково, на Windows, потрібно вимкнути Hyper-V:

    ```bash
    dism.exe /Online /Disable-Feature:Microsoft-Hyper-V
    ```

## Налаштування Minikube

Після встановлення необхідних інструментів, виконайте наступні команди для запуску Minikube:

1. Запустіть Minikube з параметрами, що виділяють ресурси для вашого кластера:

    ```bash
    minikube start --cpus=2 --memory=2gb --disk-size=10gb -p STEP
    ```

2. Для використання VirtualBox як драйвера:

    ```bash
    minikube start --cpus=2 --memory=2gb --disk-size=10gb -p STEP --driver=virtualbox
    ```

3. Щоб зупинити Minikube кластер:

    ```bash
    minikube stop -p STEP
    ```

4. Для видалення кластера:

    ```bash
    minikube delete -p STEP
    ```

## Використання Kubernetes

Для роботи з вашим Kubernetes кластером, ви можете використовувати `kubectl` для виконання різних команд:

1. Перевірка статусу компонентів:

    ```bash
    kubectl get componentstatuses
    ```

2. Перевірка сервісів у кластері:

    ```bash
    kubectl get services
    ```

3. Інформація про кластер:

    ```bash
    kubectl cluster-info
    ```

4. Перевірка вузлів у кластері:

    ```bash
    kubectl get nodes
    ```

5. Перегляд та керування контейнерами (Pods):

    ```bash
    kubectl get pods
    kubectl delete pods hello
    kubectl describe pods hello
    kubectl exec hello date
    kubectl exec -it hello -- /bin/bash
    ```

6. Створення та опис поду:

    ```bash
    kubectl run pode-1 --image=ubuntu/apache2 --port=80
    kubectl describe pod pode-1
    kubectl exec -it pode-1 --container pode-1 -- /bin/bash
    ```

7. Порт-форвардинг:

    ```bash
    kubectl port-forward pode-1 8000:80
    ```

## Маніфести

Маніфести використовуються для опису ресурсів, які будуть розгорнуті в Kubernetes.

1. Мінімальний маніфест для створення ресурсу:

    ```yaml
    apiVersion: batch/v1
    kind: test
    metadata:
      name: test
    spec:
      containers:
      - name: test
        image: ubuntu/apache2
    ```

    Для застосування маніфесту використовуйте команду:

    ```bash
    kubectl apply -f manifest.yaml
    ```

2. Для видалення маніфесту:

    ```bash
    kubectl delete -f manifest.yaml
    ```

3. Маніфест для створення поду з двома контейнерами (Nginx та Tomcat):

    ```yaml
    apiVersion : v1
    kind: Pod
    metadata:
      name: my-app
    spec:
      containers:
        - name : container-web
          image: nginx:latest
          ports:
            - containerPort: 80
        - name : container-api
          image: tomcat:8.5.38
          ports:
            - containerPort: 8080
    ```

Цей маніфест створює под з двома контейнерами: один для веб-сервера Nginx, інший для серверу додатків Tomcat.
