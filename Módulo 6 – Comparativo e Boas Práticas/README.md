# Módulo 6 – Comparativo e Boas Práticas

## Objetivo
Consolidar **boas práticas** no uso de Generics em Delphi, evitando armadilhas comuns, analisando performance e comparando com outras linguagens.  
Este módulo fecha o ciclo, trazendo uma visão crítica e aplicável ao dia a dia.

---

## Conteúdos

### 1. Quando **não usar Generics**
- Quando o tipo é fixo e não precisa ser parametrizado.  
- Se a legibilidade for prejudicada sem ganho real de flexibilidade.  
- Em casos de **overhead de RTTI** que podem impactar desempenho.  
- Quando uma solução simples com **herança ou interfaces** resolve melhor.

---

### 2. Boas práticas de legibilidade e manutenção
- Use **nomes claros** para tipos genéricos (`TEntity`, `TItem`, `TKey`, `TValue`).  
- Evite aninhar muitos níveis de generics (`TDictionary<string, TObjectList<TCliente>>` pode ser difícil de ler).  
- Centralize **regras comuns** em classes auxiliares genéricas.  
- Sempre documente a intenção do generic (especialmente em bibliotecas/frameworks).  

---

### 3. Análise de performance
- Generics em Delphi são **resolvidos em tempo de compilação**, o que evita *boxing/unboxing* (diferente de linguagens como Java).  
- O uso intenso de **RTTI com Generics** pode impactar performance, especialmente em grandes volumes de dados.  
- Prefira `TList<T>` e `TObjectList<T>` para cenários de alta performance.  
- Evite criar instâncias temporárias em loops apertados.  

---

### 4. Diferenças marcantes entre Delphi e outras linguagens
- **C# / Java**: Suporte a *constraints* mais sofisticadas (ex: `where T: new()`, `where T: struct`).  
- **Delphi**: Menos opções de constraints, mas integração forte com **RTTI** e **componentes visuais**.  
- **TypeScript**: Generics voltados para tipagem estática em tempo de compilação (não existem em runtime).  
- **Delphi**: Generics existem também em runtime via RTTI, permitindo frameworks como ORMs e injeção de dependência.  


