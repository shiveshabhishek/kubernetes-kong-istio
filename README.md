# kubernetes-kong-istio
# 🚀 Cloud-Native Kubernetes Network Lab: Kong Gateway & Istio Service Mesh

A hands-on engineering lab blueprint designed for DevOps engineers to learn, implement, and master end-to-end traffic management, zero-trust security, and observability inside a local **Kubernetes (KinD)** environment.

This project implements a production-grade dual-layer networking topology: **Kong API Gateway** handles perimeter edge routing (North-South) [Kong], while **Istio Service Mesh** manages, encrypts, and observes internal pod-to-pod workloads (East-West) [Istio].

```text
[ Public Internet ] ──( HTTP / Domain URL )──> [ Local /etc/hosts ]
                                                       │
                                            (North-South Perimeter)
                                                       ▼
                                             [ Kong API Gateway ]
                                                (Rate-Limiting)
                                                       │
                                            (East-West Mesh Tunnel)
                                                       ▼
                                            [ Istio Service Mesh ]
                                             🔒 Strict mTLS Pipeline
                                                       ├── frontend-app (Nginx)
                                                       └── backend-app (http-echo)
```

## 🛠️ Tech Stack & Infrastructure Framework
* **Kubernetes Cluster:** KinD (Kubernetes in Docker)
* **LoadBalancer Provider:** `cloud-provider-kind`
* **API Management (North-South):** Kong Gateway OSS (Deployed via Helm) [Kong]
* **Service Mesh (East-West):** Istio Service Mesh & Envoy Sidecar Proxies [Istio]
* **Observability Core:** Kiali Dashboard & Prometheus Engine [Istio]

---

## 📂 Repository Directory Architecture
The repository files are organized sequentially to match each phase of the deployment framework:

```text
kubernetes-kong-istio/
├── Part-2-Sample-App/
│   ├── backend-deploy.yaml       # Lightweight backend echo mock API service
│   └── frontend-deploy.yaml      # Nginx proxy frontend serving static asset portal
├── Part-3-Kong/
│   ├── values.yaml               # Custom configuration overrides for Kong core Helm chart
│   ├── kong-ingress.yaml         # Edge reverse-proxy routing rules mapping local domain
│   └── kong-rate-limiting.yaml   # KongPlugin applying API layer perimeter security
└── Part-4-Istio/
    ├── istio-strict-mtls.yaml    # PeerAuthentication enforcing cluster zero-trust bounds
    ├── kong-ui-exemption.yaml    # Targeted permissive fallback rule for local administration
    └── meshed-client.yaml        # Standard deployment workload sandbox for secure debugging
```

---

## 🎯 High-Value DevOps Learning Milestones Built-In
1. **The DB-less Architecture Pattern:** Learn how to manage edge gateways as immutable read-only components driven entirely by GitOps YAML states [Kong].
2. **Perimeter vs Mesh Boundaries:** Grasp the exact operational dividing line between API gateways (North-South) and service meshes (East-West) [Kong, Istio].
3. **Zero-Trust Hardening:** Witness connection packet behavior shift between unencrypted plaintext states and strict, authenticated mTLS pipelines [Istio].
4. **Live Observability Telemetry:** Experience active traffic mapping, metric aggregation, and protocol trace tracing via the Kiali topology engine [Istio].

---

## 🚀 Getting Started Quickstart
1. Spin up your local environment cluster using KinD.
2. Ensure your external traffic path is active by running `cloud-provider-kind`.
3. Map your host adapter domain: `sudo echo "YOUR_KONG_EXTERNAL_IP devops-project.local" >> /etc/hosts`.
4. Deploy each component subfolder sequentially using `kubectl apply -f <directory>/`.
