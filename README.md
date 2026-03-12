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

## URL de acesso (Staging)

Após aplicar os manifests e configurar o DNS, o Metabase fica disponível em:

**https://metabase.stg.lbpay.com.br**

A variável `MB_SITE_URL` está configurada no deployment para redirects e cookies funcionarem corretamente.

**Configuração DNS:** Crie um registro CNAME `metabase.stg.lbpay.com.br` apontando para o hostname do ALB criado pelo Ingress (obtido com `kubectl get ingress -n analytics`).

## Instalação

```bash
kubectl apply -k base/
```

## Acesso

- **Dentro do cluster:** `http://metabase.analytics.svc.cluster.local`
- **Port-forward local:** `kubectl port-forward svc/metabase -n analytics 3000:80` → `http://localhost:3000`

Na primeira execução, o Metabase solicita a criação do usuário administrador.
