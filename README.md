# metabase-config

Manifests Kubernetes para deploy do Metabase no EKS, baseados no docker-compose original.

## Estrutura

```
base/
├── namespace.yaml
├── pvc.yaml
├── metabase-db-deployment.yaml
├── metabase-db-service.yaml
├── metabase-deployment.yaml
├── metabase-service.yaml
└── kustomization.yaml
```

## Instalação

```bash
kubectl apply -k base/
```

## Acesso

- **Dentro do cluster:** `http://metabase.analytics.svc.cluster.local`
- **Port-forward local:** `kubectl port-forward svc/metabase -n analytics 3000:80` → `http://localhost:3000`

Na primeira execução, o Metabase solicita a criação do usuário administrador.
