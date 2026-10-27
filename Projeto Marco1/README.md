# Assistente de avisos de grupo de turma

Marco 1 de Engenharia de Prompts, LLMs e Uso Ético e Seguro (IESB, 2026/2)
Prof. Rodrigo Gonçalves · Aluno: Felipe Ribeiro Garcia · Turma: ENGIADM1A

## O problema
Em grupos de WhatsApp da turma, avisos importantes (prova, prazo, mudança de sala)
se perdem entre piadas e correções posteriores. O assistente lê a conversa e devolve
uma tabela com os avisos, o status final de cada um (vigente, corrigido, cancelado
ou não confirmado) e o trecho que comprova.

## O que tem aqui
- `relatorio/marco1_relatorio.pdf`: relatório do Marco 1
- `prompts/`: prompts por técnica e versão (zero-shot v1, few-shot com guardrail v2) e `HISTORICO.md`
- `testes/casos_de_teste.xlsx`: 8 casos com gabarito e registro de avaliação
- `AUTORES.md`: autoria e log de contribuição

## Como reproduzir
1. Abra um chat de LLM de acesso gratuito (ChatGPT, Claude etc.).
2. Copie o prompt de `Prompts/` e troque `{{conversa}}` pelo texto de um caso da planilha.
3. Cole a resposta, sem editar, na aba "Registro de avaliação", com modelo, versão e data.

## Modelos testados
ChatGPT, GPT-6.

## Privacidade
Todas as conversas são fictícias. Nenhum dado pessoal real foi usado.
