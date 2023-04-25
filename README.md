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
```sh
istioctl install
```

Деплоим Kiali.
```sh
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.17/samples/addons/kiali.yaml
```

Открываем Kiali Dashboard.
```sh
istioctl dashboard kiali
```
