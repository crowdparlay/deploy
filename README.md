# Пререквизиты

### Окружение
- Linux
- Docker
- Kubernetes

### CLI
- kubectl
- istioctl



# Подготовка

Инициализируем Istio в дефолтном неймспейсе.
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
