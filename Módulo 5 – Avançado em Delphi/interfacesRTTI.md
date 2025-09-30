# Integração com Interfaces e RTTI Avançada em Delphi

## 1. Introdução
Interfaces em Delphi permitem abstrair contratos e separar implementação da definição.  
Quando combinadas com **Generics** e **RTTI Avançada**, abrem caminho para criar frameworks robustos, como ORMs, sistemas de injeção de dependência e validações dinâmicas.

Este módulo cobre:
- Uso de **interfaces genéricas**.  
- Reflexão avançada com RTTI.  
- Atributos customizados para enriquecer o mapeamento.  
- Integração de RTTI + Interfaces em cenários reais.

---

## 2. Interfaces Genéricas
### 2.1 Exemplo Básico
```delphi
type
  IRepositorio<T: class> = interface
    ['{C9B4D2BA-AD8C-4DBB-A8F7-AC1F72644E87}']
    procedure Adicionar(AEntidade: T);
    function ObterTodos: TArray<T>;
  end;


---
uses Generics.Collections;

type
  TRepositorio<T: class, constructor> = class(TInterfacedObject, IRepositorio<T>)
  private
    FLista: TObjectList<T>;
  public
    constructor Create;
    procedure Adicionar(AEntidade: T);
    function ObterTodos: TArray<T>;
  end;

constructor TRepositorio<T>.Create;
begin
  FLista := TObjectList<T>.Create(True);
end;

procedure TRepositorio<T>.Adicionar(AEntidade: T);
begin
  FLista.Add(AEntidade);
end;

function TRepositorio<T>.ObterTodos: TArray<T>;
begin
  Result := FLista.ToArray;
end;