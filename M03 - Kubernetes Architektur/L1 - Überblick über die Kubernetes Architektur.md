## Kubernetes: Überblick über die Kubernetes Architektur

Kubernetes ist ein leistungsstarkes Open-Source-Orchestrierungstool, das für die Verwaltung containerisierter Anwendungen entwickelt wurde. Die Architektur von Kubernetes ist modular und ermöglicht die Skalierung, den Betrieb und die Verwaltung von Anwendungen in großen Clustern von Hosts. Im Folgenden wird ein Überblick über die Kernkomponenten und die allgemeine Architektur von Kubernetes gegeben:

### Kernkomponenten

#### 1. Master-Knoten (Master Node)

Der Master-Knoten ist das Hauptsteuerelement des Kubernetes-Clusters und besteht aus mehreren Komponenten:

- **Kube-apiserver**: Die zentrale API-Schnittstelle für Kubernetes, über die alle Anfragen und Operationen an das Cluster gesendet werden.
- **etcd**: Ein konsistenter und hochverfügbarer Key-Value-Store, der für die Speicherung des Clusterzustands und der Konfigurationseinstellungen verwendet wird.
- **Kube-scheduler**: Verantwortlich für die Planung von Pods auf den Nodes im Cluster basierend auf Ressourcenanforderungen, Affinitäten und anderen Richtlinien.
- **Kube-controller-manager**: Enthält mehrere Controller, die den Zustand des Clusters überwachen und sicherstellen, dass die deklarative Zustandsdefinition mit dem tatsächlichen Zustand übereinstimmt.

#### 2. Worker-Knoten (Worker Node)

Die Worker-Knoten sind die Rechenressourcen des Kubernetes-Clusters, auf denen die Container ausgeführt werden. Jeder Worker-Knoten besteht aus folgenden Komponenten:

- **Kubelet**: Ein Agent, der auf jedem Worker-Knoten läuft und die Kommunikation zwischen dem Kubernetes-Master und den Containern auf dem Node verwaltet.
- **Kube-proxy**: Ein Netzwerk-Proxy, der auf jedem Worker-Knoten läuft und den Netzwerkverkehr für die Pods in einem Kubernetes-Cluster verwaltet.
- **Container Runtime**: Die Software, die für das Ausführen von Containern zuständig ist, z. B. Docker, containerd oder CRI-O.

#### 3. Kubernetes-API-Objekte

Kubernetes verwendet verschiedene API-Objekte zur Beschreibung der gewünschten Zustände von Anwendungen und Ressourcen im Cluster:

- **Pods**: Die kleinste ausführbare Einheit in Kubernetes, die einen oder mehrere Container enthält.
- **Services**: Eine permanente Netzwerkverbindung, die auf Pods verweist und Load-Balancing sowie Service Discovery ermöglicht.
- **Deployments**: Eine Möglichkeit, Pods und ReplicaSets zu deklarieren und zu verwalten, um Anwendungen in einem Kubernetes-Cluster zu skalieren und zu aktualisieren.
- **ConfigMaps und Secrets**: Ressourcen zur Verwaltung von Konfigurationsdaten und sensiblen Informationen, die von Anwendungen verwendet werden.

### Architekturübersicht

Die Architektur von Kubernetes besteht aus einem Master-Knoten, der die Steuerungsebene des Clusters bildet, und einer beliebigen Anzahl von Worker-Knoten, die die ausführbare Ebene bilden. Der Master-Knoten ist für die Koordination und Verwaltung des Clusterzustands sowie für die Bereitstellung von Diensten und APIs verantwortlich. Die Worker-Knoten führen die tatsächlichen Arbeitslasten aus, indem sie Container basierend auf den bereitgestellten Spezifikationen starten und verwalten.

Kubernetes bietet eine flexible und skalierbare Architektur, die es ermöglicht, containerisierte Anwendungen effizient zu betreiben und zu verwalten, unabhängig von der Größe und Komplexität des Clusters.
