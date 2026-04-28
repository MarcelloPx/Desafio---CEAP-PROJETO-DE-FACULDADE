# Relatório de Exploração Web | Challenge CEAP - Fase 3 🦊🔍

[cite_start]Este repositório contém o **Relatório Técnico de Teste de Intrusão** e Exploração Web realizado na aplicação `dev.pedreira.org`[cite: 3129, 3130]. [cite_start]O projeto integra a Fase 3 do Challenge CEAP do curso de Defesa Cibernética da FIAP[cite: 3128, 3131].

## 🎯 Objetivo e Escopo
[cite_start]O escopo da avaliação englobou as fases de Reconhecimento, Análise de Vulnerabilidades Web e Enumeração de Superfície[cite: 3130].
* [cite_start]**Alvo Avaliado:** `dev.pedreira.org` (Diretório `/devSecurityG5/`)[cite: 3130].
* [cite_start]**Metodologia:** OWASP Top 10, CVSS v3.1, PTES[cite: 3130].
* [cite_start]**Compliance Avaliado:** LGPD (Lei 13.709/2018), ISO/IEC 27001, NIST SP 800-115[cite: 3130].

## 🛠️ Ferramentas Utilizadas
[cite_start]Os testes foram executados a partir de um ambiente Kali Linux (Máquina Virtual)[cite: 3130], utilizando o seguinte arsenal de segurança:
* [cite_start]Nmap, Nikto, ffuf, dirsearch, OWASP ZAP, Burp Suite, curl, Netcat[cite: 3130].

## 🚨 Vulnerabilidades Identificadas
[cite_start]Durante a análise, não foram identificadas vulnerabilidades críticas isoladas[cite: 3152]. [cite_start]No entanto, a combinação de fragilidades de severidade baixa e média gera um cenário real de risco e de potencial comprometimento de sessões[cite: 3144, 3153]:

| Vulnerabilidade | CVSS v3.1 | Severidade |
| :--- | :--- | :--- |
| **Biblioteca jQuery 1.11.3 com CVEs conhecidos** | 6.1 | [cite_start]MÉDIA | [cite: 3151]
| **Ausência de Headers de Segurança HTTP** | 5.3 | [cite_start]MÉDIA | [cite: 3151]
| **Endpoint `/metrics` exposto sem autenticação** | 5.3 | [cite_start]MÉDIA | [cite: 3151]
| **Ausência de Subresource Integrity (SRI)** | 5.0 | [cite_start]MÉDIA | [cite: 3151]
| **Cookie sem atributo SameSite** | 4.3 | [cite_start]BAIXA | [cite: 3151]
| **Cookie sem flag HttpOnly (ESR)** | 4.0 | [cite_start]BAIXA/MÉDIA | [cite: 3151]

## 🛡️ Plano de Ação Recomendado (Mitigação)
[cite_start]Para reduzir a superfície de ataque e garantir a conformidade com as normas aplicáveis, as seguintes ações de **Prioridade Alta** são recomendadas[cite: 3900]:
1. [cite_start]**CSP:** Implementar Content-Security-Policy (CSP) em todos os headers de resposta[cite: 3901].
2. [cite_start]**Proteção de Sessão:** Ativar a flag HttpOnly em todos os cookies de sessão[cite: 3902].
3. [cite_start]**Atualização de Bibliotecas:** Atualizar o jQuery da versão 1.11.3 para a versão 3.7.x ou superior[cite: 3903].
4. [cite_start]**Controlo de Acesso:** Restringir o acesso ao endpoint `/metrics` exigindo autenticação[cite: 3904, 3905].

## 👥 Equipe - Grupo Purplefox Security
* [cite_start]Dyego de Souza Evaristo - RM 566801 [cite: 3135]
* [cite_start]Marcello Paixão da Cruz - RM 567205 [cite: 3135]
* [cite_start]Regis Ramos Pinheiro - RM 567534 [cite: 3134]
* [cite_start]Suzana Maciel da Silva - RM 566914 [cite: 3135]
* [cite_start]Thomás Henrique Pandolfo de Campos - RM 567744 [cite: 3134]

## ⚠️ Observações e Conduta Ética
* [cite_start]**Autorização e Limites:** Este projeto foi conduzido exclusivamente em ambiente de homologação autorizado, sem uso de ataques de força bruta ou qualquer modificação de dados da aplicação[cite: 3894, 3895]. [cite_start]Não foi utilizado nenhum payload destrutivo que pudesse causar indisponibilidade[cite: 3896].
* [cite_start]**Caráter Confidencial:** Este documento e os seus achados têm fins puramente académicos e éticos[cite: 3139, 3140].