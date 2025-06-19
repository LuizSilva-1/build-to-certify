# Seção 3 – A Amazon AWS

## 12. A Infraestrutura da Amazon AWS

A infraestrutura global da AWS foi projetada para oferecer alta disponibilidade, tolerância a falhas, escalabilidade e baixa latência. Ela é composta por:

- **Regiões (Regions)**
- **Zonas de Disponibilidade (Availability Zones)**
- **Zonas Locais (Local Zones)**
- **AWS Wavelength**
- **AWS Outposts**

---

## 13. As Regiões (Regions)

Uma **Região AWS** é uma área geográfica física onde a AWS possui múltiplos data centers agrupados. Cada região contém pelo menos duas zonas de disponibilidade.

- Exemplo: `us-east-1` (Norte da Virgínia), `sa-east-1` (São Paulo)
- As regiões são isoladas umas das outras para oferecer tolerância a falhas e independência.

---

## 14. Zonas de Disponibilidade (Availability Zones - AZs)

Cada **zona de disponibilidade** é composta por um ou mais data centers físicos com energia, refrigeração e rede redundantes.

- Elas estão interconectadas por redes de alta velocidade e baixa latência.
- São projetadas para operar de forma independente e evitar falhas em cascata.
- Ao distribuir recursos entre AZs, você aumenta a disponibilidade da aplicação.

---

## 15. Zonas Locais (Local Zones)

As **Zonas Locais** são extensões das regiões da AWS que colocam serviços de computação, armazenamento e banco de dados **mais próximas dos usuários finais em grandes áreas metropolitanas**.

- Reduzem a latência para aplicações que exigem resposta rápida (ex: jogos, streaming, edição de vídeo).
- São ideais para workloads que exigem baixa latência mas que não podem ser executadas em data centers próprios.
- Exemplo de uso: um estúdio de cinema que edita vídeos em tempo real próximo a Los Angeles.

---

## 16. AWS Wavelength

O **AWS Wavelength** integra os serviços da AWS diretamente às redes **5G de operadoras de telecomunicações**, reduzindo drasticamente a latência para aplicações móveis e IoT.

- Usado para entregar experiências imersivas como realidade aumentada, jogos móveis e carros autônomos.
- Os servidores Wavelength rodam dentro das redes 5G das operadoras, próximos ao usuário final.
- A comunicação entre instâncias no Wavelength e na região da AWS ocorre com latência mínima.

📌 **Importante para prova**: Wavelength é voltado para aplicações que **exigem latência ultra baixa** (<10 ms), normalmente em cenários móveis.

---

## 17. AWS Outposts

O **AWS Outposts** leva a infraestrutura da AWS **para dentro do seu data center local**, oferecendo uma **extensão física da nuvem da AWS on-premises**.

- Ideal para clientes que precisam manter parte da carga de trabalho local por razões de compliance, latência ou dependências técnicas.
- Você pode usar os mesmos serviços da AWS (como EC2, EBS, RDS) diretamente em seu ambiente local, com gerenciamento centralizado.
- AWS instala e gerencia fisicamente os Outposts no local do cliente.

📌 **Importante para prova**: Outposts é a solução híbrida da AWS quando a nuvem pública **não é suficiente sozinha**.

---

## ✅ Resumo Comparativo

| Recurso          | Finalidade                                        | Latência        | Localização      |
|------------------|---------------------------------------------------|------------------|------------------|
| Regiões          | Isolamento geográfico de recursos                 | Alta             | Global           |
| Zonas de Disponibilidade | Alta disponibilidade e redundância         | Baixa            | Dentro da região |
| Zonas Locais     | Baixa latência para áreas metropolitanas          | Muito baixa      | Próximo do cliente |
| AWS Wavelength   | Latência ultrabaixa para apps 5G                  | Ultra baixa (<10ms) | Rede 5G          |
| AWS Outposts     | Solução híbrida local + nuvem AWS                 | Variável         | Dentro do data center do cliente |
