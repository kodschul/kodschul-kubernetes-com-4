## Kubernetes: Admission Controller, Pod Policies und Network Policies

In Kubernetes bieten Admission Controller, Pod Policies und Network Policies Mechanismen zur Durchsetzung von Sicherheitsrichtlinien und zur Steuerung des Verhaltens von Pods und Netzwerkverkehr. Diese Funktionen sind entscheidend für die Sicherheit und den Betrieb von Kubernetes-Clustern. Im Folgenden sind einige grundlegende Konzepte und Methoden beschrieben, die mit Admission Controllern, Pod Policies und Network Policies in Kubernetes verbunden sind:

### Admission Controller

Admission Controller sind Webhooks oder Plugins, die Anfragen auf Ressourcen in einem Kubernetes-Cluster validieren und ändern können, bevor sie akzeptiert und persistiert werden. Sie ermöglichen die Durchsetzung von Sicherheitsrichtlinien, Quotierung und benutzerdefinierten Validierungen.

#### Beispiele für Admission Controller-Funktionen:

- **Pod-Sicherheitsrichtlinien (Pod Security Policies)**: Definieren, welche Sicherheitskontexte für Pods zulässig sind, z.B. erzwingen, dass Pods mit einem bestimmten Service-Konto ausgeführt werden.
- **Limitberechnung (Resource Quotas)**: Begrenzen Sie die Menge an CPU, Speicher und anderen Ressourcen, die von einer Namespace oder einem Benutzer verwendet werden können.
- **Validierung benutzerdefinierter Ressourcen**: Stellen Sie sicher, dass benutzerdefinierte Ressourcen bestimmte Anforderungen erfüllen, bevor sie erstellt werden.

### Pod Policies

Pod Policies ermöglichen es Administratoren, Sicherheitsrichtlinien für Pods in einem Kubernetes-Cluster festzulegen. Diese Richtlinien umfassen Einstellungen wie Zugriffssteuerung, Netzwerkrichtlinien und Sicherheitskontexte.

#### Beispiele für Pod Policy-Einstellungen:

- **Zugriffssteuerung (Access Control)**: Definieren, welche Benutzer oder Dienstkonten auf bestimmte Pods zugreifen dürfen.
- **Sicherheitskontexte (Security Contexts)**: Festlegen von Sicherheitsattributen für Pods, wie z.B. Benutzer-ID, Gruppen-ID und Berechtigungen.
- **Netzwerkrichtlinien (Network Policies)**: Steuern des ein- und ausgehenden Netzwerkverkehrs für Pods.

### Network Policies

Network Policies ermöglichen die Kontrolle des ein- und ausgehenden Netzwerkverkehrs für Pods in einem Kubernetes-Cluster. Sie definieren Regeln, die den Datenverkehr auf der Netzwerkschicht (Layer 3/4) basierend auf Quell- und Ziel-IP-Adressen, Portnummern und Protokollen steuern.

#### Beispiel für Network Policy-Regeln:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-nginx
spec:
  podSelector:
    matchLabels:
      app: nginx
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 80
```

In diesem Beispiel wird definiert, dass nur Pods mit dem Label "role: frontend" eingehenden TCP-Verkehr auf Port 80 an Pods mit dem Label "app: nginx" senden dürfen.

Die Verwendung von Admission Controllern, Pod Policies und Network Policies in Kubernetes ermöglicht eine granulare Kontrolle über die Sicherheit und das Verhalten von Pods und Netzwerkverkehr im Cluster. Dies ist entscheidend für die sichere Bereitstellung und den Betrieb von Anwendungen in Kubernetes.