## Kubernetes: RBAC APIs und Zugriffssteuerung

Kubernetes bietet eine leistungsstarke Zugriffssteuerung durch Role-Based Access Control (RBAC). RBAC ermöglicht es Administratoren, den Zugriff auf Kubernetes-Ressourcen basierend auf den Rollen der Benutzer zu kontrollieren. Im Folgenden sind einige grundlegende Konzepte und Operationen von RBAC in Kubernetes beschrieben:

### Grundlegende Konzepte

RBAC in Kubernetes basiert auf folgenden grundlegenden Konzepten:

- **Benutzer (User)**: Eine Entität, die auf das Kubernetes-Cluster zugreift.
- **Rolle (Role)**: Eine Sammlung von Berechtigungen, die auf bestimmte Ressourcen in einem Namespace angewendet werden.
- **Rollenbindung (RoleBinding)**: Eine Zuordnung zwischen einem Benutzer oder einer Gruppe und einer Rolle.
- **Clusterrolle (ClusterRole)**: Eine Sammlung von Berechtigungen, die auf Cluster-Ressourcen angewendet werden.
- **Clusterrollenbindung (ClusterRoleBinding)**: Eine Zuordnung zwischen einem Benutzer oder einer Gruppe und einer Clusterrolle.

### RBAC-APIs

In Kubernetes werden die oben genannten Konzepte durch spezifische APIs verwaltet:

- **Role API**: Verwaltet Rollen und Rollenbindungen auf Namespace-Ebene.
- **ClusterRole API**: Verwaltet Clusterrollen und Clusterrollenbindungen auf Cluster-Ebene.

### Beispiel 1: Erstellen einer Rolle

Eine Rolle definiert eine Sammlung von Berechtigungen, die auf Ressourcen in einem Namespace angewendet werden.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

In diesem Beispiel wird eine Rolle namens "pod-reader" erstellt, die Berechtigungen zum Lesen von Pods im Standardnamespace gewährt.

### Beispiel 2: Erstellen einer Rollenbindung
Eine Rollenbindung weist eine Rolle einem Benutzer oder einer Gruppe in einem Namespace zu.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: alice
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

In diesem Beispiel wird die Rolle "pod-reader" der Benutzerin "alice" im Standardnamespace zugewiesen.

### Beispiel 3: Erstellen einer Clusterrolle
Eine Clusterrolle definiert eine Sammlung von Berechtigungen, die auf Cluster-Ressourcen angewendet werden.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

In diesem Beispiel wird eine Clusterrolle namens "cluster-pod-reader" erstellt, die Berechtigungen zum Lesen von Pods im gesamten Cluster gewährt.

### Beispiel 4: Erstellen einer Clusterrollenbindung
Eine Clusterrollenbindung weist eine Clusterrolle einem Benutzer oder einer Gruppe im gesamten Cluster zu.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-cluster-pods
subjects:
- kind: User
  name: alice
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-pod-reader
  apiGroup: rbac.authorization.k8s.io
```

In diesem Beispiel wird die Clusterrolle "cluster-pod-reader" der Benutzerin "alice" im gesamten Cluster zugewiesen.

### Zusammenfassung
RBAC in Kubernetes bietet eine flexible und granulare Zugriffssteuerung für Cluster-Ressourcen. Durch die Verwendung von Rollen und Bindungen können Administratoren den Zugriff von Benutzern und Gruppen auf bestimmte Ressourcen effektiv kontrollieren.