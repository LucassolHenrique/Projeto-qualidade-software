# Testes Funcionais vs Estruturais – Local Eats

## 1. Escolha da Funcionalidade
**Funcionalidade:** Busca de restaurantes (por tipo de culinária, localização e faixa de preço).
* **O que a funcionalidade faz:** Permite que o utilizador filtre a base de dados de restaurantes utilizando um ou mais parâmetros (ex: "Italiana", "Centro", "$$").
* **O que o utilizador espera:** Receber rapidamente uma lista de restaurantes que correspondam exatamente aos filtros selecionados, ou uma mensagem clara caso não haja correspondência.

## 2. Testes Caixa-Preta (Visão do Utilizador / Funcionais)
Pensando apenas na interface e no comportamento externo, sem ver o código:
* **Entradas possíveis:**
  * Pesquisa por texto exato (ex: "Pizza").
  * Seleção de múltiplos filtros simultâneos (ex: Culinária: "Japonesa" + Preço: "$$$").
  * Entradas inválidas ou caracteres especiais (ex: "@#%").
* **Comportamentos esperados:**
  * Retornar os restaurantes corretos correspondentes aos filtros.
  * A paginação ou o "scroll infinito" deve funcionar se houver muitos resultados.
* **Situações de erro a validar:**
  * O que acontece se o utilizador pesquisar uma culinária que não existe na cidade? (Deve mostrar estado vazio amigável, não quebrar a tela).
  * O que acontece se a internet cair durante a pesquisa? (Deve exibir aviso de erro de rede).

## 3. Testes Caixa-Branca (Visão do Sistema / Estruturais)
Imaginando que temos acesso ao código-fonte (back-end e query ao banco):
* **Possíveis estruturas lógicas:**
  * Estruturas condicionais (`if/else` ou `switch/case`) para montar a query de acordo com os filtros preenchidos. Exemplo: `if (preco != null) { addWhereClause("preco", preco); }`.
  * Tratamento de exceções (`try/catch`) na comunicação com o banco de dados.
* **Situações que precisam ser testadas no código:**
  * Cobertura de ramificações (Branch Coverage): Garantir que a lógica passa corretamente pelo `if` quando o filtro de localização está preenchido e pelo `else` quando está vazio.
  * Proteção contra falhas de segurança: Validar se a query está parametrizada para evitar *SQL Injection* nos campos de pesquisa de texto livre.

## 4. Comparação entre as Abordagens
* **Diferença principal:** O teste caixa-preta baseia-se nos **Requisitos** (o sistema faz o que o negócio pediu?), focando na validação. O teste caixa-branca baseia-se na **Arquitetura/Código** (o sistema foi construído corretamente?), focando na verificação interna.
* **Tipos de problema encontrados:**
  * *Caixa-preta* encontra problemas de Usabilidade, falhas de integração visual e fluxos quebrados para o utilizador final.
  * *Caixa-branca* encontra lógica defeituosa (operações matemáticas erradas, loops infinitos), código morto e vulnerabilidades de performance a nível de servidor.

## 5. Reflexão no Contexto do Local Eats
* **Qual abordagem é mais útil agora?** Ambas são indispensáveis para o cenário atual, mas complementares. O problema de "buscas retornarem resultados incorretos" é essencialmente um problema lógico (Caixa-Branca - a query no banco de dados provavelmente está errada ou os joins estão a cruzar dados indevidos). Já as "telas confusas" são um problema de experiência (Caixa-Preta).
* **Apenas uma seria suficiente?** Não. Se usarmos apenas Caixa-Branca, o desenvolvedor pode provar que a função da base de dados funciona, mas o utilizador continua sem conseguir clicar no botão de pesquisa (falha de front-end). Se usarmos apenas Caixa-Preta, podemos validar que o botão funciona, mas não garantimos que a pesquisa é eficiente, mantendo o problema da "lentidão nos horários de pico". A combinação garante que a interface atende o utilizador e o motor atende o sistema.
