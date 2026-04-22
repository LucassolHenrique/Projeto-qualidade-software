# Diagnóstico de Qualidade – Startup Local Eats

## 1. Diagnóstico da Situação Atual
Atualmente, a startup enfrenta problemas críticos em produção (pedidos duplicados, erros no checkout) devido à ausência de uma cultura de qualidade consolidada. Provavelmente, os papéis existentes (Desenvolvedores e Analistas) estão a acumular a função de testar o seu próprio trabalho, o que gera viés de validação. Quando as responsabilidades de qualidade não são claras, ocorre o "efeito silo": o desenvolvedor acredita que a sua parte está pronta, mas o fluxo de ponta a ponta falha. A qualidade do software não é um cargo isolado; deve ser entendida como uma **responsabilidade partilhada por toda a equipa**, exigindo processos claros e a introdução de profissionais focados em mitigar riscos antes de as funcionalidades entrarem em produção.

## 2. Papéis da Equipe
Para estabilizar e escalar o produto, propomos a seguinte estruturação:

* **Desenvolvedor:**
  * *Responsabilidades:* Escrever código limpo, realizar testes unitários das suas próprias funções e corrigir os bugs reportados.
  * *Relação com a Qualidade:* É a primeira linha de defesa. Garante que a base do sistema é robusta antes de enviar para a revisão estrutural.
* **Analista de Qualidade de Software (QA):**
  * *Responsabilidades:* Desenhar casos de teste, validar requisitos e executar testes funcionais (exploratórios e sistémicos) antes do lançamento.
  * *Relação com a Qualidade:* É o guardião do utilizador final. O seu foco é quebrar o sistema intencionalmente para encontrar e documentar falhas ocultas.
* **Product Owner / Analista de Sistemas:**
  * *Responsabilidades:* Levantar requisitos detalhados e definir os "Critérios de Aceite" de cada funcionalidade.
  * *Relação com a Qualidade:* Garante que o desenvolvedor sabe exatamente o que tem de ser construído e que o QA sabe exatamente o que tem de ser testado.

## 3. Práticas de QA Sugeridas
1. **Revisão de Código (Code Review):** Nenhum código entra em produção sem ser lido e aprovado por, pelo menos, um desenvolvedor diferente daquele que o escreveu.
2. **Shift-Left Testing (Testar Cedo):** Envolver o QA logo na fase de planeamento (definição de requisitos), para antecipar armadilhas lógicas antes sequer de se escrever uma linha de código.
3. **Gestão Estruturada de Defeitos:** Utilização de ferramentas (como Jira, Trello ou GitHub Issues) para o registo, categorização e acompanhamento do ciclo de vida de cada bug encontrado.
4. **Testes Exploratórios Regulares:** Simulações periódicas utilizando cenários não padronizados para garantir que o utilizador final não é capaz de quebrar o sistema através de comportamentos imprevisíveis.

## 4. Anúncios de Contratação

### Vaga 1: Analista de Qualidade de Software (QA)
**Empresa:** Local Eats
**Local:** Porto Alegre – RS
**Modelo:** Híbrido

**Sobre a vaga:**
Procuramos um Analista de Qualidade (QA) proativo para estruturar os nossos processos de testes e garantir a fiabilidade do nosso sistema de pedidos online. Trabalhará lado a lado com os nossos desenvolvedores para evitar que anomalias cheguem aos nossos clientes e parceiros comerciais.

**Principais Responsabilidades:**
* Planeamento e execução de casos de teste funcionais e exploratórios.
* Identificação, documentação detalhada e acompanhamento de bugs.
* Apoio na definição de critérios de qualidade junto à equipa de produto.
* Atuar como o representante das necessidades operacionais do utilizador final.

**Requisitos Obrigatórios:**
* Compreensão sólida de metodologias e documentação de testes de software.
* Capacidade analítica para identificar cenários de falha.
* Boa comunicação para alinhar ajustes de forma construtiva com a equipa de engenharia.

**Requisitos Desejáveis:**
* Noções práticas de banco de dados (SQL) para validação de integridade.
* Conhecimento prévio no uso de ferramentas de versionamento (Git).
* Certificação ISTQB – CTFL.

---

### Vaga 2: Desenvolvedor Back-End Júnior / Pleno
**Empresa:** Local Eats
**Local:** Porto Alegre – RS
**Modelo:** Híbrido

**Sobre a vaga:**
A Local Eats procura um desenvolvedor responsável e detalhista, focado em construir e manter uma arquitetura escalável. Se constrói código pensando na performance e tem brio em entregar funcionalidades robustas e já validadas, o seu lugar é aqui.

**Principais Responsabilidades:**
* Desenvolvimento e manutenção de APIs para o nosso ecossistema web e mobile.
* Integração de regras de negócio consistentes (evitando cenários como duplicação de transações).
* Criação de testes unitários para o código implementado.
* Revisão de código dos pares, assegurando as boas práticas do projeto.

**Requisitos Obrigatórios:**
* Domínio em lógica de programação e em linguagens de desenvolvimento web.
* Habilidade para ler e escrever queries complexas em banco de dados relacional.
* Compreensão prática do conceito de qualidade como responsabilidade do desenvolvedor.

**Requisitos Desejáveis:**
* Experiência prévia em e-commerce ou plataformas de processamento de pedidos.
* Familiaridade com práticas de CI/CD.
