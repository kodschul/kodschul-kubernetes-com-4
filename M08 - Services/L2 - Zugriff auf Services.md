## Kubernetes: Zugriff auf Services

In Kubernetes ermöglichen Services die Exposition von Anwendungen im Cluster und die Kommunikation zwischen verschiedenen Teilen einer Anwendung. Der Zugriff auf Services ist entscheidend für die Bereitstellung von Anwendungen und die Interaktion mit ihnen. Im Folgenden sind einige grundlegende Konzepte und Methoden beschrieben, wie auf Services in Kubernetes zugegriffen werden kann:

### Service Discovery

Service Discovery ist der Prozess, durch den Clients die IP-Adresse und den Port eines Dienstes finden können, um mit ihm zu kommunizieren. Kubernetes bietet verschiedene Methoden für Service Discovery:

#### 1. DNS-Namensauflösung

Kubernetes stellt standardmäßig DNS-Namensauflösung für Services bereit. Jeder Service erhält automatisch einen DNS-Eintrag, der die Auflösung des Service-Namens in die entsprechende IP-Adresse ermöglicht.

Beispiel: Der Service "my-service" kann über den DNS-Namen "my-service.namespace.svc.cluster.local" aufgerufen werden.

#### 2. Umgebungsvariablen

Kubernetes setzt automatisch Umgebungsvariablen für jeden Container in einem Pod, die den Zugriff auf Services ermöglichen. Diese Variablen enthalten die IP-Adresse und den Port des Dienstes.

Beispiel: Ein Service "my-service" kann in einem Container über die Umgebungsvariable "MY_SERVICE_SERVICE_HOST" aufgerufen werden.

### Exponieren von Services

Kubernetes bietet verschiedene Möglichkeiten, Services nach außen zu exponieren, damit sie von Clients außerhalb des Clusters erreichbar sind:

#### 1. NodePort

Der NodePort-Typ exponiert einen Service auf einem festgelegten Port auf allen Nodes im Cluster. Der Service ist dann über die IP-Adresse des Nodes und den zugewiesenen Port erreichbar.

Beispiel:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30000
```

In diesem Beispiel wird der Service "my-service" auf Port 30000 auf allen Nodes im Cluster exponiert.

#### 2. LoadBalancer
Der LoadBalancer-Typ erstellt einen externen Load Balancer in einem unterstützten Cloud-Provider, der den eingehenden Traffic auf den Service verteilt.

Beispiel:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
```

In diesem Beispiel wird ein externer Load Balancer erstellt, der den eingehenden Traffic auf Port 80 an den Service "my-service" weiterleitet.

#### Ingress
Ingress ist eine Kubernetes-Ressource, die den Zugriff auf Services auf Layer 7 ermöglicht. Sie bietet Funktionen wie SSL-Terminierung, Routen basierend auf Hostnamen und Pfaden sowie Load-Balancing.

Beispiel:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: my.domain.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

In diesem Beispiel wird der Service "my-service" über den Hostnamen "my.domain.com" und den Pfad "/" über den Ingress zugänglich gemacht.

Der Zugriff auf Services ist ein grundlegendes Konzept in Kubernetes und ermöglicht die Skalierung, Kommunikation und Bereitstellung von Anwendungen im Cluster.