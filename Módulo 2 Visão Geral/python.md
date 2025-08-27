
---

### 📌 `python.md`
```markdown
# Python

- **Criada em:** 1991  
- **Generics introduzidos em:** 2015 (PEP 484 - typing, Python 3.5)  
- **Documentação oficial:** [Python - Typing](https://docs.python.org/3/library/typing.html)

## Código

```python
from typing import List

class Pessoa:
    def __init__(self, nome: str, sobrenome: str, idade: int):
        self.nome = nome
        self.sobrenome = sobrenome
        self.idade = idade

lista: List[Pessoa] = []

def cadastrar(nome: str, sobrenome: str, idade: int) -> None:
    lista.append(Pessoa(nome, sobrenome, idade))

def listar() -> None:
    for p in lista:
        print(f"{p.nome} {p.sobrenome} - {p.idade}")

if __name__ == "__main__":
    cadastrar("Ana", "Silva", 30)
    cadastrar("João", "Souza", 25)
    listar()
