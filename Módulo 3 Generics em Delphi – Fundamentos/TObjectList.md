
---

### 📌 `tobjectlist.md`

```markdown
# Exemplo com TObjectList<T>

**Explicação:**  
`TObjectList<T>` é uma lista de objetos genérica.  
Pode assumir a responsabilidade de liberar memória dos itens (`OwnsObjects = True`).

---

## Código

```delphi
unit ExemploTObjectList;

interface

uses
  System.SysUtils,
  System.Generics.Collections;

type
  TPessoa = class
  private
    FNome: string;
    FIdade: Integer;
  public
    constructor Create(const ANome: string; AIdade: Integer);
    property Nome: string read FNome;
    property Idade: Integer read FIdade;
  end;

  TExemploTObjectList = class
  private
    FLista: TObjectList<TPessoa>;
  public
    constructor Create;
    destructor Destroy; override;
    procedure Adicionar(const ANome: string; AIdade: Integer);
    function Buscar(const ANome: string): TPessoa;
    procedure Excluir(const ANome: string);
    procedure Listar;
  end;

implementation

constructor TPessoa.Create(const ANome: string; AIdade: Integer);
begin
  FNome := ANome;
  FIdade := AIdade;
end;

constructor TExemploTObjectList.Create;
begin
  FLista := TObjectList<TPessoa>.Create(True);
end;

destructor TExemploTObjectList.Destroy;
begin
  FLista.Free;
  inherited;
end;

procedure TExemploTObjectList.Adicionar(const ANome: string; AIdade: Integer);
begin
  FLista.Add(TPessoa.Create(ANome, AIdade));
end;

function TExemploTObjectList.Buscar(const ANome: string): TPessoa;
var
  LItem: TPessoa;
begin
  Result := nil;
  for LItem in FLista do
    if SameText(LItem.Nome, ANome) then
      Exit(LItem);
end;

procedure TExemploTObjectList.Excluir(const ANome: string);
var
  LItem: TPessoa;
begin
  for LItem in FLista do
    if SameText(LItem.Nome, ANome) then
    begin
      FLista.Remove(LItem);
      Break;
    end;
end;

procedure TExemploTObjectList.Listar;
var
  LItem: TPessoa;
begin
  for LItem in FLista do
    Writeln(LItem.Nome, ' - ', LItem.Idade);
end;

end.
