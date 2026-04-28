# Relatório Challenge CEAP - Fases 1 e 2 🦊🔍
**Planejamento, Proposta Detalhada e Mapeamento Operacional**

Este repositório contém a documentação da fase inicial de avaliação de segurança autorizada no alvo `dev.pedreira.org`. O trabalho consiste num **Vulnerability Assessment Passivo**, estruturando o escopo, metodologia e o mapeamento técnico da infraestrutura (reconhecimento).

## 👥 Grupo Purplefox Security
* **Regis Ramos Pinheiro** – RM 567534
* **Thomás Henrique Pandolfo de Campos** – RM 567744
* **Suzana Maciel da Silva** – RM 566914
* **Dyego de Souza Evaristo** – RM 566801
* **Marcello Paixão da Cruz** – RM 567205

---

## 🎯 1. Introdução e Proposta Detalhada (Fase 1)

O objetivo principal desta fase foi estabelecer a base técnica e metodológica para a futura execução de testes éticos em ambiente de homologação. A defesa proativa exige a identificação antecipada de falhas, garantindo a redução de riscos, a conformidade com a LGPD (Lei nº 13.709/2018) e a validação das configurações de segurança.

### 📚 Metodologia Aplicada
A abordagem baseia-se nos seguintes padrões da indústria de cibersegurança:
* **PTES** (Penetration Testing Execution Standard)
* **NIST SP 800-115**
* **OWASP Testing Guide**

### 🛡️ Escopo e Limites
O trabalho consiste estritamente em **Reconhecimento Passivo**, sem interação agressiva ou ações intrusivas.

| Classificação | Atividade |
| :--- | :--- |
| ✅ **Permitida** | Análise de registros DNS |
| ✅ **Permitida** | Fingerprinting por headers HTTP |
| ✅ **Permitida** | Identificação de tecnologias |
| ✅ **Permitida** | Mapeamento passivo de subdomínios |
| ✅ **Permitida** | Verificação de certificado TLS |
| ❌ **Proibida** | Exploração de vulnerabilidades |
| ❌ **Proibida** | Injeção de dados (SQLi, XSS etc.) |
| ❌ **Proibida** | Aumento de impacto ou privilégio |
| ❌ **Proibida** | Qualquer ação que modifique dados |

### 🛠️ Ferramentas Utilizadas
| Ferramenta / Framework | Finalidade |
| :--- | :--- |
| **Whois** | Consulta de registros de domínio e IP |
| **Dig** | Análise de registros DNS |
| **Curl** | Fingerprinting de headers HTTP |
| **Nmap** *(modo seguro)* | Verificação de certificados SSL/TLS |
| **Crt.sh / Amass** | Enumeração passiva de subdomínios |
| **DevTools (F12)** | Análise de headers e comportamento web |

---

## 🗺️ 2. Mapeamento do Ambiente (Fase 2)

### 2.1 Análise WHOIS
Foram realizadas consultas WHOIS para identificar os responsáveis pelo domínio e pela infraestrutura física do IP.

**Domínio (`pedreira.org`)**
* **Registrar:** eNom, LLC (IANA 48)
* **Registry:** PIR – Public Interest Registry
* **DNS:** Cloudflare
* **DNSSEC:** Unsigned
* **Validade:** 08/04/2008 a 08/04/2026

**Infraestrutura (IP `177.190.193.105`)**
* **Alocado a:** CTINET Soluções – Brasil
* **Contato:** registro.br@cti.com.br

### 2.2 Análise de DNS (`dig`)
O mapeamento DNS revelou a estrutura de roteamento e as políticas de e-mail do domínio alvo:

| Item | Detalhe |
| :--- | :--- |
| **IP Real (A)** | `177.190.193.105` |
| **CNAME** | `ceap.dyndns.org` |
| **Autoridade (NS)** | Cloudflare |
| **E-mails (MX)** | smtp.google.com (Google Workspace) |
| **Segurança E-mail** | **SPF:** Configurado \| **DKIM:** Ausente \| **DMARC:** Ausente |

### 2.3 Enumeração de Subdomínios (Força Bruta Passiva)
Através de iterações passivas com listas comuns de subdomínios, identificou-se a seguinte superfície:
* `www.pedreira.org` (Resposta: Cloudflare)
* `dev.pedreira.org` (Resposta: ceap.dyndns.org)
* *Demais (api, test, mail, vpn, admin, etc):* Sem resposta.

### 2.4 Fingerprinting Web (cURL)
* **`http://dev.pedreira.org`** ➡️ Redirecionamento 302 para HTTPS.
* **`https://dev.pedreira.org/dev`** ➡️ Redirecionamento interno para a aplicação.
* **Comportamento Geral:** Server headers minimalistas e HSTS (HTTP Strict Transport Security) ativo.

### 2.5 Verificação Criptográfica (Nmap SSL/TLS)
A verificação passiva na porta `443` confirmou boas práticas de encriptação na infraestrutura:
* **Validade do Certificado:** 2025 – 2026 (Emitido por *GlobalSign*)
* **Versão TLS:** TLS 1.3 suportado
* **Suítes de Cifra:** AES-GCM / CHACHA20 (Boa segurança)

### 2.6 Descobertas: HAProxy e Exposição de Endpoint
A enumeração revelou a exposição do endpoint `/metrics` do HAProxy/Tomcat sem autenticação. Embora não permita acesso direto ao sistema de arquivos, vaza informações estruturais críticas:

| Alerta | Descrição | Risco / Causa |
| :--- | :--- | :--- |
| **Versão Exposta** | Apache Tomcat 9.0.93.0 visível publicamente. | Pode facilitar a busca direcionada por CVEs (Exploits). |
| **Erros no Tomcat** | Alta proporção de requisições com erro (404). | Indica possível varredura de bots/scanners ou *health check* mal configurado. |
| **Garbage Collector** | 10x mais coletas pesadas do que leves (G1 GC). | Comportamento anómalo, indicando possível vazamento de memória (Memory Leak). |

---

## 🏁 3. Considerações Finais
As Fases 1 e 2 foram concluídas com sucesso, estabelecendo os fundamentos metodológicos e documentando integralmente a superfície de ataque inicial sem impacto no ambiente.

A infraestrutura apresenta bons níveis básicos de segurança (TLS 1.3, redirecionamentos seguros e HSTS). Contudo, a ausência de assinaturas de e-mail avançadas (**DKIM e DMARC**) e o vazamento de métricas internas no endpoint **`/metrics`** representam pontos de atenção significativos. 

O projeto avançará para as **Fases 3 e 4**, onde testes controlados e ativos focarão na validação destas descobertas e na procura por vulnerabilidades mais profundas.
