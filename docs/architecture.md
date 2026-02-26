2️⃣ Documentação da Arquitetura (Markdown)

📘 Arquitetura On-Premises – Aplicativo de Descontos

🎯 Objetivo

Projetar uma arquitetura altamente disponível, segura e resiliente para um aplicativo de descontos operando em ambiente on-premises.

🧩 Componentes Principais
🔹 NGINX (API Gateway)

Funcao:
- Roteamento de requisições
- SSL Termination
- Rate Limiting
- Autenticação básica (opcional)
- Load Balancing

Alta disponibilidade:
- 2 ou mais instâncias
- Keepalived + VIP
- Health checks ativos

Segurança:
- TLS 1.2+
- Headers de segurança
- WAF opcional
- Mutual TLS interno

🔹 Redis (Cache de Leitura)

Funcao:
- Cache de descontos
- Redução de carga no PostgreSQL
- TTL para expiração automática

Alta disponibilidade:
- Redis Cluster (3 mestres + 3 réplicas)
- Sentinel para failover automático

Segurança:
- AUTH habilitado
- TLS interno
- Bind apenas rede privada

🔹 Kafka (Mensageria)

Funcao:
- Processamento assíncrono
- Eventos: criação de desconto, expiração, auditoria
- Integração com outros sistemas

Alta disponibilidade:
- Cluster com 3+ brokers
- Replication factor >= 3
- Zookeeper ou KRaft (modo moderno)

Segurança:
- SASL/SCRAM
- TLS
- ACL por tópico

🔹 PostgreSQL (Persistência)

Funcao:
- Base transacional principal
- Consistência ACID

Alta disponibilidade:
- Primary + 2 Réplicas
- Streaming Replication
- Patroni ou Repmgr
- Backup com WAL archiving

Segurança:
- SSL obrigatório
- pg_hba.conf restritivo
- Roles com privilégio mínimo
- Criptografia em disco (LUKS)

🔐 Segurança em Camadas
Camada	    Estratégia
Rede	      Segmentação VLAN
Perímetro	  Firewall + WAF
Aplicação	  Rate limiting
Dados	      TLS interno
Banco	      Roles mínimas
Auditoria	  Logs centralizados


♻️ Estratégias de Alta Disponibilidade

- Cluster em todas as camadas
- Failover automático
- Replicação síncrona (quando necessário)
- Health checks ativos
- Monitoramento (Prometheus + Grafana)
- Backups automatizados
