Relatório Challenge CEAP - Fases 1 e 2 | Reconhecimento Passivo 🦊🔍
Este repositório contém a documentação técnica referente ao Planejamento, Proposta Detalhada e Mapeamento Operacional da aplicação dev.pedreira.org. O projeto faz parte do 1º Semestre do curso de Defesa Cibernética da FIAP


🎯 Objetivo e EscopoO objetivo desta fase foi estabelecer a base técnica e metodológica para a futura execução de testes éticos de segurança em um ambiente de homologação. Trata-se de um Vulnerability Assessment Passivo, onde não houve exploração de falhas, injeção de dados ou ações intrusivas.  Alvo Avaliado: dev.pedreira.org (IP 177.190.193.105).  Metodologia Aplicada: PTES, NIST SP 800-115 e OWASP Testing Guide.  Infraestrutura e DNS: Domínio sob autoridade da Cloudflare e IP alocado à CTINET Soluções - Brasil


🛠️ Ferramentas Utilizadas
A coleta de informações (Reconhecimento Passivo) utilizou o seguinte ferramental:  

Whois: Consulta de registros de domínio e IP.  

Dig: Análise detalhada de registros DNS.  

Curl: Fingerprinting de cabeçalhos HTTP.  

Nmap: Verificação de certificados SSL/TLS em modo seguro.  

Crt.sh / Amass: Enumeração passiva de subdomínios.


🚨 Principais Descobertas (Reconhecimento Passivo)A infraestrutura apresentou padrões de segurança superficiais adequados, porém com pontos de atenção relevantes:  Segurança de E-mail: O registro SPF está configurado, mas há ausência dos registros DKIM e DMARC.  Criptografia (SSL/TLS): A aplicação utiliza um certificado válido emitido pela GlobalSign, possui suporte ao protocolo moderno TLS 1.3 e utiliza suítes de cifra robustas (AES-GCM / CHACHA20). Além disso, o HSTS está ativo.  Exposição de Informações Sensíveis: Foi identificado o endpoint /metrics acessível publicamente e sem autenticação.  Alertas do HAProxy/Tomcat: O monitoramento exposto no /metrics revelou uma alta proporção de requisições com erro 404 (possível varredura de bots), vazamento da versão exata do Apache (9.0.93.0) e um comportamento anômalo do Garbage Collector, o que pode indicar vazamento de memória


Próximos Passos
O mapeamento passivo forneceu a inteligência necessária para as fases subsequentes. A continuidade do projeto (Fases 3 e 4) envolverá a varredura, identificação e validação de vulnerabilidades de forma ativa e controlada


Equipe - Grupo Purplefox Security

Dyego de Souza Evaristo.  
Marcello Paixão da Cruz.  
Regis Ramos Pinheiro.  
Suzana Maciel da Silva.  
Thomás Henrique Pandolfo de Campos.  


Aviso Legal: Todas as análises descritas neste documento foram realizadas de maneira totalmente passiva, sem causar impacto ao ambiente, respeitando rigorosamente o escopo ético e as atividades permitidas (fingerprinting, enumeração de DNS e verificação TLS)
