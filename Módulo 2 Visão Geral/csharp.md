
---

### 📌 `csharp.md`
```markdown
# C#

- **Criada em:** 2000  
- **Generics introduzidos em:** 2005 (.NET 2.0)  
- **Documentação oficial:** [Microsoft - Generics](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/)

## Código

```csharp
using System;
using System.Collections.Generic;

class Pessoa {
    public string Nome { get; }
    public string Sobrenome { get; }
    public int Idade { get; }

    public Pessoa(string nome, string sobrenome, int idade) {
        Nome = nome;
        Sobrenome = sobrenome;
        Idade = idade;
    }
}

class Program {
    static List<Pessoa> lista = new List<Pessoa>();

    static void Cadastrar(string nome, string sobrenome, int idade) {
        lista.Add(new Pessoa(nome, sobrenome, idade));
    }

    static void Listar() {
        foreach (var p in lista) {
            Console.WriteLine($"{p.Nome} {p.Sobrenome} - {p.Idade}");
        }
    }

    static void Main() {
        Cadastrar("Ana", "Silva", 30);
        Cadastrar("João", "Souza", 25);
        Listar();
    }
}
