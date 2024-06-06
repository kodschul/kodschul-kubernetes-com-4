## Kubernetes: Getting Started mit Kubernetes

Kubernetes ist eine Open-Source-Plattform zur Automatisierung der Bereitstellung, Skalierung und Verwaltung containerisierter Anwendungen. Dieses Getting Started Guide bietet eine Einführung in die Grundlagen von Kubernetes und hilft beim Einstieg in die Arbeit mit der Plattform.

### Grundlegende Konzepte

Bevor Sie mit Kubernetes beginnen, ist es wichtig, einige grundlegende Konzepte zu verstehen:

- **Pods**: Die kleinste Bereitstellungseinheit in Kubernetes. Ein Pod kann einen oder mehrere Container enthalten, die gemeinsame Ressourcen und ein gemeinsames Netzwerk teilen.
- **Deployments**: Eine Controller-Ressource zur Deklaration von Anwendungsdeklarationen und -updates. Deployments verwalten Pods und erlauben eine einfache Skalierung und Rollback.
- **Services**: Eine Abstraktion, die Pods gruppiert und einen stabilen DNS-Namen sowie eine IP-Adresse zur Verfügung stellt, über die auf die Pods zugegriffen werden kann.
- **Ingress**: Eine Ressource, die den Zugriff auf Dienste von außerhalb des Kubernetes-Clusters ermöglicht. Ingress kann HTTP- und HTTPS-Routen steuern und Lastenausgleichsfunktionen bereitstellen.

### Beispielanwendung: Hello World

Um die Grundlagen von Kubernetes zu verstehen, können wir eine einfache "Hello World" -Anwendung bereitstellen:

1. Schreiben Sie eine Dockerfile, um eine einfache Anwendung zu containerisieren.
2. Erstellen Sie ein Kubernetes Deployment, um den Container zu starten.
3. Erstellen Sie einen Kubernetes Service, um auf die bereitgestellte Anwendung zuzugreifen.

### Schritt-für-Schritt-Anleitung

#### 1. Erstellen der Docker-Image

```Dockerfile
# Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
```

#### 2. Erstellen des Kubernetes Deployment

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: your-username/hello-world:latest
        ports:
        - containerPort: 80
```

#### 3. Erstellen des Kubernetes Service

```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world-service
spec:
  selector:
    app: hello-world
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```

### Ausführen der Anwendung
1. Erstellen Sie das Docker-Image und laden Sie es in ein Container-Repository hoch.
2. Wenden Sie das Deployment- und Service-Manifest mit kubectl apply -f deployment.yaml und kubectl apply -f service.yaml an.
3. Überprüfen Sie den Status des Deployments mit kubectl get deployments.
4. Überprüfen Sie den Status des Services mit kubectl get services.
5. Greifen Sie auf die bereitgestellte Anwendung über die zugewiesene IP-Adresse oder den DNS-Namen zu.