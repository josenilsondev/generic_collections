# Declaração de Classes e Métodos Genéricos

Em Delphi, é possível criar **classes e métodos genéricos** que trabalham com qualquer tipo, mantendo segurança de tipo em tempo de compilação.

---

## Exemplo em Delphi

```delphi


unit ClassesMetodosGenericos;

interface

uses
  System.SysUtils,
  System.Generics.Collections;

type

  TGeneric<T> = class
  private
    FItens: TList<T>;
  public
    constructor Create;
    destructor Destroy; override;
    procedure Adicionar(const AItem: T);
    function Buscar(const AIndex: Integer): T;
    procedure Listar;
  end;

implementation

{ TGeneric<T> }

constructor TGeneric<T>.Create;
begin
  FItens := TList<T>.Create;
end;

destructor TGeneric<T>.Destroy;
begin
  FItens.Free;
  inherited;
end;

procedure TGeneric<T>.Adicionar(const AItem: T);
begin
  FItens.Add(AItem);
end;

function TGeneric<T>.Buscar(const AIndex: Integer): T;
begin
  Result := FItens[AIndex];
end;

procedure TGeneric<T>.Listar;
var
  LItem: T;
begin
  for LItem in FItens do
    Writeln(LItem.ToString);
end;

end.
