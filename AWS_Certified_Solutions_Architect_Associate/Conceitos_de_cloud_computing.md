## Seção 2 – Conceitos de Cloud Computing

### ☁️ O que é Cloud Computing?

Cloud Computing é um modelo de entrega de recursos de computação sob demanda via internet, com pagamento conforme o uso. Esses recursos podem incluir:

- Servidores virtuais (como EC2)
- Armazenamento (como S3)
- Bancos de dados (como RDS)
- Redes, segurança, ferramentas de machine learning, entre outros

A computação em nuvem permite que empresas evitem o gerenciamento de data centers locais (on-premises), reduzindo custos com:

- Hardware físico
- Energia elétrica
- Climatização
- Equipes técnicas locais
- Segurança física

---

### 📦 Modelos de Serviço em Cloud

A AWS oferece diferentes modelos de serviço, cada um com um nível diferente de responsabilidade do cliente e da AWS.

#### 🧱 IaaS – Infrastructure as a Service

> Você gerencia: sistema operacional, aplicações, dados e configurações  
> A AWS gerencia: hardware, rede, virtualização, segurança física

**Exemplos na AWS:** EC2, EBS, VPC

---

#### ⚙️ PaaS – Platform as a Service

> Você gerencia: apenas o código da aplicação  
> A AWS gerencia: infraestrutura, sistema operacional, runtime, patching

**Exemplos na AWS:** Elastic Beanstalk, AWS App Runner, RDS

---

#### 🧑‍💼 SaaS – Software as a Service

> Você apenas consome a aplicação  
> A AWS (ou o provedor) gerencia tudo

**Exemplos:** Amazon Chime, Office 365, Salesforce

---

### 🔐 Modelo de Responsabilidade Compartilhada (Shared Responsibility Model)

Na AWS, a segurança é responsabilidade compartilhada:

| Responsabilidade | Cliente | AWS |
|------------------|---------|-----|
| Configuração de segurança | ✅ | ❌ |
| Dados e permissões (IAM) | ✅ | ❌ |
| Sistema operacional (no EC2) | ✅ | ❌ |
| Infraestrutura física | ❌ | ✅ |
| Segurança da rede física | ❌ | ✅ |

---

### 🏢 Comparativo: On-Premises vs Cloud

| Item                          | On-Premises             | Cloud (AWS)                 |
|-------------------------------|--------------------------|-----------------------------|
| Compra de hardware            | Responsável              | Não necessário              |
| Instalação de sistemas        | Responsável              | Automatizado pela AWS       |
| Manutenção física             | Responsável              | Gerenciada pela AWS         |
| Escalabilidade                | Limitada                 | Sob demanda (auto scaling)  |
| Investimento inicial (CAPEX) | Alto                     | Reduzido (modelo OPEX)      |

---

### ✅ Benefícios da Computação em Nuvem

- **Elasticidade:** aumenta ou diminui recursos conforme a demanda
- **Escalabilidade:** cresce com o seu negócio
- **Alta disponibilidade:** infraestrutura distribuída globalmente
- **Redução de custos operacionais**
- **Agilidade na entrega de serviços**
- **Modelo "pay as you go"**: pague apenas pelo que usar

---

> 🔍 *Outros temas como billing, regions e serviços específicos serão abordados em seções futuras.*
