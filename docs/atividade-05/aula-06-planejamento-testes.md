# Planejamento e Execução de Testes – LocalEats

## 1. Plano de Testes
* **Objetivo:** Validar a integridade, funcionalidade e usabilidade do motor de busca e filtragem do sistema LocalEats.
* **Escopo:**
    * **O que será testado:** Campo de busca por texto livre, botões de categorias e retorno de resultados no grid.
    * **O que não será testado:** Processamento de pagamentos, login de usuários e edição de perfil de restaurante.
* **Funcionalidades selecionadas:** Busca de restaurantes e filtros de categoria (Italiana, Japonesa, etc.).
* **Estratégia de testes:** Abordagem de teste funcional de caixa-preta, focada na perspectiva do usuário final, utilizando técnicas de Particionamento de Equivalência para validar diferentes tipos de inputs.
* **Responsáveis:** Equipe de QA (Consultoria Externa).

## 2. Casos de Teste (Sintaxe Gherkin)

**CT01 - Busca por termo parcial (Sucesso)**
* **ID:** CT01
* **Título:** Busca por termo inicial em letras minúsculas.
* **Pré-condição:** O sistema deve estar online e com restaurantes cadastrados no banco de dados.
* **Passos:**
    1. Acessar a página inicial.
    2. No campo de busca, digitar "re".
    3. Clicar em "Buscar".
* **Resultado esperado:** O sistema deve listar todos os restaurantes que contenham "re" no título (ex: Restaurante Sabor X).

**CT02 - Busca Case-Sensitive (Sucesso/Happy Path)**
* **ID:** CT02
* **Título:** Busca ignorando diferenciação entre maiúsculas e minúsculas.
* **Passos:**
    1. No campo de busca, digitar "Res" (com R maiúsculo).
    2. Clicar em "Buscar".
* **Resultado esperado:** O sistema deve retornar os mesmos resultados da busca por "res" (em minúsculo), sendo indiferente à capitalização.

**CT03 - Seleção de Categoria (Sucesso)**
* **ID:** CT03
* **Título:** Filtragem por culinária específica através de botões.
* **Passos:**
    1. Clicar na categoria "Japonesa".
* **Resultado esperado:** Apenas restaurantes com a tag "Japonesa" devem permanecer visíveis no grid.

**CT04 - Busca por termo inexistente (Erro)**
* **ID:** CT04
* **Título:** Validação de feedback para termo não encontrado.
* **Passos:**
    1. Digitar um termo aleatório que não corresponda a nenhum restaurante (ex: "xyz123").
    2. Clicar em "Buscar".
* **Resultado esperado:** Exibição da mensagem "Nenhum restaurante encontrado".

**CT05 - Busca com campo vazio (Erro)**
* **ID:** CT05
* **Título:** Comportamento do sistema ao buscar sem dados de entrada.
* **Passos:**
    1. Limpar o campo de busca.
    2. Clicar em "Buscar".
* **Resultado esperado:** O sistema deve manter a lista completa ou solicitar o preenchimento do campo.

## 3. Execução dos Testes

| ID | Resultado | Evidência (Descrição/Print) |
| :--- | :--- | :--- |
| **CT01** | **FALHOU** | **[Evidência: image_evd_1.png]** Ao buscar por "re", o sistema retornou apenas 2 resultados (Sabor 4 e 12), ignorando outros restaurantes que deveriam estar na lista. |
| **CT02** | **FALHOU** | **[Evidência: image_evd_2.png]** Ao utilizar o termo "Res", o sistema falhou em encontrar os registros, comprovando que a busca é *case-sensitive* (sensível a maiúsculas). |
| **CT03** | **PASSOU** | **[Evidência: image_evd_3.png]** O sistema filtra corretamente os restaurantes ao clicar nas categorias disponíveis na interface. |
| **CT04** | **PASSOU** | O sistema apresenta a mensagem de "Nenhum restaurante encontrado" corretamente para termos inexistentes. |
| **CT05** | **FALHOU** | O sistema não apresenta uma validação de campo obrigatório ao clicar em buscar vazio. |

## 4. Análise dos Resultados
* **Testes Executados:** 5.
* **Passaram:** 2 | **Falharam:** 3.
* **Principais problemas encontrados:** Foram detectados defeitos críticos na lógica de busca (Back-end). O sistema falha ao tratar letras maiúsculas, o que é uma má prática de usabilidade e funcionalidade. Além disso, há uma inconsistência na recuperação de dados, onde a busca parcial não retorna a totalidade dos registros esperados.

## 5. Reflexão no contexto do LocalEats
O plano de testes foi fundamental para identificar que o sistema, apesar de visualmente funcional, possui falhas estruturais na comunicação com o banco de dados. Durante a execução, percebemos que o erro de *case-sensitivity* é um impeditivo real para o usuário comum, que pode usar a capitalização automática do celular e não encontrar o que procura. Como melhoria, sugerimos a normalização dos dados de entrada para minúsculo antes da consulta SQL e a revisão das queries de busca parcial.

---

**Dica técnica de QA:** Como você notou esse erro de maiúsculas/minúsculas, no seu commit você pode descrever isso como um Bug Report. Isso mostra pro professor que você tem a visão de "corrigir na raiz", que é o que você faz no dia a dia com Apex e SQL.
