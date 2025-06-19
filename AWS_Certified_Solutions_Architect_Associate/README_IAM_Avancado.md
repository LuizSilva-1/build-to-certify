# Seção 4 – IAM e Access Management

## 18. Introdução ao IAM

O IAM (Identity and Access Management) é o serviço central da AWS para controle de identidades e permissões. Ele permite:

- Criar usuários, grupos e roles
- Aplicar políticas (policies) para controlar acesso
- Autenticar e autorizar chamadas à API
- Gerenciar acesso seguro baseado em boas práticas

---

## 19. Entendendo sobre Usuários, Grupos e Políticas

- **Usuários IAM**: Representam indivíduos ou aplicações. Cada usuário pode ter acesso via console, CLI ou API.
- **Grupos IAM**: Coleções de usuários com permissões comuns.
- **Políticas IAM**: Arquivos JSON que definem permissões. Podem ser anexadas a usuários, grupos ou roles.

---

## 20. Criar um Usuário no IAM

Ao criar um usuário, você define:
- Nome do usuário
- Tipo de acesso (console, programático)
- Permissões iniciais (diretamente, via grupo ou role)
- Tags e configurações adicionais

---

## 21. Aplicando uma Política ao Usuário

É possível anexar políticas diretamente ao usuário ou através de grupos. Exemplo de política simples para S3:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::meu-bucket"
  }]
}
```

---

## 22. Entendendo sobre o Processo de Autenticação

- A autenticação pode ocorrer via login no console, uso de chaves de acesso na CLI ou tokens temporários via STS.
- Após a autenticação, a autorização verifica as permissões por meio das políticas.

---

## 23. Sobre o MFA

O **Multi-Factor Authentication (MFA)** adiciona uma camada extra de segurança. Ele exige que o usuário insira um segundo fator (como código temporário) além da senha.

---

## 24. Habilitando MFA

Pode ser habilitado para:
- Conta root
- Usuários IAM

Tipos de dispositivos MFA:
- Virtual (como Google Authenticator)
- Hardware (chaves físicas)
- U2F/FIDO (chaves de segurança USB)

---

## 25. Utilizando o STS

O **AWS STS (Security Token Service)** é um serviço que permite criar **credenciais temporárias** para acessar recursos da AWS. Essas credenciais funcionam como se fossem chaves de acesso normais, mas com **tempo de vida limitado**.

### 🔐 Quando usar o STS?

| Situação | Exemplo |
|----------|---------|
| Delegar acesso entre contas AWS | Conta A cria uma role que a conta B pode assumir |
| Acesso federado (AD, SAML, Google) | Usuário externo assume uma role na AWS |
| Aplicação externa/móvel acessa a AWS | Token temporário gerado para acesso controlado |
| MFA exigido para uma sessão temporária | Geração com `GetSessionToken` |

---

### 🧪 Principais operações do STS

#### 1. `AssumeRole`
Permite que uma entidade (usuário, serviço) **assuma temporariamente uma role**.

```bash
aws sts assume-role \
  --role-arn arn:aws:iam::123456789012:role/RoleAcessoS3 \
  --role-session-name SessaoTeste
```

Retorna um bloco de credenciais temporárias que podem ser usadas em `aws configure`.

#### 2. `AssumeRoleWithSAML`
Usado para **acesso federado** com provedores SAML (como ADFS, Google Workspace, etc.).

#### 3. `GetSessionToken`
Gera credenciais temporárias para um usuário IAM **autenticado via MFA**.

```bash
aws sts get-session-token \
  --serial-number arn:aws:iam::123456789012:mfa/luiz \
  --token-code 123456
```

#### 4. `GetFederationToken`
Gera um token temporário para um **usuário não IAM**, útil para aplicações web/mobile externas.

---

### 📦 Exemplo real (Cross-account Access com STS)

1. Na **Conta A**, crie uma role com política de confiança (`trust policy`) permitindo ser assumida por Conta B.
2. Na **Conta B**, chame `assume-role`.
3. Use as credenciais retornadas para acessar, por exemplo, um bucket S3 da Conta A.

---

### 🛡️ Boas práticas com STS

- Limite a duração da sessão (padrão: 1h, máximo: 12h)
- Combine com MFA para maior segurança
- Nunca use STS para substituir roles permanentes em serviços internos

---

### 🎯 Dicas para a prova

- Acesso entre contas → `AssumeRole`
- MFA + sessão temporária → `GetSessionToken`
- Login com SAML (AD/Google) → `AssumeRoleWithSAML`
- Usuário externo temporário → `GetFederationToken`

---

## 26. Alterando a Política de Senhas no IAM

A AWS permite definir políticas de senha como:
- Comprimento mínimo
- Requisitos de complexidade (números, maiúsculas, símbolos)
- Validade da senha e histórico

---

## 27. Políticas de Recurso e Identidade

- **Identity-Based Policies (IBP)**: Ligadas a usuários, grupos e roles
- **Resource-Based Policies (RBP)**: Ligadas a recursos como S3, Lambda, etc.
- Importante para controle de acesso entre contas (cross-account access)

---

## 28. A Estrutura das Policies

Uma policy é composta por:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow" | "Deny",
    "Action": "serviço:ação",
    "Resource": "arn:aws:...",
    "Condition": { ... }
  }]
}
```

Campos principais:
- **Effect**: Permitir ou negar
- **Action**: Ações permitidas
- **Resource**: Alvo da permissão
- **Condition**: Filtros adicionais (ex: IP, MFA)

---

## 29. Boas Práticas para o IAM

- Não usar a conta root para operações do dia a dia
- Habilitar MFA sempre que possível
- Seguir o princípio do menor privilégio
- Revisar permissões com frequência
- Preferir roles para acesso entre serviços
- Utilizar grupos para gerenciamento escalável
