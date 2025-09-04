# Exemplo com TList<T>

**Explicação:**  
`TList<T>` é uma lista genérica que pode armazenar qualquer tipo (primitivo ou objeto).  
Não gerencia automaticamente a memória de objetos.

---

## Código

```delphi
unit ExemploTList;

interface

uses
  System.SysUtils,
  System.Generics.Collections;

type
  TExemploTList = class
  private
    FLista: TList<string>;
  public
    constructor Create;
    destructor Destroy; override;
    procedure Adicionar(const AValor: string);
    function Buscar(const AValor: string): Integer;
    procedure Excluir(const AValor: string);
    procedure Listar;
  end;

implementation

constructor TExemploTList.Create;
begin
  FLista := TList<string>.Create;
end;

destructor TExemploTList.Destroy;
begin
  FLista.Free;
  inherited;
end;

procedure TExemploTList.Adicionar(const AValor: string);
begin
  FLista.Add(AValor);
end;

function TExemploTList.Buscar(const AValor: string): Integer;
begin
  Result := FLista.IndexOf(AValor);
end;

procedure TExemploTList.Excluir(const AValor: string);
var
  LIndex: Integer;
begin
  LIndex := FLista.IndexOf(AValor);
  if LIndex >= 0 then
    FLista.Delete(LIndex);
end;

procedure TExemploTList.Listar;
var
  LItem: string;
begin
  for LItem in FLista do
    Writeln(LItem);
end;

end.
