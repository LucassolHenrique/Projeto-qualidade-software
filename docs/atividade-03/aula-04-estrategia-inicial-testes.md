# Estratégia Inicial de Testes – Local Eats

## 1. Funcionalidades Principais
Para esta estratégia inicial, focaremos no núcleo de valor do negócio:
1. **Busca de restaurantes** (por localização, culinária e preço).
2. **Visualização de cardápios e detalhes** (fotos e informações do estabelecimento).
3. **Gestão de avaliações** (submissão e leitura de feedbacks).
4. **Sistema de Favoritos** (salvar estabelecimentos para consulta rápida).
5. **Motor de recomendações personalizadas**.

## 2. Níveis de Teste
Abaixo detalhamos onde e o porquê de cada nível, aplicando a visão estrutural sobre as funcionalidades:

* **Teste Unitário (Base do código):**
  * *O que testa:* Lógica isolada. Exemplo: validar se o algoritmo de busca filtra corretamente a faixa de preço inserida, ou se a função de cálculo de média de avaliações retorna o valor matemático correto, sem acessar o banco de dados.
* **Teste de Integração (Comunicação):**
  * *O que testa:* O contrato entre os módulos. Exemplo: garantir que o front-end web e mobile consigam consumir a mesma API de busca e que o módulo de "Favoritos" consiga gravar a relação Usuário-Restaurante no banco de dados com sucesso.
* **Teste de Sistema (Fluxo End-to-End):**
  * *O que testa:* A jornada completa. Exemplo: buscar um restaurante, abrir o cardápio e submeter uma avaliação, garantindo que o sistema como um todo se comporta de forma íntegra.
* **Teste de Aceitação (Visão do Negócio):**
  * *O que testa:* A satisfação do utilizador e os critérios de aceite. Exemplo: validar se a tela de busca deixou de ser "confusa e pouco intuitiva", assegurando que um utilizador comum consegue encontrar sua comida sem frustração.

## 3. Prioridades e Riscos
* **Mais críticas:** Busca de restaurantes e Visualização de cardápios.
* **Maior impacto:** Uma falha na **Busca** inutiliza o propósito principal do aplicativo. Se a busca retorna resultados incorretos (como relatado no diagnóstico), o utilizador não encontra o que deseja e abandona a plataforma. Da mesma forma, se o **Cardápio** não carregar, não há conversão (pedido/visita).
* **Justificativa:** O risco financeiro e de reputação concentra-se no funil de conversão. Funcionalidades como "Favoritos" ou "Recomendações", embora gerem engajamento, não são bloqueantes para o consumo imediato e possuem prioridade secundária na esteira de correções.

## 4. Pirâmide de Testes
* **Maior quantidade (Base):** **Testes Unitários**. São rápidos de executar, baratos de manter e devem ser aplicados massivamente em todas as lógicas de negócio (validações, cálculos, filtros). Ajudam a evitar que erros básicos cheguem aos ambientes superiores.
* **Menor quantidade (Topo):** **Testes de Sistema / UI End-to-End**. São lentos, custosos e suscetíveis a falsos positivos (flaky tests). Devem focar estritamente nos "Caminhos Felizes" (Happy Paths) das funcionalidades críticas (ex: realizar uma busca e abrir o cardápio).
* **Justificativa:** Inverter a pirâmide (testar tudo pela interface) atrasaria os lançamentos e encareceria a manutenção. A pirâmide tradicional garante feedback rápido para o desenvolvedor e eficiência operacional.

## 5. Testes em Produção
* **Uso recomendado:** Sim, o sistema deve utilizar testes em produção, mas de forma controlada.
* **Situações de uso:**
  * **Monitorização e Telemetria:** Para investigar a "lentidão em horários de pico", é vital realizar testes de performance passivos e monitorizar tempos de resposta diretamente no ambiente real, onde o tráfego é genuíno.
  * **Feature Flags / Canary Releases:** Lançar a nova tela de buscas gradualmente (ex: para apenas 10% dos utilizadores) para validar se as melhorias de usabilidade foram eficazes antes de substituir o sistema inteiro, reduzindo o risco de novas falhas em dispositivos específicos.
