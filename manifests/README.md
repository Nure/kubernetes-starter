# Kubernetes Manifests

Sample manifests demonstrating core Kubernetes resources in the `nginx` namespace.

## Files

| File | Resource | Purpose |
| --- | --- | --- |
| [`namespace.yml`](./namespace.yml) | `Namespace` | Creates the `nginx` namespace (apply this first). |
| [`pod.yml`](./pod.yml) | `Pod` | Standalone Nginx pod (for learning single-pod deployment). |
| [`deployment.yml`](./deployment.yml) | `Deployment` | Manages 2 replicas of `nginx` (`app: nginx`). |
| [`service.yml`](./service.yml) | `Service` | Exposes `app: nginx` pods on port `80` via `NodePort`. |

## Usage

### 1. Create the Namespace

Always apply the namespace first so the remaining resources have a target namespace:

```bash
kubectl apply -f manifests/namespace.yml
```

### 2. Deploy Nginx and Expose It

For the recommended Deployment + Service workflow:

```bash
kubectl apply -f manifests/deployment.yml
kubectl apply -f manifests/service.yml
```

*(Optional)* To try a standalone pod instead of a Deployment:

```bash
kubectl apply -f manifests/pod.yml
```

### 3. Verify Resources

```bash
kubectl -n nginx get all
```

### 4. Access the Service

Use port-forwarding (works identically on both KIND and Minikube):

```bash
kubectl -n nginx port-forward svc/nginx-service 8080:80
```

Then visit `http://localhost:8080` (or run `curl http://localhost:8080`).

On **Minikube**, you can also open the `NodePort` service directly:

```bash
minikube service nginx-service -n nginx --url
```

### 5. Clean Up

Deleting the `nginx` namespace removes all resources created inside it:

```bash
kubectl delete namespace nginx
```
