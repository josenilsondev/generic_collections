# Desempenho e RTTI com Generics em Delphi

## 1. Introdução
O uso de Generics em Delphi traz flexibilidade e reutilização de código, mas envolve considerações importantes sobre desempenho e uso de RTTI (Run-Time Type Information).  
Neste arquivo, veremos:

- Impactos de desempenho no uso de generics.  
- Como o compilador gera código para cada tipo instanciado.  
- Como acessar e manipular metadados em tempo de execução com RTTI.  
- Exemplos práticos para balancear flexibilidade e performance.

---

## 2. Desempenho em Generics
### 2.1 Geração de Código
- O compilador Delphi gera uma versão **específica** da classe genérica para cada tipo T utilizado.  
- Isso evita *boxing/unboxing* (como ocorre em .NET ou Java), trazendo desempenho próximo ao uso de classes concretas.  
- Porém, pode gerar **inchaço de código** (code bloat) em projetos com muitos tipos diferentes instanciando a mesma classe genérica.

### 2.2 Custos Potenciais
- Métodos genéricos que usam RTTI podem ter impacto maior no desempenho.  
- Operações frequentes em listas grandes devem ser analisadas para garantir que o custo extra não comprometa a performance.  

### 2.3 Boas Práticas de Performance
- Usar generics para cenários de **reuso** e **clareza**.  
- Evitar instanciar centenas de tipos diferentes de uma mesma classe genérica.  
- Usar `TObjectList<T>` quando for necessário gerenciar memória automaticamente (ownership).  

---

## 3. RTTI com Generics
### 3.1 O que é RTTI
- RTTI (Run-Time Type Information) permite inspecionar tipos, atributos e métodos em tempo de execução.  
- No contexto de generics, é útil para criar frameworks de mapeamento, serialização ou reflexão.

### 3.2 Ativando RTTI
Delphi permite controlar a geração de RTTI com atributos:
```delphi
{$RTTI EXPLICIT METHODS([vcPublic]) PROPERTIES([vcPublic]) FIELDS([vcPublic])}

### 4. NOTAS

RTTI é poderosa mas custosa: cada chamada a TRttiContext pode ser cara em loops extensos.
Estratégia recomendada:
Cachear resultados de RTTI (ex.: propriedades e tipos já inspecionados).
Evitar chamar RTTI repetidamente dentro de laços críticos.

class var FCacheProps: TArray<TRttiProperty>;

if Length(FCacheProps) = 0 then
  FCacheProps := LRttiType.GetProperties;

ORMs: mapeamento dinâmico entre classes e tabelas.

Serialização JSON/XML: RTTI ajuda a converter objetos genéricos para representações textuais.
Frameworks de validação: ler atributos customizados em propriedades e aplicar regras automaticamente.
Generics em Delphi são eficientes, mas podem gerar código duplicado para cada tipo instanciado.
RTTI traz grande poder de abstração, porém com custo de performance.
A chave está no equilíbrio: usar RTTI e generics onde a flexibilidade é necessária, mas sempre com caching e boas práticas de otimização.