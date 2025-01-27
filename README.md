# Infraestrutura Redis - FrameVideo

Este repositório contém a configuração do Terraform para provisionar a infraestrutura Redis utilizada pelo serviço FrameVideo na AWS.

## Recursos Provisionados

- **Grupo de Subnet do Redis**: Configurado nas subnets sa-east-1a e sa-east-1b
- **Grupo de Replicação Redis**: 
  - Engine: Redis 7.0
  - Tipo de nó: cache.t3.micro
  - 2 clusters com failover automático
  - Multi-AZ habilitado
  - Grupo de parâmetros padrão Redis 7

- **Grupo de Segurança**:
  - Porta 6379 aberta para entrada
  - Todas as portas liberadas para saída

- **Secrets Manager**:
  - Armazena credenciais do Redis (host, porta)
  - Política IAM para acesso aos secrets

## Variáveis de Ambiente Necessárias

- `AWS_ACCESS_KEY_ID`: Chave de acesso AWS
- `AWS_SECRET_ACCESS_KEY`: Chave secreta AWS
- `AWS_REGION`: Região AWS (default: sa-east-1)

## Pipeline CI/CD

O repositório inclui um workflow do GitHub Actions que:

1. Inicializa o Terraform
2. Valida a formatação
3. Valida a configuração
4. Gera e aplica o plano de infraestrutura

## Outputs

- `redis_primary_endpoint`: Endpoint primário do Redis
- `redis_port`: Porta do Redis
- `secrets_policy`: ARN da política de secrets
- `secrets_id`: ID do secret no Secrets Manager
