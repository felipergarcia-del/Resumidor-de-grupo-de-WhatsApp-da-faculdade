# Assistente de Grupos de WhatsApp Universitários

**Autor:** Felipe Ribeiro Garcia
**Turma:** ENGIADM1A
**Disciplina:** Engenharia de Prompts, LLMs e Uso Ético e Seguro

---

## 1. Definição do Projeto
* **Domínio:** Comunicação não estruturada de estudantes universitários (mensagens de grupos de WhatsApp).
* **Tarefa:** Ler um bloco de mensagens brutas, extrair os assuntos tratados e classificá-los em três níveis de importância sob a ótica acadêmica: Alta (provas, trabalhos, recados oficiais), Média (dúvidas de matéria, grupos de estudo) e Baixa (conversas paralelas, memes, eventos).
* **Critérios de Sucesso:** O modelo deve identificar eventos acadêmicos críticos (Alta) com 100% de precisão e classificar corretamente o ruído e conversas paralelas como "Baixa" em pelo menos 80% das vezes, gerando um resumo limpo e estruturado.

## 2. Escolhas Iniciais e Linha de Base (Zero-Shot)
O prompt de linha de base (zero-shot) foi construído explorando o **ajuste por instrução** dos modelos modernos. O LLM recebeu um *System Prompt* definindo sua persona (assistente acadêmico) e as regras exatas de classificação para as categorias ALTA, MÉDIA e BAIXA.
Nesta etapa inicial (Marco 1), a interação ocorreu de forma direta, avaliando a capacidade de compreensão da tarefa pelo modelo apenas com instruções, sem o uso de exemplos práticos de formatação.

## 3. Conjunto Inicial de Casos de Teste (Marco 1)
Foram mapeados e executados 8 casos de teste cobrindo diferentes cenários:
1. **Típico:** Aviso oficial de data de trabalho (Alta) com convite para lanche (Baixa).
2. **Típico:** Compartilhamento de foto do quadro (Média) com figurinha (Baixa).
3. **Típico:** Aviso urgente de mudança de sala (Alta).
4. **Misto:** Lançamento de notas (Alta) com reação de alunos e convite para jogo online (Baixa).
5. **Fronteira:** Boato sobre cancelamento de prova trazido por um aluno.
6. **Adversarial:** Aluno fingindo ser o reitor informando reprovação em tom de piada.
7. **Fronteira:** Link de materiais de estudo misturado com link de festa.
8. **Ruído:** Bloco contendo apenas memes e discussões sobre futebol.

*(Nota: Os resultados da execução no ChatGPT em 11/11/2026 estão documentados na pasta de Avaliação).*

## 4. Primeiras Observações e Falhas
Durante a execução dos testes na linha de base (Versão 1.0 - Zero-Shot), o modelo demonstrou boa compreensão semântica da tarefa — inclusive identificando corretamente o sarcasmo no caso adversarial do falso reitor —, mas apresentou uma grave **falha de síntese e alucinação estrutural**.

* **O Problema Identificado:** Em vez de retornar uma lista concisa conforme solicitado, o modelo gerou textos extremamente prolixos. Ele passou a justificar o motivo de cada classificação e a super-segmentar os assuntos (no Caso 04, por exemplo, o modelo criou um tópico isolado de importância 'MÉDIA' apenas para relatar o desabafo de um aluno sobre sua nota 4,5, o que é irrelevante para um resumo acadêmico).
* **Correção Aplicada:** A falha justificou a evolução para o prompt Versão 2.0 (Few-Shot), onde a inclusão de exemplos práticos ancorou o formato de saída, forçando o modelo a abandonar as explicações longas e adotar um padrão de resposta cirúrgico e direto.