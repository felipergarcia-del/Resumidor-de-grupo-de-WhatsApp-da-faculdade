# Histórico de iteração dos prompts

| Versão | Técnica | O que mudou | Por quê | Resultado observado |
|---|---|---|---|---|
| v1 | zero-shot | Versão inicial, só a instrução. | Linha de base para comparação. | Marco 1: 7 de 8 casos corretos. Erro no C04: escreveu "Amanhã (27/10/2026)", data que não está na conversa (repetido em 2 execuções). Nenhuma resposta citou a fonte. |
| v2 | few-shot + guardrail | Adicionados papel, 6 regras, formato de tabela com coluna de fonte e 2 exemplos. | Reduzir datas supostas, tratar boato como não confirmado, exigir fonte e barrar instruções escondidas na conversa. | Marco 1: 7 de 8 corretos. Corrigiu o C04 e todas as respostas citaram a fonte. Erro novo no C01: marcou "não confirmado" um aviso repassado pelo professor. Usou status fora do padrão ("confirmado", "atualizado", "informado"). |
| v3 | few-shot + guardrail + CoT | Lista de status permitidos; regra de que "o prof falou" é vigente; datas relativas não viram data do calendário; proibido acrescentar ano; regra para ignorar assuntos não acadêmicos; 4 passos de raciocínio antes da tabela; terceiro exemplo com data relativa. | Corrigir os problemas do v2 observados no Marco 1 e testar CoT como técnica avançada. | [PREENCHER após os testes do Marco 2] |
