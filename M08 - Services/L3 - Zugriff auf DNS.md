## Kubernetes: Zugriff auf DNS

Kubernetes bietet eine integrierte DNS-Lösung, die es Anwendungen im Cluster ermöglicht, sich unter Verwendung von DNS-Namen aufzulösen. Dies erleichtert die Kommunikation zwischen verschiedenen Anwendungen und Diensten im Kubernetes-Cluster. Im Folgenden sind einige grundlegende Konzepte und Methoden zum Zugriff auf DNS in Kubernetes beschrieben:

### Grundlegende Konzepte

#### Cluster-DNS

In einem Kubernetes-Cluster wird ein DNS-Server bereitgestellt, der die Namensauflösung für Dienste und Pods im Cluster verwaltet. Dieser DNS-Server ist standardmäßig als `kube-dns` oder `coredns` konfiguriert und ist über die IP-Adresse `10.96.0.10` erreichbar.

#### Namensauflösung

Pods im Kubernetes-Cluster können DNS verwenden, um sich gegenseitig zu erreichen. Die DNS-Namenskonvention für die Auflösung von Dienstnamen lautet: `[servicename].[namespace].svc.cluster.local`.

#### Externe Namensauflösung

Kubernetes bietet auch die Möglichkeit zur Auflösung externer DNS-Namen. Dies ermöglicht es Anwendungen im Cluster, auf Ressourcen außerhalb des Clusters zuzugreifen, indem sie externe DNS-Namen auflösen.

### Methoden zum Zugriff auf DNS

#### Verwendung von DNS-Namen in YAML-Dateien

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dns-example
spec:
  containers:
  - name: dns-container
    image: busybox
    command: ['nslookup', 'example-service.default.svc.cluster.local']
```

In diesem Beispiel wird ein Pod definiert, der den DNS-Namen example-service.default.svc.cluster.local auflöst und das Ergebnis mit nslookup anzeigt.

### Verwendung von DNS in Anwendungscode
Anwendungen in Kubernetes können DNS-Namen verwenden, um auf Dienste zuzugreifen. Zum Beispiel kann eine Anwendung eine HTTP-Anfrage an einen Dienstnamen senden, der von DNS aufgelöst wird.

```pyton
import requests

response = requests.get("http://example-service.default.svc.cluster.local")
print(response.text)
```

In diesem Python-Beispiel sendet die Anwendung eine HTTP-Anfrage an den Dienst example-service unter Verwendung des DNS-Namens.

### Zusammenfassung
Der Zugriff auf DNS in Kubernetes erleichtert die Kommunikation zwischen Anwendungen und Diensten im Cluster. Durch die Verwendung von DNS-Namen können Anwendungen dynamisch und flexibel auf verschiedene Ressourcen im Cluster zugreifen, ohne harte Codierungen von IP-Adressen oder Ports verwenden zu müssen.