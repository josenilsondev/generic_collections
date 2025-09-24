# Interação com Banco de Dados usando Generics e RTTI

## Explicação

Em Delphi, é possível criar repositórios genéricos (`TRepositorio<T>`) para abstrair operações comuns de banco de dados (CRUD). Usando **RTTI**, conseguimos mapear dinamicamente as propriedades de uma classe para colunas de uma tabela.

### Benefícios:

* Redução de código repetitivo
* Flexibilidade para reuso em várias entidades
* Melhor legibilidade e manutenção

---

## Exemplo

### Entidade Pessoa

```delphi
unit ModelPessoa;

interface

type
  TPessoa = class
  private
    FId: Integer;
    FNome: string;
    FEmail: string;
    FTelefone: string;
  public
    property Id: Integer read FId write FId;
    property Nome: string read FNome write FNome;
    property Email: string read FEmail write FEmail;
    property Telefone: string read FTelefone write FTelefone;
  end;

implementation

end.
```

---

### Repositório Genérico

```delphi
unit RepositorioGenerico;

interface

uses
  System.Rtti,
  System.SysUtils,
  System.Generics.Collections,
  ModelPessoa;

type
  TRepositorio<T: class, constructor> = class
  private
    FLista: TObjectList<T>;
  public
    constructor Create;
    destructor Destroy; override;

    procedure Inserir(AEntidade: T);
    procedure Remover(AEntidade: T);
    function Listar: TObjectList<T>;
    function BuscarPorId(AId: Integer): T;
  end;

implementation

{ TRepositorio<T> }

constructor TRepositorio<T>.Create;
begin
  FLista := TObjectList<T>.Create(True);
end;

destructor TRepositorio<T>.Destroy;
begin
  FLista.Free;
  inherited;
end;

procedure TRepositorio<T>.Inserir(AEntidade: T);
begin
  FLista.Add(AEntidade);
end;

procedure TRepositorio<T>.Remover(AEntidade: T);
begin
  FLista.Remove(AEntidade);
end;

function TRepositorio<T>.Listar: TObjectList<T>;
begin
  Result := FLista;
end;

function TRepositorio<T>.BuscarPorId(AId: Integer): T;
var
  LCtx: TRttiContext;
  LProp: TRttiProperty;
  LItem: T;
begin
  Result := nil;
  for LItem in FLista do
  begin
    LCtx := TRttiContext.Create;
    try
      LProp := LCtx.GetType(T).GetProperty('Id');
      if Assigned(LProp) and (LProp.GetValue(LItem).AsInteger = AId) then
        Exit(LItem);
    finally
      LCtx.Free;
    end;
  end;
end;

end.
```

---

### Uso do Repositório

```delphi
program TesteRepositorio;

{$APPTYPE CONSOLE}

uses
  System.SysUtils,
  ModelPessoa,
  RepositorioGenerico;

var
  Repositorio: TRepositorio<TPessoa>;
  Pessoa: TPessoa;
begin
  Repositorio := TRepositorio<TPessoa>.Create;
  try
    Pessoa := TPessoa.Create;
    Pessoa.Id := 1;
    Pessoa.Nome := 'Maria';
    Pessoa.Email := 'maria@email.com';
    Pessoa.Telefone := '99999-9999';
    Repositorio.Inserir(Pessoa);

    Writeln('Pessoa cadastrada: ', Repositorio.BuscarPorId(1).Nome);
  finally
    Repositorio.Free;
  end;
end.
```

---

## Resultado esperado (console)

```
Pessoa cadastrada: Maria
```


