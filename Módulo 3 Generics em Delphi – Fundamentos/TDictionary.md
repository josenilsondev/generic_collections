# TDictionary<TKey, TValue>

**Explicação:**  
`TDictionary<TKey, TValue>` é usado para armazenar pares **chave/valor**.  
Permite buscas rápidas e impede chaves duplicadas.

---

## Exemplo em Delphi

```delphi
unit ExemploTDictionary;

interface

uses
  System.SysUtils, System.Generics.Collections;

type
  TExemploTDictionary = class
  private
    FMapa: TDictionary<string, Integer>;
  public
    constructor Create;
    destructor Destroy; override;
    procedure Adicionar(const AChave: string; AValor: Integer);
    function Buscar(const AChave: string): Integer;
    procedure Excluir(const AChave: string);
    procedure Listar;
  end;

implementation

constructor TExemploTDictionary.Create;
begin
  FMapa := TDictionary<string, Integer>.Create;
end;

destructor TExemploTDictionary.Destroy;
begin
  FMapa.Free;
  inherited;
end;

procedure TExemploTDictionary.Adicionar(const AChave: string; AValor: Integer);
begin
  FMapa.AddOrSetValue(AChave, AValor);
end;

function TExemploTDictionary.Buscar(const AChave: string): Integer;
begin
  if not FMapa.TryGetValue(AChave, Result) then
    raise Exception.Create('Chave não encontrada: ' + AChave);
end;

procedure TExemploTDictionary.Excluir(const AChave: string);
begin
  FMapa.Remove(AChave);
end;

procedure TExemploTDictionary.Listar;
var
  LPair: TPair<string, Integer>;
begin
  for LPair in FMapa do
    Writeln(LPair.Key, ' = ', LPair.Value);
end;

end.
