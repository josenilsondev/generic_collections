
---

### 📌 `rust.md`
```markdown
# Rust

- **Criada em:** 2010  
- **Generics introduzidos em:** 2010 (desde a primeira versão)  
- **Documentação oficial:** [Rust - Generics](https://doc.rust-lang.org/book/ch10-01-syntax.html)

## Código

```rust
struct Pessoa {
    nome: String,
    sobrenome: String,
    idade: i32,
}

impl Pessoa {
    fn new(nome: &str, sobrenome: &str, idade: i32) -> Self {
        Pessoa {
            nome: nome.to_string(),
            sobrenome: sobrenome.to_string(),
            idade,
        }
    }
}

fn cadastrar(lista: &mut Vec<Pessoa>, nome: &str, sobrenome: &str, idade: i32) {
    lista.push(Pessoa::new(nome, sobrenome, idade));
}

fn listar(lista: &Vec<Pessoa>) {
    for p in lista {
        println!("{} {} - {}", p.nome, p.sobrenome, p.idade);
    }
}

fn main() {
    let mut lista: Vec<Pessoa> = Vec::new();
    cadastrar(&mut lista, "Ana", "Silva", 30);
    cadastrar(&mut lista, "João", "Souza", 25);
    listar(&lista);
}
