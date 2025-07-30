
# Módulo 1: Introdução aos Generics

🎯 **Objetivo:**  
Compreender o conceito de *generics* e identificar sua utilidade prática no desenvolvimento de software, especialmente em linguagens como Delphi.

---

## ✅ O que são Generics?

Generics são um recurso da linguagem que permite criar classes, interfaces e métodos parametrizados por tipo.  
Em vez de definir explicitamente o tipo de dados com os quais uma estrutura trabalha, usamos um marcador genérico (como `<T>`) que será substituído em tempo de compilação pelo tipo desejado.

**Exemplo simples em Delphi:**

```delphi
type
  TCaixa<T> = class
  private
    FValor: T;
  public
    procedure SetValor(AValor: T);
    function GetValor: T;
  end;
```

---

## ✅ Vantagens de usar Generics

- **Reutilização de código:** uma mesma estrutura pode ser usada com diferentes tipos.
- **Segurança de tipo em tempo de compilação:** evita erros de *casting*.
- **Melhor legibilidade e manutenção:** reduz código duplicado para diferentes tipos.

---

## ✅ Comparação com tipos variantes e casting

- Com `Variant` ou `Pointer`, temos flexibilidade, mas perdemos segurança e clareza.
- Com generics, mantemos a flexibilidade **sem abrir mão da segurança de tipos**.

**Exemplo com `Variant`:**

```delphi
var
  V: Variant;
  I: Integer;
begin
  V := 10;
  I := V; // Pode compilar, mas sujeito a erro em runtime se V não for numérico
end;
```

**Com Generics:**

```delphi
type
  TCaixa<T> = class
    FValor: T;
  end;
```

---

## ✅ Situações comuns de uso

- Estruturas de dados: listas, pilhas, filas.
- DAOs e repositórios genéricos.
- Componentes reutilizáveis em frameworks.

---

## 📌 Atividade prática

**Escreva uma explicação com suas palavras do que são generics, por que são úteis, e implemente exemplos simples como:**

### 1. Pilha Genérica

```delphi
type
  TPilha<T> = class
  private
    FLista: TList<T>;
  public
    constructor Create;
    destructor Destroy; override;
    procedure Push(AValor: T);
    function Pop: T;
  end;
```

### 2. Lista Genérica (sem uso de TObjectList)

```delphi
type
  TMinhaLista<T> = class
  private
    FItens: array of T;
  public
    procedure Adicionar(AValor: T);
    function Obter(Index: Integer): T;
  end;
```

---

Este módulo é essencial para fundamentar o uso de *Generics* nos próximos conteúdos, preparando você para aplicar esse conceito em estruturas mais complexas e reais, como DAOs e frameworks.
