# Exercício 3.1 — Revisão crítica das respostas do assistente

## Avaliação realizada por mim

Utilizei a rubrica de avaliação baseada em quatro critérios:

- Precisão factual
- Citação de fonte
- Aderência aos guardrails
- Completude da resposta

Cada critério recebe nota de 1 a 3.

| # | Precisão | Fonte | Guardrails | Completude | Total | Resultado |
|---|---------|-------|------------|------------|------:|-----------|
| 1 | 3 | 3 | 3 | 3 | 12 | Excelente |
| 2 | 3 | 3 | 3 | 3 | 12 | Excelente |
| 3 | 3 | 3 | 3 | 3 | 12 | Excelente |
| 4 | 3 | 2 | 3 | 3 | 11 | Excelente |
| 5 | 3 | 3 | 3 | 3 | 12 | Excelente |
| 6 | 1 | 2 | 1 | 1 | 5 | Reprovada |
| 7 | 3 | 3 | 3 | 3 | 12 | Excelente |
| 8 | 2 | 3 | 1 | 2 | 8 | Reprovada |

---

## Justificativa das respostas reprovadas

### Resposta 6

A pergunta não informava o destino do frete.

Mesmo assim o assistente assumiu que o destino era o Sudeste.

Essa informação não foi fornecida pelo usuário, caracterizando uma inferência incorreta e violando o guardrail de não inventar informações.

---

### Resposta 8

Embora o conteúdo estivesse correto, a resposta foi entregue em inglês.

O padrão definido para o assistente é responder em português, portanto houve descumprimento do guardrail de idioma.

---

# Segunda avaliação utilizando Claude

Após solicitar uma segunda revisão ao Claude, o resultado foi praticamente o mesmo.

As respostas 6 e 8 também foram classificadas como inadequadas pelos mesmos motivos:

- resposta 6 faz uma suposição não informada pelo usuário;
- resposta 8 viola o idioma padrão esperado.

As demais respostas foram consideradas aprovadas.

---

# Comparação

Minha avaliação e a avaliação do Claude chegaram às mesmas conclusões.

Não houve divergências relevantes na classificação das respostas.

Isso demonstra que a rubrica possui critérios objetivos e gera avaliações consistentes entre revisores diferentes.

---

# Relatório (Claude Cowork)

## Resumo

- Respostas avaliadas: 8
- Aprovadas: 6
- Reprovadas: 2
- Score médio: 10,5 / 12

## Motivos das reprovações

**Resposta 6**
- Assumiu informação não fornecida pelo usuário.

**Resposta 8**
- Respondeu em inglês em vez de português.

## Parecer para Go-Live

O sistema demonstra boa qualidade geral e atende à maioria dos requisitos funcionais.

Entretanto, antes da entrada em produção recomenda-se corrigir os problemas relacionados à inferência indevida de informações e ao cumprimento do idioma padrão.

Após essas correções, o assistente estará apto para seguir para produção com risco reduzido.
