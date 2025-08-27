
---

### 📌 `kotlin.md`
```markdown
# Kotlin

- **Criada em:** 2011  
- **Generics introduzidos em:** 2011 (desde a primeira versão)  
- **Documentação oficial:** [Kotlin - Generics](https://kotlinlang.org/docs/generics.html)

## Código

```kotlin
data class Pessoa(val nome: String, val sobrenome: String, val idade: Int)

val lista: MutableList<Pessoa> = mutableListOf()

fun cadastrar(nome: String, sobrenome: String, idade: Int) {
    lista.add(Pessoa(nome, sobrenome, idade))
}

fun listar() {
    for (p in lista) {
        println("${p.nome} ${p.sobrenome} - ${p.idade}")
    }
}

fun main() {
    cadastrar("Ana", "Silva", 30)
    cadastrar("João", "Souza", 25)
    listar()
}
