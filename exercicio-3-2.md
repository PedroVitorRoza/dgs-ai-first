# Exercício 3.2 — Revisão crítica dos testes gerados por IA

## Avaliação realizada por mim

### Teste 1 — Assertions vagas

```typescript
describe('query endpoint', () => {
  it('should return a response', async () => {
    const res = await request(app).post('/api/query').send({ question: 'prazo devolução' });
    expect(res.status).toBe(200);
    expect(res.body).toBeDefined();
  });
});
```

### O que o teste verifica

- O endpoint responde com status 200.
- Existe um corpo de resposta.

### O que ele deixa de verificar

- Se a resposta está correta.
- Se o prazo informado é realmente o esperado.
- Se existe citação da fonte.
- Se a resposta atende aos requisitos do domínio.

### Risco

O teste pode passar mesmo que o assistente devolva uma resposta incorreta ou sem fonte, gerando uma falsa sensação de segurança.

---

## Teste 2 — Dados irreais

```typescript
describe('query endpoint edge cases', () => {
  it('should handle empty question', async () => {
    const res = await request(app).post('/api/query').send({ question: '' });
    expect(res.status).toBe(400);
  });
});
```

### O que o teste verifica

- Validação para pergunta vazia.

### O que ele deixa de verificar

Apesar de ser um edge case válido, não testa nenhuma situação real do domínio da NovaTech, como devoluções, SLA ou cálculo de frete.

### Risco

Uma funcionalidade importante pode estar quebrada enquanto todos os testes continuam passando.

---

## Teste 3 — Mock que mascara bug

```typescript
describe('feedback endpoint', () => {
  it('should save feedback', async () => {
    const mockCreate = jest.fn().mockResolvedValue({ id: '123' });

    const res = await request(app).post('/api/feedback').send({
      queryId: 'q1',
      rating: 5,
      comment: 'great'
    });

    expect(res.status).toBe(200);
    expect(mockCreate).toHaveBeenCalled();
  });
});
```

### O que o teste verifica

- Apenas que o endpoint retorna sucesso.
- Que o mock foi chamado.

### O que ele deixa de verificar

- Validação dos dados enviados.
- Persistência correta.
- Tratamento de erros.

Além disso, utiliza **Jest**, enquanto o projeto define o uso do **Vitest**, gerando inconsistência com os padrões estabelecidos.

### Risco

Mesmo que exista um erro na validação ou na persistência dos dados, o teste continuará passando.

---

# Segunda revisão utilizando Claude

Após solicitar uma segunda revisão ao Claude, as conclusões foram equivalentes às minhas.

O Claude também identificou que:

- o Teste 1 possui assertions genéricas;
- o Teste 2 não cobre cenários reais do domínio;
- o Teste 3 utiliza um mock permissivo e ainda emprega Jest em um projeto padronizado com Vitest.

---

# Comparação

Minha revisão e a revisão realizada pelo Claude chegaram às mesmas conclusões.

A principal observação adicional foi reforçar que utilizar Jest em um projeto padronizado com Vitest representa uma inconsistência em relação ao AGENTS.md e aos padrões definidos anteriormente.

---

# Teste 1 reescrito

```typescript
describe('QueryHandler', () => {
  it('should return the correct return period and cite the source document', async () => {

    // Arrange
    const response = await request(app)
      .post('/api/query')
      .send({
        question: 'Qual é o prazo de devolução?'
      });

    // Act
    const body = response.body;

    // Assert
    expect(response.status).toBe(200);
    expect(body.answer).toContain('7 dias');
    expect(body.source_document).toBe('POL-001');
    expect(body.confidence_score).toBeGreaterThan(0.8);
  });
});
```

## Melhorias realizadas

- Nome do teste mais descritivo.
- Estrutura clara em Arrange, Act e Assert.
- Verificação do conteúdo da resposta.
- Validação da fonte utilizada.
- Validação do nível de confiança.
- Assertions específicas, evitando apenas `toBeDefined()`.
