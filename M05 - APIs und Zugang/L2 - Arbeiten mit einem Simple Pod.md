## Kubernetes: Arbeiten mit einem Simple Pod

Ein Pod ist die kleinste bereitstellbare Einheit in Kubernetes, die eine oder mehrere Container enthält und gemeinsame Netzwerk- und Speicherressourcen teilt. Das Arbeiten mit einem einfachen Pod ist ein grundlegendes Konzept in Kubernetes, um Containeranwendungen zu orchestrieren. Im Folgenden werden die grundlegenden Schritte beschrieben, um einen einfachen Pod in Kubernetes zu erstellen und zu verwalten:

### Schritt 1: Pod-Definition erstellen

Eine Pod-Definition ist eine YAML-Datei, die die Konfiguration des Pods definiert, einschließlich des Containerimages, der Umgebungsvariablen, der Ressourcenanforderungen usw. Ein einfaches Beispiel für eine Pod-Definition könnte so aussehen:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: nginx
```

In diesem Beispiel wird ein einfacher Pod mit einem Container erstellt, der das Nginx-Image verwendet.

### Schritt 2: Pod erstellen
Um den Pod in Kubernetes zu erstellen, verwenden Sie den Befehl kubectl apply mit der Pod-Definition:

```bash

kubectl apply -f pod-definition.yaml
```

Dieser Befehl erstellt den Pod gemäß der definierten Konfiguration.

### Schritt 3: Pod-Status überprüfen
Nachdem der Pod erstellt wurde, können Sie den Status des Pods überprüfen, um sicherzustellen, dass er erfolgreich gestartet wurde:

```bash
kubectl get pods
```

Dieser Befehl zeigt eine Liste der vorhandenen Pods und ihren aktuellen Status an.

### Schritt 4: Auf den Pod zugreifen
Um auf den Pod zuzugreifen und mit ihm zu interagieren, können Sie den Befehl kubectl exec verwenden:

```bash
kubectl exec -it mypod -- /bin/bash
```

Dieser Befehl öffnet eine interaktive Shell im Container des Pods, sodass Sie Befehle ausführen und den Zustand des Containers überprüfen können.

### Schritt 5: Pod löschen
Wenn der Pod nicht mehr benötigt wird, können Sie ihn mit dem Befehl kubectl delete löschen:

```bash
kubectl delete pod mypod
```
