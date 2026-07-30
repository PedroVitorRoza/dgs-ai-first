# SKILL - create-integration-test

## Objetivo

Esta skill define o padrão para criação de testes de integração no projeto NovaTech Assistant.

Ela deve ser utilizada sempre que um agente de IA precisar gerar ou alterar testes de integração para APIs, endpoints ou componentes que dependam de serviços externos.

---

# Quando utilizar

Use esta skill sempre que for solicitado:

- Criar testes de integração.
- Adicionar novos cenários de teste.
- Atualizar testes existentes.
- Cobrir novos requisitos funcionais.

---

# Dependências

Antes de utilizar esta skill, consulte:

- AGENTS.md
- Testing Standards
- Documentação do domínio
- Fixtures disponíveis em `/tests/fixtures`

---

# Template

```typescript
describe('ModuleName', () => {

  it('should [expected behavior] when [condition]', async () => {

    // Arrange

    // Act

    // Assert

  });

});
```

---

# Exemplo (DO)

```typescript
describe('QueryHandler', () => {

  it('should return the correct answer when the query exists', async () => {

    // Arrange

    server.use(...);

    const request = createQueryRequest();

    // Act

    const response = await handler(request);

    // Assert

    expect(response.status).toBe(200);
    expect(response.source_document).toBe('PROC-042 v2');
    expect(response.answer).toContain('frete');

  });

});
```

Boas práticas:

- Nome descritivo.
- Arrange, Act e Assert separados.
- Assertions específicas.
- Uso de mocks.
- Dados reutilizáveis.

---

# Exemplo (DON'T)

```typescript
test('works', async () => {

    const result = await handler(request);

    expect(result).toBeDefined();

});
```

Problemas encontrados:

- Nome genérico.
- Não possui Arrange/Act/Assert.
- Assertion muito vaga.
- Não utiliza mocks.
- Difícil manutenção.

---

# Anti-padrões

Evitar:

- toBeDefined() como única validação.
- toBeTruthy() sem verificar comportamento.
- Dados hardcoded quando existir fixture.
- Dependência entre testes.
- Chamada para APIs reais.
- Mocks excessivamente permissivos.
- Testar detalhes internos da implementação em vez do comportamento esperado.

---

# Checklist de revisão

Antes de considerar o teste aprovado, verificar:

- Nome do teste está descritivo.
- Estrutura Arrange / Act / Assert está presente.
- Assertions verificam comportamento.
- Não existe acesso a serviços externos.
- Fixtures reutilizáveis foram utilizadas.
- Mock configurado corretamente.
- Teste é independente dos demais.
- Resultado esperado está claro.

Todos os itens acima devem ser atendidos antes da aprovação do teste.
