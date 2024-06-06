## Kubernetes: Übersicht über Helm

Helm ist ein Paketmanager für Kubernetes, der das einfache Bereitstellen, Aktualisieren und Verwalten von Anwendungen im Kubernetes-Cluster ermöglicht. Helm verwendet sogenannte "Charts", um Kubernetes-Ressourcen und Anwendungsabhängigkeiten zu definieren und zu organisieren. Im Folgenden sind einige grundlegende Konzepte und Funktionen von Helm beschrieben:

### Charts

Ein Helm-Chart ist eine Sammlung von Dateien, die die Struktur einer Kubernetes-Anwendung definieren. Ein Chart enthält typischerweise:

- **Chart.yaml**: Metadaten des Charts wie Name, Version und Beschreibung.
- **values.yaml**: Konfigurationseinstellungen, die vom Benutzer überschrieben werden können.
- **Templates**: Kubernetes-Ressourcenmanifeste mit Helm-Templatfunktionen für dynamische Konfiguration.

### Helm-Befehle

Helm bietet eine Vielzahl von Befehlen zum Verwalten von Charts und Anwendungen im Kubernetes-Cluster. Einige der wichtigsten Befehle sind:

- **helm install**: Installiert ein Helm-Chart im Cluster.
- **helm upgrade**: Aktualisiert eine vorhandene Helm-Installation.
- **helm uninstall**: Deinstalliert eine Helm-Installation.
- **helm list**: Zeigt alle installierten Charts an.
- **helm search**: Sucht nach verfügbaren Charts in einem Chart-Repository.

### Chart-Repositorys

Helm-Charts werden in Repositorys gehostet, die als zentralisierte Orte für die Veröffentlichung und Entdeckung von Charts dienen. Standardmäßig verwendet Helm das öffentliche Repository "Helm Hub", aber es können auch benutzerdefinierte Repositorys konfiguriert werden.

### Helm-Templates

Helm verwendet Go-Vorlagen, um Kubernetes-Ressourcenmanifeste zu generieren. Dies ermöglicht die Verwendung von Variablen, Schleifen, Bedingungen und anderen Steuerstrukturen, um dynamische Konfigurationen zu erstellen.

Beispiel für eine Helm-Template-Datei (`deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-deployment
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Chart.Name }}
  template:
    metadata:
      labels:
        app: {{ .Chart.Name }}
    spec:
      containers:
      - name: {{ .Chart.Name }}-container
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        ports:
        - containerPort: {{ .Values.port }}
```

In diesem Beispiel werden Variablen wie .Release.Name, .Values.replicaCount und .Values.image.repository verwendet, um dynamische Werte in das Deployment-Manifest einzusetzen.

Helm bietet eine leistungsstarke Möglichkeit, Kubernetes-Anwendungen zu verpacken, zu verwalten und zu bereitstellen. Durch die Verwendung von Charts können Entwickler und Betreiber komplexe Anwendungen mit wiederholbaren und konsistenten Bereitstellungsprozessen erstellen.