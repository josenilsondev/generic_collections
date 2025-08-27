
---

### 📌 `java.md`
```markdown
# Java

- **Criada em:** 1995  
- **Generics introduzidos em:** 2004 (Java 5 / J2SE 5.0)  
- **Documentação oficial:** [Oracle - Generics](https://docs.oracle.com/javase/tutorial/java/generics/)

## Código

```java
import java.util.ArrayList;
import java.util.List;

class Pessoa {
    String nome;
    String sobrenome;
    int idade;

    Pessoa(String nome, String sobrenome, int idade) {
        this.nome = nome;
        this.sobrenome = sobrenome;
        this.idade = idade;
    }
}

public class GenericsPessoa {
    private static List<Pessoa> lista = new ArrayList<>();

    public static void cadastrar(String nome, String sobrenome, int idade) {
        lista.add(new Pessoa(nome, sobrenome, idade));
    }

    public static void listar() {
        for (Pessoa p : lista) {
            System.out.println(p.nome + " " + p.sobrenome + " - " + p.idade);
        }
    }

    public static void main(String[] args) {
        cadastrar("Ana", "Silva", 30);
        cadastrar("João", "Souza", 25);
        listar();
    }
}
