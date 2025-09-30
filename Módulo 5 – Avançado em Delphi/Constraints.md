# Constraints em Generics no Delphi

##  O que são?

Constraints são **restrições aplicadas aos parâmetros de tipo genéricos** em Delphi.  
Elas determinam quais tipos podem ser usados em classes, métodos ou interfaces genéricas.

Com isso, conseguimos garantir em **tempo de compilação** que apenas tipos adequados sejam utilizados, evitando problemas de compatibilidade e erros de execução.

---

## Tipos de Constraints

1. **`class`**  
   - Restringe o tipo a classes (não aceita registros ou tipos primitivos).  
   - Exemplo: `T<T: class>`.

2. **`record`**  
   - Restringe o tipo a registros.  
   - Exemplo: `T<T: record>`.

3. **`constructor`**  
   - Exige que o tipo possua um construtor padrão (`Create`).  
   - Exemplo: `T<T: constructor>`.

4. **Herança ou Interface específica**  
   - Permite restringir para tipos descendentes de uma classe ou que implementem uma interface.  
   - Exemplo: `T<T: TEntidade>` ou `T<T: IInterface>`.

5. **Combinação**  
   - É possível combinar várias restrições.  
   - Exemplo: `T<T: class, TEntidade, constructor>`.

---

## Exemplo 

### Classe Base
```delphi
type
  TEntidade = class
  private
    FId: Integer;
  public
    property Id: Integer read FId write FId;
  end;

type
  TPessoa = class(TEntidade)
  private
    FNome: string;
  public
    property Nome: string read FNome write FNome;
  end;

type
  TRepositorio<T: class, TEntidade, constructor> = class
  public
    function Novo: T;
    procedure Salvar(AObj: T);
  end;

function TRepositorio<T>.Novo: T;
begin
  Result := T.Create;
end;

procedure TRepositorio<T>.Salvar(AObj: T);
begin
  Writeln('Salvando entidade Id=' + AObj.Id.ToString);
end;

var
  RepoPessoa: TRepositorio<TPessoa>;
  Pessoa: TPessoa;
begin
  RepoPessoa := TRepositorio<TPessoa>.Create;

  Pessoa := RepoPessoa.Novo;
  Pessoa.Id := 1;
  Pessoa.Nome := 'João da Silva';

  RepoPessoa.Salvar(Pessoa);

  Pessoa.Free;
  RepoPessoa.Free;
end;
