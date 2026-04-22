# Diagnóstico de Qualidade – Startup Local Eats

## 1. Problemas Identificados e Análise Baseada na ISO/IEC 25000

| Problema identificado | Atributo de qualidade afetado | Justificativa técnica |
| :--- | :--- | :--- |
| O sistema fica lento em horários de pico | Eficiência de Desempenho (Comportamento em relação ao tempo) | O tempo de resposta elevado compromete a fluidez da navegação, sobrecarrega o servidor e prejudica diretamente a submissão de pedidos. |
| Algumas interfaces são confusas e pouco intuitivas | Usabilidade (Apreensibilidade / Operabilidade) | A interface apresenta uma curva de aprendizagem elevada, dificultando a interação do utilizador e gerando atrito para concluir ações simples. |
| Certas buscas retornam resultados incorretos | Adequação Funcional (Acurácia / Correção funcional) | O sistema falha ao processar as regras de negócio corretamente, não entregando a precisão esperada na recuperação de dados da base de dados. |
| A aplicação apresenta falhas em determinados modelos de smartphone | Portabilidade (Adaptabilidade) e Compatibilidade | A aplicação não possui resiliência estrutural para ser executada de forma estável em diferentes hardwares ou sistemas operativos. |
| Dificuldade para concluir ações simples | Usabilidade (Operabilidade) | O fluxo de navegação não é lógico ou amigável, exigindo um esforço cognitivo excessivo do utilizador final. |
| Avaliações desaparecem após atualização da página | Confiabilidade (Maturidade / Recuperabilidade) | Falha crítica na persistência de dados (operações DML no banco), onde a informação submetida não é gravada de forma permanente. |
| Inconsistências entre a versão web e mobile | Adequação Funcional e Usabilidade (Estética da interface) | A falta de padronização quebra a integridade da experiência, gerando comportamentos e aspetos visuais divergentes para as mesmas funções. |
