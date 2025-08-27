
---

### 📌 `typescript.md`
```markdown
# TypeScript

- **Criada em:** 2012  
- **Generics introduzidos em:** 2012 (desde a primeira versão)  
- **Documentação oficial:** [TypeScript - Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)

## Código

```typescript
class Pessoa {
  nome: string;
  sobrenome: string;
  idade: number;

  constructor(nome: string, sobrenome: string, idade: number) {
    this.nome = nome;
    this.sobrenome = sobrenome;
    this.idade = idade;
  }
}

let lista: Array<Pessoa> = [];

function cadastrar(nome: string, sobrenome: string, idade: number): void {
  lista.push(new Pessoa(nome, sobrenome, idade));
}

function listar(): void {
  lista.forEach(p => {
    console.log(`${p.nome} ${p.sobrenome} - ${p.idade}`);
  });
}

cadastrar("Ana", "Silva", 30);
cadastrar("João", "Souza", 25);
listar();
