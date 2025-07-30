# 🔵 ***Kubernetes Blue-Green Deployment with Kustomize***

This repository demonstrates a clean, production-style **Blue-Green Deployment strategy** using **Kustomize** for Kubernetes. It provides a minimal yet powerful example of how to manage multiple app versions (`blue` and `green`) with zero-downtime release capability and clean separation of environments.

## 🚀 ***What This Is***

A fully functional, GitOps-friendly Kubernetes deployment pattern using Kustomize overlays to deploy two versions (`blue` and `green`) of the same application in parallel.

You can easily switch traffic between versions by updating a label in the `Service` selector — all without disrupting running pods or users.

## 🎯 ***Why I Built This***

In modern DevOps and Platform Engineering, **safe, repeatable deployments** are crucial. Blue-Green is one of the most reliable deployment strategies for:
- Zero-downtime upgrades
- Easy rollback
- Clear separation between "current" and "next" versions

This repository was created to **demonstrate how simple and powerful Blue-Green deployment can be using native Kubernetes tools** like Kustomize — no Helm, no custom controllers, no vendor lock-in.

## 📁 ***Project Structure***

```bash
kustomize-bluegreen/
├── base/                # Base configuration (shared)
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
├── overlays/            # Environment-specific overlays
│   ├── blue/
│   │   ├── kustomization.yaml
│   │   └── patch.yaml
│   └── green/
│       ├── kustomization.yaml
│       └── patch.yaml
```

## ⚙️ ***How It Works***
- The base config defines a Deployment and Service for a simple web app (e.g., Nginx).
- Two overlays (blue and green) apply patches to create parallel environments.
- The Service is configured to select one version (blue or green) using a label selector.
- By updating the version in the Service, you can shift traffic between environments.

## ✅ ***Use Cases***
- Zero-downtime application deployments
- Safe production rollouts
- CI/CD pipelines with ArgoCD or Flux
- GitOps-style deployment workflows
- Easy rollback mechanisms

## 📦 ***How to Use***

1. ***Clone the Repository***

```bash
git clone https://github.com/your-username/kustomize-bluegreen.git
cd kustomize-bluegreen/kustomize-bluegreen
```
2. ***Deploy Blue Version***

```bash
kubectl apply -k overlays/blue/
```
3. ***Deploy Green Version***

```bash
kubectl apply -k overlays/green/
```
4. ***Switch Traffic (Service selector)***

Edit base/service.yaml:

```yaml
selector:
  app: my-app
  version: green   # ← change from blue to green

```
Then re-apply:

```bash
kubectl apply -k base/
```
5. ***Cleanup (optional)***

```bash
kubectl delete -k overlays/blue/
kubectl delete -k overlays/green/

```
## 🧩 ***Extend This***

- Add HPA support for autoscaling.
- Integrate with Ingress for external access.
- Use this pattern inside ArgoCD applications.
- Add automated promotion logic via CI/CD.
- Build Canary + Blue-Green hybrids for complex apps.

## 🛠 ***Tech Stack***

- Kubernetes
- Kustomize
- GitOps-ready folder structure
- Nginx (as placeholder workload)

## 🙌 ***Contributions Welcome***

Found something missing or have a better way to handle promotions? PRs and feedback are welcome! Feel free to fork, tweak, and contribute.

Built with ❤️ to make Kubernetes deployments safe and simple.

```yaml
Let me know if you'd also like a version of this for the Helm-based chart, or a `README.md` file with badges and example screenshots!
```