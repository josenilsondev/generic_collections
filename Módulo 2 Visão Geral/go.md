# Go

- **Criada em:** 2009  
- **Generics introduzidos em:** 2022 (Go 1.18)  
- **Documentação oficial:** [Go - Generics](https://go.dev/doc/go1.18#generics)

## Código

```go
package main

import (
	"fmt"
)

type Pessoa struct {
	Nome      string
	Sobrenome string
	Idade     int
}

var lista []Pessoa

func Cadastrar(nome, sobrenome string, idade int) {
	lista = append(lista, Pessoa{Nome: nome, Sobrenome: sobrenome, Idade: idade})
}

func Listar() {
	for _, p := range lista {
		fmt.Printf("%s %s - %d\n", p.Nome, p.Sobrenome, p.Idade)
	}
}

func main() {
	Cadastrar("Ana", "Silva", 30)
	Cadastrar("João", "Souza", 25)
	Listar()
}
