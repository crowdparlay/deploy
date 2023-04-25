# Пререквизиты

### Окружение
- Linux
- Docker
- Kubernetes

### CLI
- kubectl
- istioctl



# Подготовка

Инициализируем Istio.
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
