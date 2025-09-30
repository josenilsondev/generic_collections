# Herança com Classes Genéricas em Delphi

## 📌 Introdução

Em Delphi, é possível criar classes genéricas que **herdam de outras classes genéricas**.  
Isso permite ampliar funcionalidades de forma estruturada, reaproveitando código e criando hierarquias flexíveis.

Com essa técnica, você pode definir comportamentos genéricos em uma classe base e, depois, especializar em classes derivadas.

---

##  Exemplo 1 

```delphi
type
  TRepositorioBase<T: class, constructor> = class
  public
    function Novo: T;
  end;

  TRepositorioPessoa<T: class, constructor> = class(TRepositorioBase<T>)
  public
    procedure Exibir(AObj: T);
  end;

function TRepositorioBase<T>.Novo: T;
begin
  Result := T.Create;
end;

procedure TRepositorioPessoa<T>.Exibir(AObj: T);
begin
  Writeln('Objeto: ' + AObj.ClassName);
end;

type
  TPessoa = class
    Nome: string;
  end;

var
  Repo: TRepositorioPessoa<TPessoa>;
  P: TPessoa;
begin
  Repo := TRepositorioPessoa<TPessoa>.Create;
  P := Repo.Novo;
  P.Nome := 'Maria';
  Repo.Exibir(P);
  P.Free;
  Repo.Free;
end;

---
##  Exemplo 1 
type
  TRepositorio<T: class, constructor> = class
  public
    procedure Salvar(AObj: T); virtual;
  end;

  TRepositorioCliente = class(TRepositorio<TPessoa>)
  public
    procedure Salvar(AObj: TPessoa); override;
  end;

procedure TRepositorio<T>.Salvar(AObj: T);
begin
  Writeln('Salvando objeto do tipo ' + AObj.ClassName);
end;

procedure TRepositorioCliente.Salvar(AObj: TPessoa);
begin
  Writeln('Salvando cliente: ' + AObj.Nome);
end;

var
  Repo: TRepositorioCliente;
  P: TPessoa;
begin
  Repo := TRepositorioCliente.Create;
  P := TPessoa.Create;
  P.Nome := 'João';
  Repo.Salvar(P);
  P.Free;
  Repo.Free;
end;

---
## Benefícios do Uso de Herança com Genéricos

Reaproveitamento de código: comportamentos comuns ficam na classe base.

Flexibilidade: classes derivadas podem estender ou sobrescrever comportamentos.

Segurança de tipo: generics garantem que os objetos tratados sejam do tipo esperado.

Facilidade de manutenção: permite centralizar regras comuns em um ponto único.

---
## Conclusão

Herança com classes genéricas em Delphi é uma técnica poderosa que combina polimorfismo com tipos genéricos, trazendo escalabilidade e robustez para projetos complexos.