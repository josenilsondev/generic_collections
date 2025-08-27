
---

### 📌 `swift.md`
```markdown
# Swift

- **Criada em:** 2014  
- **Generics introduzidos em:** 2014 (desde a primeira versão)  
- **Documentação oficial:** [Swift - Generics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/generics/)

## Código

```swift
class Pessoa {
    var nome: String
    var sobrenome: String
    var idade: Int

    init(nome: String, sobrenome: String, idade: Int) {
        self.nome = nome
        self.sobrenome = sobrenome
        self.idade = idade
    }
}

var lista: [Pessoa] = []

func cadastrar(nome: String, sobrenome: String, idade: Int) {
    lista.append(Pessoa(nome: nome, sobrenome: sobrenome, idade: idade))
}

func listar() {
    for p in lista {
        print("\(p.nome) \(p.sobrenome) - \(p.idade)")
    }
}

cadastrar(nome: "Ana", sobrenome: "Silva", idade: 30)
cadastrar(nome: "João", sobrenome: "Souza", idade: 25)
listar()
