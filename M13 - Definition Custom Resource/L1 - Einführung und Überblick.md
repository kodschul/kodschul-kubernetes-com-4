## Kubernetes: Einführung und Überblick über die Definition von Custom Resources

In Kubernetes können benutzerdefinierte Ressourcen (Custom Resources) erstellt werden, um die Funktionalität des Clusters zu erweitern und eigene Ressourcentypen zu definieren. Dies ermöglicht es Entwicklern, Kubernetes an ihre spezifischen Anforderungen anzupassen. Im Folgenden werden grundlegende Konzepte und die Definition von Custom Resources in Kubernetes erläutert:

### Grundlegende Konzepte

- **Custom Resources (CR)**: Erweiterung der Kubernetes-API um benutzerdefinierte Ressourcentypen.
- **Custom Resource Definition (CRD)**: Definition eines neuen Ressourcentyps in Kubernetes.
- **Controller**: Eine Kubernetes-Komponente, die benutzerdefinierte Ressourcen überwacht und darauf reagiert.

### Custom Resource Definition (CRD)

Eine Custom Resource Definition ermöglicht es Entwicklern, benutzerdefinierte Ressourcentypen zu definieren und in Kubernetes zu verwenden.

#### Beispiel 1: Definition einer Custom Resource

Die folgende YAML-Datei definiert eine Custom Resource mit dem Namen `MyCustomResource`.

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: mycustomresources.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
  scope: Namespaced
  names:
    plural: mycustomresources
    singular: mycustomresource
    kind: MyCustomResource
    shortNames:
      - mcr
```

In diesem Beispiel wird eine Custom Resource mit dem Namen MyCustomResource in der Gruppe example.com definiert. Die Ressource ist in Kubernetes verfügbar und kann über die API verwendet werden.

### Verwendung von Custom Resources
Nachdem eine Custom Resource definiert wurde, können Instanzen dieser Ressource erstellt und in Kubernetes verwendet werden.

#### Beispiel 2: Erstellung einer Instanz einer Custom Resource
Die folgende YAML-Datei erstellt eine Instanz der Custom Resource MyCustomResource.

```yaml
apiVersion: example.com/v1
kind: MyCustomResource
metadata:
  name: my-instance
spec:
  key: value
```

In diesem Beispiel wird eine Instanz der Custom Resource MyCustomResource mit dem Namen my-instance und einem benutzerdefinierten Feld key erstellt.

### Controller für Custom Resources
Um auf benutzerdefinierte Ressourcen zu reagieren und Aktionen auszuführen, können Controller in Kubernetes erstellt werden.

#### Beispiel 3: Controller für eine Custom Resource
Ein Controller kann benutzerdefinierte Ressourcen überwachen und darauf reagieren, indem er zusätzliche Aktionen ausführt.

```go
package main

import (
	"fmt"
	"time"

	"k8s.io/client-go/kubernetes"
	"k8s.io/client-go/rest"
)

func main() {
	config, err := rest.InClusterConfig()
	if err != nil {
		panic(err.Error())
	}

	clientset, err := kubernetes.NewForConfig(config)
	if err != nil {
		panic(err.Error())
	}

	for {
		customResources, err := clientset.ExampleV1().MyCustomResources("default").List(metav1.ListOptions{})
		if err != nil {
			panic(err.Error())
		}

		for _, cr := range customResources.Items {
			fmt.Printf("Custom Resource Name: %s\n", cr.Name)
			// weitere Aktionen ausführen...
		}

		time.Sleep(10 * time.Second)
	}
}

```

Dieses Beispiel zeigt einen einfachen Controller, der benutzerdefinierte Ressourcen überwacht und auf Änderungen reagiert.

### Zusammenfassung
Custom Resources ermöglichen es Entwicklern, Kubernetes an ihre spezifischen Anforderungen anzupassen, indem sie benutzerdefinierte Ressourcentypen definieren und verwenden. Die Definition von Custom Resources mit CRDs und die Implementierung von Controllern erweitern die Funktionalität von Kubernetes und ermöglichen eine flexible und skalierbare Konfiguration des Clusters.
