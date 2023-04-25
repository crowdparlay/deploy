# Пререквизиты

### Окружение
- Linux
- Docker
- Kubernetes

### CLI
- kubectl
- istioctl (см. [Download Istio](https://istio.io/latest/docs/setup/getting-started/#download))



# Поднимаем Istio и Kiali

Инициализируем Istio в дефолтном неймспейсе (см. [Install Istio](https://istio.io/latest/docs/setup/getting-started/#install)).
```fish
istioctl install
kubectl label namespace default istio-injection=enabled
```

Деплоим Kiali.
```fish
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.17/samples/addons/kiali.yaml
```

Открываем Kiali Dashboard.
```fish
istioctl dashboard kiali
```



# Поднимаем Kafka

Выделяем для неё отдельный неймспейс.
```fish
kubectl create namespace kafka
```

Деплоим оператор Strimzi (см. [Strimzi Quick Start](https://strimzi.io/quickstarts/)).
> Apply the Strimzi install files, including ClusterRoles, ClusterRoleBindings and some Custom Resource Definitions (CRDs). The CRDs define the schemas used for the custom resources (CRs, such as Kafka, KafkaTopic and so on) you will be using to manage Kafka clusters, topics and users.
```fish
kubectl create -f https://strimzi.io/install/latest?namespace=kafka -n kafka
```

Создаём кластер Apache Kafka.
```fish
kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka
```



# Тестируем Kafka

В одном терминале запускаем продьюсера.
```posh
kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.34.0-kafka-3.4.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic
```

В другом — консьюмера.
```posh
kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.34.0-kafka-3.4.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning
```

Ну и собственно гоняем plain text сообщения через `stdin`/`stdout`, чтобы проверить работоспособность.
