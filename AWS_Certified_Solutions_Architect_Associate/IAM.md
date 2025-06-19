# Seção 3 – IAM (Identity and Access Management)

## 🔐 O que é o IAM?

O **AWS IAM (Identity and Access Management)** é o serviço que permite **criar e gerenciar usuários, grupos, funções (roles)** e **políticas de permissões** para controlar com segurança o acesso a recursos da AWS.

Com o IAM, é possível:

- Autenticar identidades (usuários e aplicações)
- Autorizar ações em recursos
- Controlar acesso centralizadamente
- Aplicar boas práticas de segurança (como MFA e princípio do menor privilégio)

---

## 👤 Formas de Acesso à AWS

Os usuários podem interagir com os serviços da AWS por três interfaces:

| Método     | Descrição                                      |
|------------|------------------------------------------------|
| Console    | Interface gráfica via navegador (Web GUI)      |
| CLI        | Linha de comando para execução de comandos     |
| API / SDKs | Acesso programático por aplicações ou scripts  |

Todas as chamadas passam por **autenticação IAM** antes de acessar qualquer recurso.

---

## 🧱 Principais Componentes do IAM

### 👤 Usuários (Users)
Entidades que representam pessoas ou aplicações. Cada usuário pode ter um login com senha (console) e/ou chaves de acesso (CLI/API).

### 👥 Grupos (Groups)
Conjuntos de usuários com permissões compartilhadas. Permite gerenciamento em escala.

### 🎭 Funções (Roles)
Entidades assumíveis por usuários ou serviços. Utilizadas para acesso temporário ou delegação segura. Ex: EC2 assumindo role para acessar S3.

### 🌐 Usuários Federados (Federated Users)
Usuários que vêm de fora do IAM (ex: Active Directory, Google, SAML). Recebem permissões ao assumirem uma role específica.

---

## 📖 Tipos de Políticas no IAM

As permissões são concedidas por meio de **políticas JSON** que determinam o que um principal (usuário, grupo ou role) pode fazer em quais recursos.

Existem dois tipos principais de política:

---

### 🧑‍💼 IBP – Identity-Based Policies

As **políticas baseadas em identidade** são associadas diretamente a usuários, grupos ou roles no IAM. Elas definem o que essas identidades podem fazer com recursos da AWS.

#### ✅ Exemplos de uso:
- Conceder acesso de leitura a um bucket S3
- Permitir que uma role de EC2 acesse DynamoDB

#### 📄 Exemplo JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

#### 📌 Características:
- Associadas a usuários, grupos ou roles
- Não possuem campo `"Principal"`
- Permitem granularidade com ações e condições

---

### 🗂️ RBP – Resource-Based Policies

As **políticas baseadas em recurso** são anexadas diretamente aos recursos da AWS. Elas definem quem (principal) pode acessar aquele recurso e o que pode fazer.

#### ✅ Exemplos de uso:
- Um bucket S3 permite leitura por uma role de outra conta
- Uma função Lambda permite ser invocada por um serviço específico

#### 📄 Exemplo JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111122223333:user/Luiz"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

#### 📌 Características:
- Associadas diretamente a recursos (como S3, Lambda, SNS)
- Possuem campo obrigatório `"Principal"`
- Suportam acesso **cross-account**

---

## 🔁 Comparativo: IBP vs RBP

| Característica                    | IBP (Identity-Based Policy)     | RBP (Resource-Based Policy)         |
|----------------------------------|----------------------------------|-------------------------------------|
| Aplicada a                       | Usuário, grupo ou role           | Recurso da AWS (ex: S3, Lambda)     |
| Campo `"Principal"` necessário   | ❌ Não                           | ✅ Sim                              |
| Uso para cross-account           | ⚠️ Indireto, via role            | ✅ Direto                           |
| Cenário comum                    | Conceder acesso a um usuário     | Compartilhar recurso com outra conta|
| Exemplo de uso                   | Role com acesso ao RDS           | Bucket S3 acessível externamente    |

---

## 🛡️ Boas Práticas com IAM (cobradas na certificação)

- 🚫 **Não use a conta root no dia a dia**
- 🔐 **Habilite MFA** para usuários administrativos
- 🧼 **Use políticas com menor privilégio possível**
- 🧠 **Prefira roles para serviços (EC2, Lambda, etc.)**
- 🧾 **Audite permissões com IAM Access Analyzer**
- 🔄 **Revogue permissões não utilizadas**
- 📅 **Use roles com duração limitada quando possível**

---

## 📝 Dica de Prova

A AWS frequentemente cobra cenários em que você precisa:

- Distinguir quando usar uma **IBP** ou **RBP**
- Saber como conceder acesso entre contas com segurança
- Aplicar o **modelo de segurança** de forma escalável e auditável
- Entender o papel das roles assumidas por serviços (STS)

> 📌 Sempre pergunte: **“Quem está acessando o quê, e de onde?”**
