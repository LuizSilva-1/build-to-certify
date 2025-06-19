# Seção 5 – Armazenamento AWS (Amazon S3)

## 30. Introdução ao S3

O Amazon S3 (Simple Storage Service) é um serviço de armazenamento de objetos altamente escalável, seguro e durável.

- Armazena arquivos como objetos dentro de buckets.
- Cada objeto possui: chave (nome), valor (conteúdo), metadados e identificador de versão (se ativado).
- Suporta cargas de trabalho como backup, logs, websites estáticos, big data, etc.
- Durabilidade de 99.999999999% (11 9s) e alta disponibilidade.

---

## 31. Criando sua primeira Bucket

Buckets são os contêineres onde os objetos são armazenados.

- Nome globalmente único
- Escolha da região influencia latência e custo
- Configurações possíveis: versionamento, logs, criptografia, ACLs e políticas de bucket

---

## 32. Classes de Armazenamento do S3

O S3 oferece múltiplas classes de armazenamento, cada uma com finalidade e custo diferentes:

- **S3 Standard**: Acesso frequente, baixa latência, alta disponibilidade
- **S3 Intelligent-Tiering**: Otimiza custos automaticamente com base no uso
- **S3 Standard-IA**: Acesso esporádico, com menor custo e tarifa por recuperação
- **S3 One Zone-IA**: Igual ao Standard-IA, mas com dados em apenas uma AZ
- **S3 Glacier**: Arquivamento, recuperação em minutos ou horas
- **S3 Glacier Deep Archive**: Arquivamento de longo prazo, recuperação em até 12h

---

## 33. Valores do S3

Cada bucket/objeto pode ter configurações como:

- Versionamento
- Replicação
- Criptografia (SSE-S3, SSE-KMS, SSE-C)
- Logging
- Ciclo de vida (lifecycle)
- ACL e políticas (IAM, bucket policies)

---

## 34. Alterando a Classe de Armazenamento no S3

Você pode alterar manualmente a classe de armazenamento de um objeto ou configurar regras de ciclo de vida para isso.

---

## 35–37. Versionamento no S3

- **Versionamento** permite manter múltiplas versões de um objeto.
- Útil para proteção contra exclusões acidentais.
- Excluir um objeto versionado na verdade cria um marcador de exclusão.
- Permite restaurar versões anteriores.

---

## 38. Server Access Logging

- Registra requisições feitas a objetos e buckets
- Logs são enviados para outro bucket
- Útil para auditoria e análise de acesso

---

## 39–40. Hospedando um Website no S3

- Buckets podem ser usados para hospedar **sites estáticos**
- Requer habilitar o modo de hospedagem estática
- O nome do bucket deve ser igual ao domínio (opcional com Route 53)
- Requer permissões públicas (com atenção à segurança)

---

## 41. Habilitando o Ciclo de Vida no S3

- Permite definir **regras automáticas** para arquivamento ou exclusão de objetos com base na idade
- Exemplo: mover para Glacier após 30 dias, excluir após 365 dias

---

## 42. Replicação de Objetos

- Permite replicar objetos automaticamente de um bucket para outro (mesma ou outra região)
- Tipos:
  - CRR: Cross-Region Replication
  - SRR: Same-Region Replication
- Requer versionamento habilitado

---

## 43–44. IAM Policy vs Bucket Policy

- **IAM Policy**: Define o que usuários/roles podem fazer nos buckets (identidade → recurso)
- **Bucket Policy**: Define quem pode acessar o bucket (recurso → identidade), suporta acesso público e entre contas

---

## 45–46. ACL (Access Control List)

- ACLs são mecanismos legados de controle de acesso por objeto ou bucket
- Devem ser evitadas em novos projetos
- Permitem permissões granulares por conta ou usuários específicos

---

## 47–48. S3 Encryption

Três métodos de criptografia no S3:

- **SSE-S3**: Gerenciado pela AWS
- **SSE-KMS**: Integração com AWS KMS (chaves customizadas)
- **SSE-C**: Chaves fornecidas pelo cliente (não armazenadas na AWS)

Também é possível criptografar no lado do cliente antes do upload.

---

## 49. Simulado – S3 e CloudFront

Questões comuns cobradas sobre:

- Escolha de classes de armazenamento
- Controle de acesso (IAM vs bucket policy vs ACL)
- Versionamento, replicação e ciclo de vida
- Hospedagem de site estático
- Criptografia e compliance
- Integração com CloudFront para distribuição de conteúdo

---

## ✅ Dicas para a Prova

- **Versionamento** não é reversível
- **S3 Standard-IA** cobra por recuperação de dados
- **Glacier Deep Archive** tem maior tempo de recuperação, mas menor custo
- **Use Bucket Policy para acesso entre contas**
- **S3 não é sistema de arquivos – é armazenamento de objetos**
- **Sempre preferir policies ao invés de ACLs**
