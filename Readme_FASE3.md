# Relatório de Exploração Web | Challenge CEAP - Fase 3 🦊🔍

Este repositório contém o **Relatório Técnico de Teste de Intrusão** e Exploração Web realizado na aplicação `dev.pedreira.org`. O projeto integra a Fase 3 do Challenge CEAP do curso de Defesa Cibernética da FIAP.

## 🎯 Objetivo e Escopo
O escopo da avaliação englobou as fases de Reconhecimento, Análise de Vulnerabilidades Web e Enumeração de Superfície.
* **Alvo Avaliado:** `dev.pedreira.org` (Diretório `/devSecurityG5/`).
* **Metodologia:** OWASP Top 10, CVSS v3.1, PTES.
* **Compliance Avaliado:** LGPD (Lei 13.709/2018), ISO/IEC 27001, NIST SP 800-115.

## 🛠️ Ferramentas Utilizadas
Os testes foram executados a partir de um ambiente Kali Linux (Máquina Virtual), utilizando o seguinte arsenal de segurança:
* Nmap, Nikto, ffuf, dirsearch, OWASP ZAP, Burp Suite, curl, Netcat.

## 🚨 Vulnerabilidades Identificadas
Durante a análise, não foram identificadas vulnerabilidades críticas isoladas. No entanto, a combinação de fragilidades de severidade baixa e média gera um cenário real de risco e de potencial comprometimento de sessões:

| Vulnerabilidade | CVSS v3.1 | Severidade |
| :--- | :--- | :--- |
| **Biblioteca jQuery 1.11.3 com CVEs conhecidos** | 6.1 | MÉDIA |
| **Ausência de Headers de Segurança HTTP** | 5.3 | MÉDIA |
| **Endpoint `/metrics` exposto sem autenticação** | 5.3 | MÉDIA |
| **Ausência de Subresource Integrity (SRI)** | 5.0 | MÉDIA |
| **Cookie sem atributo SameSite** | 4.3 | BAIXA |
| **Cookie sem flag HttpOnly (ESR)** | 4.0 | BAIXA/MÉDIA |

## 🛡️ Plano de Ação Recomendado (Mitigação)
Para reduzir a superfície de ataque e garantir a conformidade com as normas aplicáveis, as seguintes ações de **Prioridade Alta** são recomendadas:
1. **CSP:** Implementar Content-Security-Policy (CSP) em todos os headers de resposta.
2. **Proteção de Sessão:** Ativar a flag HttpOnly em todos os cookies de sessão.
3. **Atualização de Bibliotecas:** Atualizar o jQuery da versão 1.11.3 para a versão 3.7.x ou superior.
4. **Controlo de Acesso:** Restringir o acesso ao endpoint `/metrics` exigindo autenticação.

## 👥 Equipe - Grupo Purplefox Security
* Dyego de Souza Evaristo - RM 566801
* Marcello Paixão da Cruz - RM 567205
* Regis Ramos Pinheiro - RM 567534
* Suzana Maciel da Silva - RM 566914
* Thomás Henrique Pandolfo de Campos - RM 567744

## ⚠️ Observações e Conduta Ética
* **Autorização e Limites:** Este projeto foi conduzido exclusivamente em ambiente de homologação autorizado, sem uso de ataques de força bruta ou qualquer modificação de dados da aplicação. Não foi utilizado nenhum payload destrutivo que pudesse causar indisponibilidade.
* **Caráter Confidencial:** Este documento e os seus achados têm fins puramente académicos e éticos.
