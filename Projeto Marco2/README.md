# Assistente de avisos de grupo de turma

Marcos 1 e 2 de Engenharia de Prompts, LLMs e Uso Ético e Seguro (IESB, 2026/2)
Prof. Rodrigo Gonçalves · Aluno: Felipe Ribeiro Garcia · Turma: ENGIADM1A

## O problema
Em grupos de WhatsApp da turma, avisos importantes (prova, prazo, mudança de sala) se perdem entre piadas e correções posteriores. O assistente lê a conversa e devolve uma tabela com os avisos, o status final de cada um (vigente, corrigido, cancelado ou não confirmado) e o trecho que comprova.

## O que tem aqui
- `relatorio/`: relatório do Marco 2 ("prompt book")
- `prompts/`: biblioteca por técnica e versão (zero-shot v1, few-shot + guardrail v2, CoT v3) e `HISTORICO.md`
- `Casos de teste.txt`: casos de teste e rubrica
- `testes/registros/`: respostas dos modelos, sem edição, com modelo, versão e data
- `AUTOR.md`: autoria

## Escolhas feitas
- Tema com gabarito controlável: conversas fictícias com avisos plantados.
- Técnicas comparadas: zero-shot (v1), few-shot + guardrail (v2), few-shot + guardrail + CoT (v3).
- Modelos comparados: [Modelo A] e [Modelo B] (versões nos registros).
- Segurança: injeção de prompt (C08, C13, C16), viés de registro (C11 × C12) e alucinação (C04, C09, C14, C15).

## Como reproduzir
1. Abra um chat novo no modelo escolhido.
2. Copie o prompt de `prompts/`, troque `{{conversa}}` pelas linhas de um caso de `Casos de teste.txt` (sem INÍCIO/FIM).
3. Cole a resposta, sem editar, no arquivo correspondente de `testes/registros/`.

## Privacidade
Todas as conversas são fictícias. Nenhum dado pessoal real foi usado.
