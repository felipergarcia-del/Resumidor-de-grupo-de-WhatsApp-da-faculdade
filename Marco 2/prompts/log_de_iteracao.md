# Log de Iteração de Prompts - Marco 1

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