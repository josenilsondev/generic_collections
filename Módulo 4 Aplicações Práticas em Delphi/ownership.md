\# OwnsObjects em TObjectList e TList



Quem é responsável por liberar a memória dos objetos armazenados na lista.

---



\## 📌 Conceitos



\### TObjectList<T> com OwnsObjects = True

\- A lista é dona dos objetos.  

\- Ao remover ou destruir a lista, os objetos também são destruídos.  

\- Evita memory leaks quando a lista é a \*\*única responsável\*\* pelos objetos.



\### TObjectList<T> com OwnsObjects = False

\- A lista não é dona dos objetos.  

\- Objetos precisam ser liberados manualmente ou por outro gerenciador.  

\- Útil quando há \*\*múltiplos donos\*\* de um objeto.



\### TList<T>

\- Lista simples de elementos.  

\- Não possui gerenciamento automático de memória para objetos.  

\- Serve apenas para tipos primitivos ou referências gerenciadas externamente.



---



\## 📌 Código



```delphi

unit ListasGenericas;



interface



uses

&nbsp; System.SysUtils,

&nbsp; System.Generics.Collections;



type

&nbsp; TCliente = class

&nbsp; private

&nbsp;   FNome: string;

&nbsp; public

&nbsp;   constructor Create(const ANome: string);

&nbsp;   property Nome: string read FNome;

&nbsp; end;



&nbsp; TListasGenericas = class

&nbsp; public

&nbsp;   procedure TObjectListTrue;

&nbsp;   procedure TObjectListFalse;

&nbsp;   procedure TList;

&nbsp; end;



implementation



constructor TCliente.Create(const ANome: string);

begin

&nbsp; FNome := ANome;

end;



procedure TListasGenericas.TObjectListTrue;

var

&nbsp; Lista: TObjectList<TCliente>;

begin

&nbsp; Lista := TObjectList<TCliente>.Create(True);

&nbsp; try

&nbsp;   Lista.Add(TCliente.Create('Cliente A'));

&nbsp;   Lista.Add(TCliente.Create('Cliente B'));

&nbsp;   Writeln('TObjectList<T> True - Total: ', Lista.Count);

&nbsp;   Lista.Delete(0);

&nbsp;   Writeln('Após exclusão: ', Lista.Count);

&nbsp; finally

&nbsp;   Lista.Free;

&nbsp; end;

end;



procedure TListasGenericas.TObjectListFalse;

var

&nbsp; Lista: TObjectList<TCliente>;

&nbsp; C1, C2: TCliente;

begin

&nbsp; Lista := TObjectList<TCliente>.Create(False);

&nbsp; try

&nbsp;   C1 := TCliente.Create('Cliente A');

&nbsp;   C2 := TCliente.Create('Cliente B');

&nbsp;   Lista.Add(C1);

&nbsp;   Lista.Add(C2);

&nbsp;   Writeln('TObjectList<T> False - Total: ', Lista.Count);

&nbsp;   Lista.Delete(0);

&nbsp;   Writeln('Após exclusão: ', Lista.Count);

&nbsp;   C1.Free;

&nbsp;   C2.Free;

&nbsp; finally

&nbsp;   Lista.Free;

&nbsp; end;

end;



procedure TListasGenericas.TList;

var

&nbsp; Lista: TList<TCliente>;

&nbsp; C1, C2: TCliente;

begin

&nbsp; Lista := TList<TCliente>.Create;

&nbsp; try

&nbsp;   C1 := TCliente.Create('Cliente A');

&nbsp;   C2 := TCliente.Create('Cliente B');

&nbsp;   Lista.Add(C1);

&nbsp;   Lista.Add(C2);

&nbsp;   Writeln('TList<T> - Total: ', Lista.Count);

&nbsp;   Lista.Delete(0);

&nbsp;   Writeln('Após exclusão: ', Lista.Count);

&nbsp;   C1.Free;

&nbsp;   C2.Free;

&nbsp; finally

&nbsp;   Lista.Free;

&nbsp; end;

end;



end.



