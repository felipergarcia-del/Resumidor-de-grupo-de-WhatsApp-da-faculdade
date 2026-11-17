# Log de Iteração de Prompts - Marco 1 e 2

Este documento registra a evolução da biblioteca de prompts, documentando as versões e a justificativa para cada mudança realizada.

## Versão 1.0: Zero-Shot (Linha de base) 11/11
*   **Arquivo:** `01_zero_shot.txt`
*   **Objetivo:** Estabelecer a linha de base para testar se o modelo consegue compreender a tarefa apenas com instruções diretas e regras de classificação.
*   **Observações de Teste:** O modelo compreendeu perfeitamente a semântica da tarefa (não caiu nas pegadinhas dos Casos 05 e 06), porém apresentou **alucinação estrutural e falha de síntese**. Ele gerou respostas extremamente prolixas, justificando suas escolhas, e super-segmentou os assuntos (no Caso 04, criou um tópico isolado apenas para o desabafo de um aluno). Faltou ancoragem de formato.

## Versão 2: Few-Shot 11/11
*   **Arquivo:** `02_few_shot.txt`
*   **Justificativa da Mudança:** A técnica de *Few-Shot* foi implementada para resolver a inconstância na formatação e na separação de tópicos.
*   **O que foi alterado:** Foram adicionados dois exemplos explícitos no *System Prompt* mostrando conversas simuladas e a saída exata esperada. O Exemplo 1 ensina o modelo a separar um recado de professor (ALTA) de uma conversa paralela (BAIXA) no mesmo bloco de texto. O Exemplo 2 ensina o modelo a ignorar ruídos visuais (figurinha) e focar na troca de materiais (MÉDIA).
*   **Resultado esperado:** Forçar o LLM a replicar o padrão estrutural dos exemplos, eliminando alucinações de formato e melhorando a precisão da triagem.
*   **Observações de Teste (Gargalos Residuais):** O *Few-Shot* corrigiu a estrutura geral (`Assunto:` e `(Contexto).`), mas o modelo gerou variações nas etiquetas (como `[IMPORTANCIA ALTA]` por extenso), omitiu os nomes dos participantes nos resumos e ainda não possuía proteção explícita contra ataques adversariais (*Prompt Injection*), viés ou falsas emergências.

## Versão 3: Few-Shot + Chain-of-Thought (CoT) Oculto + Guardrails 17/11
*   **Arquivo:** `03_few_shot_cot.txt`
*   **Justificativa da Mudança:** Consolidar o prompt final do Marco 2 para zerar variações nas tags de classificação, exigir identificação nominal dos envolvidos e blindar o assistente contra *Prompt Injection*, toxicidade e gatilhos emocionais (falsas emergências).
*   **O que foi alterado:**
    *   **Padronização Few-Shot:** Revisão dos dois exemplos para fixar as etiquetas exatas (`[ALTA]`, `[MÉDIA]`, `[BAIXA]`) e obrigar a citação nominal de todos os participantes envolvidos.
    *   **Chain-of-Thought (CoT) Oculto:** Inclusão de um fluxo lógico interno em 4 passos antes da resposta *(1. identificar remetente e intenção; 2. filtrar ameaças ou injeções; 3. mapear a classificação; 4. redigir resumo completo citando os nomes)*, com restrição explícita para não exibir o raciocínio na saída.
    *   **Cláusula de Segurança (*Guardrail*):** Adição de diretriz dedicada para ignorar comandos de *Prompt Injection* e rebaixar tentativas de manipulação, conteúdos tóxicos e desespero pessoal sem impacto coletivo para `[BAIXA]`.
*   **Resultados Validados (Marco 2):** O prompt atingiu **90/90 pontos (100%)** na rubrica de 15 casos de teste tanto no **ChatGPT** quanto no **Gemini** (um salto de **+27 pontos / +42,8%** em relação aos 63/90 da V1), neutralizando com sucesso a injeção de prompt (Caso 11), a toxicidade contra docente (Caso 12) e a falsa emergência (Caso 14) sem vazar o raciocínio interno.
