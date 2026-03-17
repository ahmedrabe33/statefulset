# Kubernetes StatefulSet Lab 🚀

This project demonstrates how to deploy a **StatefulSet** in Kubernetes using:

* StorageClass
* Headless Service
* Persistent Volume Claims (PVC)
* StatefulSet


!(/images/stf.png)

## 📦 Components

### 1. StorageClass

* Custom StorageClass named `my-storage`
* Uses Minikube hostPath provisioner
* Supports volume expansion
* Retains data even after deletion

### 2. Headless Service

* Service name: `nginx`
* `clusterIP: None` (Headless)
* Enables stable network identities for Pods

### 3. StatefulSet

* Name: `web`
* Replicas: 3 Pods (`nginx-0`, `nginx-1`, `nginx-2`)
* Each Pod gets:

  * Unique identity
  * Dedicated PVC
  * Persistent storage

---

## ⚙️ How It Works

* Each Pod mounts a volume at:

  ```
  /usr/share/nginx/html
  ```

* Kubernetes automatically creates a **PVC for each Pod**:

  ```
  www-web-0
  www-web-1
  www-web-2
  ```

* These PVCs are backed by the defined StorageClass.

---

## 🧪 Experiment

### Step 1: Create a file inside a Pod

```bash
kubectl exec -it web-0 -- sh -c "echo hello > /usr/share/nginx/html/test.txt"
```

### Step 2: Delete the Pod

```bash
kubectl delete pod web-0
```

### Step 3: Verify Pod recreation

```bash
kubectl get pods
```

### Step 4: Check the file again

```bash
kubectl exec web-0 -- cat /usr/share/nginx/html/test.txt
```

✅ Result: The file still exists!

---

## 🔥 Key Learnings

* StatefulSet provides **stable Pod identities**
* Each Pod has its own **persistent storage (PVC)**
* Data is **not lost** after Pod deletion
* Pods are created in **ordered sequence**
* Works with **Headless Service** for stable networking

---

## 📌 Use Cases

* Databases (MySQL, PostgreSQL)
* Distributed systems
* Applications requiring persistent storage

---

## 🛠️ Tech Stack

* Kubernetes
* Minikube
* NGINX

---

## 💡 Notes

* Storage is local (Minikube), not production-ready
* `Retain` policy ensures data is preserved after PVC deletion
* Each Pod is tightly coupled with its volume

---

## 📎 Author

Hands-on Kubernetes learner exploring Stateful Applications 💪
