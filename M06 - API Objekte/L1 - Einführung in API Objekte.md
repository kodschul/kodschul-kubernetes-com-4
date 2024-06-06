## Kubernetes: Einführung in API Objekte

API-Objekte sind die grundlegenden Bausteine in Kubernetes, die es ermöglichen, die gewünschten Zustände einer Anwendung oder eines Clusters zu definieren und zu verwalten. Sie werden verwendet, um Ressourcen wie Pods, Services, Deployments usw. zu beschreiben. Im Folgenden werden grundlegende Konzepte und Beispiele für Kubernetes-API-Objekte erläutert:

### Grundlegende Konzepte

Kubernetes-API-Objekte sind JSON- oder YAML-Dokumente, die die gewünschten Zustände der Ressourcen im Kubernetes-Cluster definieren. Jedes Objekt hat einen eindeutigen Namen und eine API-Version. Zu den häufig verwendeten API-Objekten gehören:

- **Pods**: Die kleinste bereitstellbare Einheit in Kubernetes, die eine oder mehrere Container enthält.
- **Services**: Definieren eine logische Gruppe von Pods und eine Richtlinie, wie auf sie zugegriffen werden kann.
- **Deployments**: Steuern die Bereitstellung von ReplicaSets und ermöglichen Updates und Rollbacks von Anwendungen.
- **ReplicaSets**: Stellen sicher, dass eine bestimmte Anzahl von Pod-Replikaten immer verfügbar ist.
- **ConfigMaps**: Halten Konfigurationsdaten in Form von Schlüssel-Wert-Paaren für Anwendungen bereit.
- **Secrets**: Speichern sensible Daten wie Kennwörter und Zugriffsschlüssel.

### Beispiel: Pod

Ein Pod-Objekt definiert einen einzelnen ausführbaren Prozess in Kubernetes.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
```

In diesem Beispiel wird ein Pod mit dem Namen "nginx-pod" erstellt, der einen einzelnen Container mit der neuesten Version von Nginx verwendet.

### Beispiel: Service
Ein Service-Objekt definiert einen gruppierten Zugriff auf eine Gruppe von Pods.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

In diesem Beispiel wird ein Service mit dem Namen "nginx-service" erstellt, der auf Pods mit dem Label "app=nginx" verweist und den TCP-Port 80 bereitstellt.

### Beispiel: Deployment
Ein Deployment-Objekt definiert eine Anwendung oder einen Mikrodienst in Kubernetes.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```

In diesem Beispiel wird ein Deployment mit dem Namen "nginx-deployment" erstellt, das drei Replikate von Pods mit dem Label "app=nginx" bereitstellt und den TCP-Port 80 öffnet.

Diese Beispiele bieten eine Einführung in die Grundlagen der API-Objekte in Kubernetes und zeigen, wie sie verwendet werden können, um Anwendungen und Dienste im Cluster zu definieren und zu verwalten.