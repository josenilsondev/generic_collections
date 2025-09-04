# Declaração de Classes e Métodos Genéricos

Em Delphi, é possível criar **classes e métodos genéricos** que trabalham com qualquer tipo, mantendo segurança de tipo em tempo de compilação.

---

## Exemplo em Delphi

```delphi
// 04/09/2025 - Autor: Josenilson - Projeto PDI Generics

unit ExemploClassesMetodosGenericos;

interface

uses
  System.SysUtils, System.Generics.Collections;

type
  // Classe genérica que funciona como repositório
  TRepositorio<T> = class
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

{ TRepositorio<T> }

constructor TRepositorio<T>.Create;
begin
  FItens := TList<T>.Create;
end;

destructor TRepositorio<T>.Destroy;
begin
  FItens.Free;
  inherited;
end;

procedure TRepositorio<T>.Adicionar(const AItem: T);
begin
  FItens.Add(AItem);
end;

function TRepositorio<T>.Buscar(const AIndex: Integer): T;
begin
  Result := FItens[AIndex];
end;

procedure TRepositorio<T>.Listar;
var
  LItem: T;
begin
  for LItem in FItens do
    Writeln(LItem.ToString);
end;

end.
