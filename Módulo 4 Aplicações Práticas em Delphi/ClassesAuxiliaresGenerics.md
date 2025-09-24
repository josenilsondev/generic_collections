Classes Auxiliares com Métodos Genéricos

## 🔎 Explicação
Classes auxiliares com métodos genéricos permitem criar **funções utilitárias reutilizáveis**, capazes de operar sobre diferentes tipos sem duplicar código.  
No Delphi, podemos centralizar regras de validação, conversão e manipulação de dados em uma unit auxiliar que será usada em todo o projeto.

Benefícios:
- Reaproveitamento de código.  
- Redução de redundância.  
- Escrita de funções mais legíveis e seguras.  
- Separação clara entre **lógica de negócio** e **funções utilitárias**.  

---

## ⚡ Código (`UHelperGenerics.pas`)

```delphi
unit UHelperGenerics;

interface

uses
  System.SysUtils, System.Generics.Collections, System.RegularExpressions;

type
  THelperGenerics = class
  public
    class function GetDefault<T>: T; static;
    class function IsDefault<T>(const AValue: T): Boolean; static;
    class function InList<T>(const AValue: T; const AList: TArray<T>): Boolean; static;
    class function OnlyNumbers(const AValue: string): string; static;
    class function IsCPF(const AValue: string): Boolean; static;
    class function IsCNPJ(const AValue: string): Boolean; static;
  end;

implementation

class function THelperGenerics.GetDefault<T>: T;
begin
  Result := Default(T);
end;

class function THelperGenerics.IsDefault<T>(const AValue: T): Boolean;
begin
  Result := AValue = Default(T);
end;

class function THelperGenerics.InList<T>(const AValue: T; const AList: TArray<T>): Boolean;
var
  LItem: T;
begin
  Result := False;
  for LItem in AList do
    if LItem = AValue then
      Exit(True);
end;

class function THelperGenerics.OnlyNumbers(const AValue: string): string;
begin
  Result := TRegEx.Replace(AValue, '\D', '');
end;

class function THelperGenerics.IsCPF(const AValue: string): Boolean;
var
  LNumbers: string;
begin
  LNumbers := OnlyNumbers(AValue);
  Result := Length(LNumbers) = 11;
end;

class function THelperGenerics.IsCNPJ(const AValue: string): Boolean;
var
  LNumbers: string;
begin
  LNumbers := OnlyNumbers(AValue);
  Result := Length(LNumbers) = 14;
end;

end.
🚀 Exemplos de Uso
1. Obter valores padrão
delphi
Copiar código
var
  LInt: Integer;
  LStr: string;
begin
  LInt := THelperGenerics.GetDefault<Integer>; // 0
  LStr := THelperGenerics.GetDefault<string>;  // ''
end;
2. Validar se é valor padrão
delphi
Copiar código
if THelperGenerics.IsDefault<Integer>(0) then
  Writeln('Zero é valor padrão');

if THelperGenerics.IsDefault<string>('') then
  Writeln('String está vazia');
3. Verificar se um valor pertence a uma lista
delphi
Copiar código
if THelperGenerics.InList<string>('Delphi', ['C#', 'Java', 'Delphi']) then
  Writeln('Achei o Delphi');
4. Extrair apenas números
delphi
Copiar código
Writeln(THelperGenerics.OnlyNumbers('(11) 98877-6655')); // "11988776655"
Writeln(THelperGenerics.OnlyNumbers('R$ 1.250,99'));     // "125099"
5. Validar CPF / CNPJ (simples, apenas tamanho)
delphi
Copiar código
if THelperGenerics.IsCPF('123.456.789-09') then
  Writeln('É um CPF válido');

if THelperGenerics.IsCNPJ('12.345.678/0001-99') then
  Writeln('É um CNPJ válido');