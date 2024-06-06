## Kubernetes: Planungseinstellungen und -richtlinien

Die Planung von Pods und Ressourcen in Kubernetes ist ein wichtiger Aspekt für die effiziente Nutzung von Cluster-Ressourcen und die Bereitstellung von Anwendungen. Kubernetes bietet verschiedene Einstellungen und Richtlinien für die Planung von Pods auf Nodes im Cluster. Im Folgenden werden einige grundlegende Konzepte und Optionen zur Planung von Pods in Kubernetes beschrieben:

### Grundlegende Konzepte

Die Planung von Pods in Kubernetes basiert auf verschiedenen Faktoren wie Ressourcenanforderungen, Node-Kapazität, Affinitäten und Anti-Affinitäten. Zu den grundlegenden Konzepten gehören:

- **Ressourcenanforderungen und -beschränkungen**: Festlegung von CPU- und Speicheranforderungen sowie maximalen Ressourcenlimits für Pods.
- **Node-Auswahlkriterien**: Festlegung von Regeln und Vorlieben für die Platzierung von Pods auf Nodes basierend auf Node-Labels, Knotenkapazität oder anderen Attributen.
- **Affinitäten und Anti-Affinitäten**: Steuerung der Pod-Platzierung basierend auf Beziehungen zu anderen Pods oder Nodes im Cluster.

### Planungseinstellungen und -richtlinien

#### Ressourcenanforderungen und -beschränkungen

Ressourcenanforderungen und -beschränkungen definieren die minimale und maximale Menge an CPU und Speicher, die ein Pod verwenden kann.

- **Beispiel**: Ein Pod mit einer CPU-Anforderung von 0.5 und einem Speicherlimit von 512 MiB.

#### Node-Auswahlkriterien

Node-Auswahlkriterien bestimmen, auf welchen Nodes ein Pod ausgeführt werden kann.

- **Beispiel**: Ein Pod mit einem NodeSelector, der sicherstellt, dass er nur auf Nodes mit dem Label "ssd=true" geplant wird.

#### Affinitäten und Anti-Affinitäten

Affinitäten und Anti-Affinitäten ermöglichen es, die Pod-Platzierung basierend auf Beziehungen zu anderen Pods oder Nodes zu steuern.

- **Beispiel**: Ein Pod mit einer Pod-Affinität, die sicherstellt, dass er nur auf Nodes geplant wird, auf denen sich bereits Pods mit einem bestimmten Label befinden.

### Zusammenfassung

Die Planungseinstellungen und -richtlinien in Kubernetes ermöglichen eine feine Steuerung der Pod-Platzierung und Ressourcennutzung im Cluster. Durch die Festlegung von Ressourcenanforderungen, Node-Auswahlkriterien und Affinitäten können Administratoren die Leistung, Zuverlässigkeit und Skalierbarkeit ihrer Anwendungen verbessern.
