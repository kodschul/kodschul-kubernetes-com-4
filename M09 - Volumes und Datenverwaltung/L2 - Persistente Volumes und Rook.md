## Kubernetes: Persistente Volumes und Rook

In Kubernetes ermöglichen Persistente Volumes (PVs) die Speicherung von Daten über den Lebenszyklus von Pods und Containern hinweg. Rook ist eine Kubernetes-Native Storage-Orchestrierung, die es ermöglicht, komplexe Speicherlösungen wie Ceph in Kubernetes-Clustern bereitzustellen und zu verwalten. Im Folgenden sind einige grundlegende Konzepte und Verwendungen von Persistente Volumes und Rook in Kubernetes beschrieben:

### Persistente Volumes (PVs)

Persistente Volumes (PVs) sind Speicherressourcen in einem Kubernetes-Cluster, die unabhängig von Pods existieren und über deren Lebenszyklus hinweg bestehen bleiben. PVs ermöglichen es, Daten zwischen verschiedenen Pods und Containern zu teilen und persistent zu speichern.

#### Grundlegende Konzepte

- **PersistentVolume (PV)**: Eine Speicherressource im Kubernetes-Cluster.
- **PersistentVolumeClaim (PVC)**: Eine Anforderung eines Pods nach einem PersistentVolume.
- **StorageClass**: Eine Möglichkeit, Speicherprovisionierungsdetails zu definieren.

#### Beispiel 1: Erstellen eines Persistente Volumes

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: slow
  hostPath:
    path: "/mnt/data"
```

In diesem Beispiel wird ein Persistente Volume definiert, das auf einem Hostpfad basiert.

#### Beispiel 2: Anfordern eines Persistente Volumes

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

In diesem Beispiel fordert ein Pod über eine Persistente Volume Claim die Bereitstellung von Speicher an.

### Rook
Rook ist eine Kubernetes-Native Storage-Orchestrierung, die es ermöglicht, komplexe Speicherlösungen wie Ceph in Kubernetes-Clustern bereitzustellen und zu verwalten. Rook automatisiert die Bereitstellung, Skalierung und Wartung von Speicherressourcen und integriert sich nahtlos in Kubernetes.

### Grundlegende Konzepte
Ceph: Ein verteiltes Speichersystem, das von Rook bereitgestellt wird.
Cluster: Ein Rook-Cluster, der mehrere Ceph-Knoten umfasst.
Pool: Eine logische Gruppierung von Speicherressourcen in einem Ceph-Cluster.
StorageClass: Eine Möglichkeit, Speicherprovisionierungsdetails zu definieren.

#### Beispiel 3: Bereitstellen von Rook mit Ceph
```yaml
apiVersion: ceph.rook.io/v1
kind: CephCluster
metadata:
  name: rook-ceph
spec:
  dataDirHostPath: "/var/lib/rook"
  mon:
    count: 3
    allowMultiplePerNode: false
  dashboard:
    enabled: true
  storage:
    useAllNodes: true
    useAllDevices: false
    deviceFilter:
      location: "/*"
    config:
      storeType: bluestore
```

In diesem Beispiel wird ein Rook-Cluster mit Ceph bereitgestellt.

#### Beispiel 4: Erstellen einer Rook StorageClass

```yaml
apiVersion: ceph.rook.io/v1
kind: CephBlockPool
metadata:
  name: replicapool
spec:
  replicated:
    size: 3
---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
   name: rook-ceph-block
provisioner: rook-ceph.rbd.csi.ceph.com
parameters:
    pool: replicapool
    clusterNamespace: rook-ceph
```

In diesem Beispiel wird eine StorageClass für Rook erstellt, um PersistentVolumeClaims zu bedienen.

Zusammenfassung
Persistente Volumes und Rook ermöglichen es, persistente Speicherressourcen in Kubernetes-Clustern bereitzustellen und zu verwalten. PVs bieten eine einfache Möglichkeit, Daten über den Lebenszyklus von Pods hinweg zu speichern, während Rook komplexe Speicherlösungen wie Ceph nahtlos in Kubernetes integriert. Durch die Kombination von PVs und Rook können Kubernetes-Benutzer hochverfügbaren und skalierbaren Speicher für ihre Anwendungen bereitstellen.