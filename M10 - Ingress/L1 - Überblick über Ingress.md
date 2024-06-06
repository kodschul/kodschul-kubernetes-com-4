## Kubernetes: Überblick über Ingress

In Kubernetes bietet der Ingress-Controller eine Möglichkeit, den externen Zugriff auf Dienste in einem Kubernetes-Cluster zu verwalten. Ingress-Ressourcen definieren Regeln für den HTTP- und HTTPS-Zugriff auf Dienste in einem Cluster. Im Folgenden wird ein Überblick über Ingress in Kubernetes gegeben:

### Grundlegende Konzepte

#### Ingress-Ressourcen

Ingress-Ressourcen definieren Regeln für den HTTP- und HTTPS-Zugriff auf Dienste in einem Kubernetes-Cluster. Sie ermöglichen die Konfiguration von Routen, Load Balancing und SSL/TLS-Terminierung.

#### Ingress-Controller

Ein Ingress-Controller ist eine Software, die Ingress-Ressourcen überwacht und die definierten Regeln implementiert. Es gibt verschiedene Ingress-Controller wie nginx-ingress, Traefik, und Istio.

### Konfiguration von Ingress

#### Beispiel 1: Einfache Ingress-Ressource

Eine einfache Ingress-Ressource definiert eine Route von einem externen Host zu einem Dienst in einem Kubernetes-Cluster.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: example-service
            port:
              number: 80
```

In diesem Beispiel wird der Host example.com auf den Dienst example-service gemappt.

#### Beispiel 2: SSL/TLS-Terminierung
Ingress-Ressourcen können auch für SSL/TLS-Terminierung konfiguriert werden, um verschlüsselte Verbindungen zu ermöglichen.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: example-service
            port:
              number: 80
  tls:
  - hosts:
    - example.com
    secretName: example-tls-secret
```

In diesem Beispiel wird ein SSL/TLS-Zertifikat mit dem Host example.com konfiguriert.

### Ingress-Controller
#### nginx-ingress
Der nginx-ingress-Controller ist ein beliebter Ingress-Controller für Kubernetes. Er verwendet den nginx-Webserver, um den HTTP- und HTTPS-Verkehr zu routen und zu steuern.

#### Traefik
Traefik ist ein moderner Ingress-Controller, der native Unterstützung für Docker und Kubernetes bietet. Er bietet Funktionen wie automatische Konfiguration, Lastausgleich und SSL/TLS-Terminierung.

#### Istio
Istio ist eine Service-Mesh-Plattform, die auch Ingress-Funktionen bereitstellt. Es bietet erweiterte Funktionen wie Verkehrsregelung, Sicherheit und Überwachung.

Zusammenfassung
Ingress in Kubernetes bietet eine flexible Möglichkeit, den externen Zugriff auf Dienste in einem Cluster zu verwalten. Durch die Konfiguration von Ingress-Ressourcen können komplexe Routing- und Load-Balancing-Szenarien implementiert werden. Die Auswahl des richtigen Ingress-Controllers ist entscheidend, um die Anforderungen an Leistung, Skalierbarkeit und Sicherheit zu erfüllen.