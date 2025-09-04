# Tipos Genéricos em RTTI

O **RTTI (Run-Time Type Information)** permite inspecionar tipos em tempo de execução.  
Com generics, podemos descobrir **qual tipo foi usado no parâmetro** de uma classe genérica.

---

## Exemplo em Delphi

```delphi
// 04/09/2025 - Autor: Josenilson - Projeto PDI Generics

unit ExemploRTTIGenericos;

interface

uses
  System.SysUtils, System.Rtti, System.TypInfo;

type
  TContainer<T> = class
  private
    FValor: T;
  public
    constructor Create(const AValor: T);
    procedure MostrarTipo;
  end;

implementation

{ TContainer<T> }

constructor TContainer<T>.Create(const AValor: T);
begin
  FValor := AValor;
end;

procedure TContainer<T>.MostrarTipo;
var
  LRttiCtx: TRttiContext;
  LRttiType: TRttiType;
begin
  LRttiCtx := TRttiContext.Create;
  try
    LRttiType := LRttiCtx.GetType(Self.ClassType);

    Writeln('Classe genérica: ', LRttiType.Name);
    Writeln('Parâmetro usado: ', PTypeInfo(TypeInfo(T))^.Name);
    Writeln('Valor armazenado: ', FValor.ToString);
  finally
    LRttiCtx.Free;
  end;
end;

end.
