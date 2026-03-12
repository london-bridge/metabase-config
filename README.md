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
├── ingress.yaml
└── kustomization.yaml
```

## URL de acesso (Dev)

**https://metabase.dev.lbpay.com.br**

A variável `MB_SITE_URL` está configurada no deployment para redirects e cookies funcionarem corretamente.

O Ingress usa ALB próprio com subnets da VPC dev. O DNS `metabase.dev.lbpay.com.br` está na zona privada Route53 `dev.lbpay.com.br` (conta dev) — requer VPN para resolução.

## Instalação

```bash
kubectl apply -k base/
```

## Acesso

- **Dentro do cluster:** `http://metabase.analytics.svc.cluster.local`
- **Port-forward local:** `kubectl port-forward svc/metabase -n analytics 3000:80` → `http://localhost:3000`

Na primeira execução, o Metabase solicita a criação do usuário administrador.
