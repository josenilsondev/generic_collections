# Delphi

- **Criada em:** 1995  
- **Generics introduzidos em:** 2009 (Delphi 2009)  
- **Documentação oficial:** [Embarcadero - Generics](https://docwiki.embarcadero.com/RADStudio/en/Generics_in_Delphi)

## Código

```delphi
program GenericsPessoa;

{$APPTYPE CONSOLE}

uses
  System.SysUtils,
  System.Generics.Collections;

type
  TPessoa = class
  private
    FNome: string;
    FSobrenome: string;
    FIdade: Integer;
  public
    constructor Create(const ANome, ASobrenome: string; AIdade: Integer);
    property Nome: string read FNome;
    property Sobrenome: string read FSobrenome;
    property Idade: Integer read FIdade;
  end;

var
  Lista: TObjectList<TPessoa>;

constructor TPessoa.Create(const ANome, ASobrenome: string; AIdade: Integer);
begin
  FNome := ANome;
  FSobrenome := ASobrenome;
  FIdade := AIdade;
end;

procedure Cadastrar(const ANome, ASobrenome: string; AIdade: Integer);
begin
  Lista.Add(TPessoa.Create(ANome, ASobrenome, AIdade));
end;

procedure Listar;
var
  P: TPessoa;
begin
  for P in Lista do
    Writeln(P.Nome, ' ', P.Sobrenome, ' - ', P.Idade);
end;

begin
  Lista := TObjectList<TPessoa>.Create(True);
  try
    Cadastrar('Ana', 'Silva', 30);
    Cadastrar('João', 'Souza', 25);
    Listar;
  finally
    Lista.Free;
  end;
end.
