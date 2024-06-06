## Kubernetes: Ingress Controller und Ingress Rules

In Kubernetes ermöglicht der Ingress-Controller den Zugriff auf Dienste innerhalb des Clusters von außen. Ingress-Rules definieren, wie der Verkehr an verschiedene Dienste innerhalb des Clusters geroutet wird. Im Folgenden werden die Konzepte des Ingress-Controllers und der Ingress-Rules erläutert:

### Ingress-Controller

Der Ingress-Controller ist eine Kubernetes-Ressource, die den eingehenden HTTP- und HTTPS-Verkehr verwaltet und an Dienste im Cluster weiterleitet.

#### Funktionen des Ingress-Controllers

- **Routen des Verkehrs**: Der Ingress-Controller leitet eingehenden Verkehr basierend auf den definierten Regeln an entsprechende Dienste weiter.
- **TLS-Terminierung**: Der Ingress-Controller ermöglicht die Terminierung von TLS-Verbindungen und das Verschlüsseln des Verkehrs für Dienste im Cluster.
- **Lastausgleich**: Durch die Konfiguration von Lastausgleichsregeln kann der Ingress-Controller den Verkehr auf mehrere Instanzen eines Dienstes verteilen.

### Ingress Rules

Ingress Rules definieren, wie der Verkehr an Dienste im Cluster geroutet wird. Sie enthalten Regeln zum Übereinstimmen von Hosts und Pfaden sowie Aktionen zum Weiterleiten des Verkehrs.

#### Aufbau von Ingress Rules

- **Host-Regeln**: Bestimmen, welche Hostnamen auf bestimmte Dienste geroutet werden.
- **Pfadregeln**: Definieren, welche Pfade zu welchen Diensten geroutet werden.
- **TLS-Konfiguration**: Legt fest, welche TLS-Zertifikate für verschlüsselten Verkehr verwendet werden.

#### Beispiel für Ingress Rules

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
      - path: /app
        pathType: Prefix
        backend:
          service:
            name: app-service
            port:
              number: 80
```

In diesem Beispiel wird definiert, dass eingehender Verkehr von example.com/app an den Dienst app-service im Cluster weitergeleitet wird.

### Verwendung von Ingress-Controllern in Kubernetes
Um einen Ingress-Controller in einem Kubernetes-Cluster zu verwenden, muss der entsprechende Controller bereitgestellt und konfiguriert werden. Beliebte Ingress-Controller sind z.B. NGINX Ingress Controller, Traefik, oder HAProxy Ingress.

### Zusammenfassung
Der Ingress-Controller und Ingress-Rules sind wichtige Konzepte in Kubernetes, die den externen Zugriff auf Dienste im Cluster ermöglichen und den Verkehr effizient routen. Durch die Definition von Ingress-Rules können komplexe Routing-Szenarien realisiert werden, um den Anforderungen von Anwendungen und Benutzern gerecht zu werden.