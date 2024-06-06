## Kubernetes: Verwendung von Helm

Helm ist ein Paketmanager für Kubernetes, der das einfache Verwalten, Installieren und Aktualisieren von Anwendungen und Ressourcen in einem Kubernetes-Cluster ermöglicht. Durch die Verwendung von Helm können komplexe Anwendungen und Services einfach bereitgestellt werden, indem sie als vordefinierte Pakete, sogenannte "Charts", definiert werden. Im Folgenden sind einige grundlegende Konzepte und Methoden beschrieben, wie Helm in Kubernetes verwendet werden kann:

### Charts

Ein Helm-Chart ist ein Paket, das eine oder mehrere Ressourcen in Kubernetes beschreibt. Es enthält eine Sammlung von YAML-Dateien, die die Konfiguration der Anwendung definieren, sowie eine optionale Vorlage zur dynamischen Generierung von Konfigurationsdateien. Charts können einfach bereitgestellt, geteilt und wiederverwendet werden.

#### Struktur eines Charts

Die grundlegende Struktur eines Helm-Charts sieht wie folgt aus:

my-chart/
Chart.yaml # Metadata des Charts
values.yaml # Standardwerte für Konfigurationsvariablen
templates/ # Vorlagen für Kubernetes-Ressourcen
charts/ # Abhängigkeiten von anderen Charts

### Installation von Charts

Die Installation eines Charts in Kubernetes erfolgt mit dem Befehl `helm install`.

Beispiel:

```bash
helm install my-release ./my-chart
```

In diesem Beispiel wird das Chart im Verzeichnis ./my-chart unter dem Namen "my-release" installiert.

### Konfiguration von Charts
Helm ermöglicht die Konfiguration von Charts durch Überschreiben von Standardwerten in der values.yaml-Datei oder durch Verwendung von Flaggen beim Installationsbefehl.

Beispiel:

```bash
helm install my-release ./my-chart --set service.port=8080
```

In diesem Beispiel wird der Service-Port des Charts auf 8080 gesetzt.

### Aktualisierung von Charts
Die Aktualisierung eines installierten Charts erfolgt mit dem Befehl helm upgrade.

Beispiel:

```bash
helm upgrade my-release ./my-chart
```

Dieser Befehl aktualisiert das Chart "my-release" auf die neueste Version im Verzeichnis ./my-chart.

### Deinstallation von Charts
Die Deinstallation eines Charts erfolgt mit dem Befehl helm uninstall.

Beispiel:

```bash
helm uninstall my-release
```

Dieser Befehl entfernt das Chart "my-release" aus dem Kubernetes-Cluster.

Helm ist ein leistungsfähiges Werkzeug zur Vereinfachung der Bereitstellung und Verwaltung von Anwendungen in Kubernetes. Durch die Verwendung von Charts können komplexe Anwendungen einfach und konsistent bereitgestellt werden.