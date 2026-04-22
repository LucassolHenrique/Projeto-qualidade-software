![alt text](image.png)# Planejamento e Execução de Testes – LocalEats

## 1. Plano de Testes
* **Objetivo:** Validar a funcionalidade de busca de restaurantes do sistema LocalEats, garantindo que o utilizador consiga encontrar opções através de texto livre e filtros.
* **Escopo:**
  * *O que será testado:* Campo de busca por texto livre, retorno de resultados e mensagens de estado vazio.
  * *O que não será testado:* Fluxo de login, favoritar restaurantes ou a página de detalhes do restaurante.
* **Funcionalidades selecionadas:** Busca de restaurantes na página inicial.
* **Estratégia de testes:** Testes funcionais manuais (Caixa-preta) focados na usabilidade e validação de entradas (Boundary Value Analysis / Equivalence Partitioning).
* **Responsáveis:** Analista de QA (Planeamento, execução e registo das evidências).

---

## 2. Casos de Teste

**CT01 - Busca por termo parcial minúsculo (Cenário de Sucesso)**
* **Pré-condição:** Estar na página principal com a lista completa de restaurantes carregada.
* **Passos:**
  * Dado que estou na página principal do LocalEats
  * E que o campo "Buscar por culinária ou localização" está visível
  * Quando eu preencho o campo com o valor "re"
  * E clico no botão "Buscar"
  * Então o sistema deve exibir todos os restaurantes que contêm "re" no nome ou descrição.

**CT02 - Busca por termo parcial com letra maiúscula (Cenário de Sucesso)**
* **Pré-condição:** Estar na página principal.
* **Passos:**
  * Dado que estou na página principal do LocalEats
  * Quando eu preencho o campo de busca com o valor "Res"
  * E clico no botão "Buscar"
  * Então o sistema deve exibir a mesma lista de restaurantes correspondentes ao termo, independentemente de ser maiúscula ou minúscula (case-insensitive).

**CT03 - Filtro por categoria específica (Cenário de Sucesso)**
* **Pré-condição:** Estar na página principal.
* **Passos:**
  * Dado que estou na página principal do LocalEats
  * Quando eu clico no botão de filtro "Japonesa"
  * Então o sistema deve exibir apenas os restaurantes com a tag correspondente (ex: Restaurante Sabor 1 e Sabor 2).

**CT04 - Busca por restaurante inexistente (Cenário de Erro)**
* **Pré-condição:** Estar na página principal.
* **Passos:**
  * Dado que estou na página principal do LocalEats
  * Quando eu preencho o campo de busca com o valor "Churrascaria Inexistente123"
  * E clico no botão "Buscar"
  * Então o sistema deve exibir a mensagem amigável "Nenhum restaurante encontrado." sem quebrar a interface.

**CT05 - Busca com caracteres especiais (Cenário de Erro)**
* **Pré-condição:** Estar na página principal.
* **Passos:**
  * Dado que estou na página principal do LocalEats
  * Quando eu preencho o campo de busca com o valor "@#$%"
  * E clico no botão "Buscar"
  * Então o sistema não deve executar scripts maliciosos e deve retornar a mensagem "Nenhum restaurante encontrado."

---

## 3. Execução dos Testes

| ID | Resultado | Evidência / Observação |
| :--- | :--- | :--- |
| **CT01** | ❌ Falhou | O sistema realizou a busca, mas limitou drasticamente o retorno. Exibiu apenas 2 restaurantes (Sabor 4 e Sabor 12), ocultando outras opções válidas disponíveis no catálogo. |
| **CT02** | ❌ Falhou | Ao buscar por "Res", a aplicação apresentou a mensagem "Nenhum restaurante encontrado". O campo é sensível a maiúsculas/minúsculas (*case-sensitive*), o que prejudica a usabilidade. |
| **CT03** | ✅ Passou | Filtros de categorias (ex: Japonesa) funcionam e atualizam o grid corretamente. |
| **CT04** | ✅ Passou | A mensagem de "Nenhum restaurante encontrado." aparece corretamente. |
| **CT05** | ✅ Passou | O sistema lida com caracteres especiais sem quebrar, retornando o estado vazio. |

---

## 4. Análise dos Resultados
* **Quantos testes foram executados?** 5 casos de teste funcionais.
* **Quantos passaram? Quantos falharam?** 3 passaram e 2 falharam criticamente.
* **Quais os principais problemas encontrados?** O motor de busca possui falhas graves na validação e recuperação de dados. A *query* na base de dados é *case-sensitive*, penalizando utilizadores que começam a escrever com letra maiúscula (falha de UX/Usabilidade). Além disso, a busca parcial está inconsistente, limitando o retorno dos itens na grelha e escondendo restaurantes válidos.

---

## 5. Reflexão no contexto do LocalEats
* **O plano de testes ajudou a organizar melhor os testes?** Sim, permitiu sair de uma análise genérica ("o sistema está com erro") para uma métrica acionável ("o sistema falha especificamente no input com iniciais maiúsculas").
* **Algum problema só foi percebido durante a execução?** Sim. O bug do *case-sensitive* (CT02) apenas foi validado ao realizar a variação de massa de dados na prática, simulando a ação de um teclado mobile que muitas vezes capitaliza a primeira letra automaticamente.
* **O que melhorariam no processo de testes?** Para evitar que este tipo de bug regresse (*regressão*), implementaríamos testes automatizados de integração logo na API de busca, garantindo que a regra de negócio converte sempre a *string* para `toLowerCase()` antes de consultar a base de dados.
