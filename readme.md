# 🔐 Kubernetes Persistent Volume Demo

Ce projet montre comment utiliser un **volume persistant (PersistentVolume + PersistentVolumeClaim)** dans Kubernetes pour conserver des données même après la suppression et le redéploiement d’un Pod.

---

## 🧠 Objectif

Créer un Pod qui utilise un volume monté sur `/data`, écrire un fichier dans ce répertoire, redémarrer le Pod, et vérifier que les données sont toujours présentes.

---

## 📁 Fichiers

| Fichier                 | Description                                 |
|-------------------------|---------------------------------------------|
| `pv.yaml`               | Définition du Persistent Volume (PV)        |
| `pvc.yaml`              | Définition du Persistent Volume Claim (PVC) |
| `pod-with-volume.yaml`  | Pod utilisant le PVC pour monter un volume  |

---

## 🧪 Étapes pour tester

### 1. Appliquer le Persistent Volume (PV)
```bash
kubectl apply -f pv.yaml
```

### 2. Appliquer le Persistent Volume Claim (PVC)
```bash
kubectl apply -f pvc.yaml
```

### 3. Déployer le Pod
```bash
kubectl apply -f pod-with-volume.yaml
```

### 4. Entrer dans le Pod
```bash
kubectl exec -it volume-demo-pod -- sh
```

### 5. Créer un fichier dans le volume
```bash
echo "Hello from Douae!" > /data/test.txt
exit
```

### 6. Supprimer et recréer le Pod
```bash
kubectl delete pod volume-demo-pod
kubectl apply -f pod-with-volume.yaml
```

### 7. Vérifier la persistance des données
```bash
kubectl exec -it volume-demo-pod -- sh
cat /data/test.txt
```

✅ **Résultat attendu** : le message `"Hello from Douae!"` s'affiche, ce qui prouve que le fichier est toujours là après le redéploiement.