
---

### 📌 `cpp.md`
```markdown
# C++

- **Criada em:** 1985  
- **Generics (Templates) introduzidos em:** 1989 (C++98 padronizou)  
- **Documentação oficial:** [cppreference - Templates](https://en.cppreference.com/w/cpp/language/templates)

## Código

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Pessoa {
public:
    string nome;
    string sobrenome;
    int idade;

    Pessoa(string n, string s, int i) : nome(n), sobrenome(s), idade(i) {}
};

vector<Pessoa> lista;

void Cadastrar(string nome, string sobrenome, int idade) {
    lista.emplace_back(nome, sobrenome, idade);
}

void Listar() {
    for (auto& p : lista) {
        cout << p.nome << " " << p.sobrenome << " - " << p.idade << endl;
    }
}

int main() {
    Cadastrar("Ana", "Silva", 30);
    Cadastrar("João", "Souza", 25);
    Listar();
    return 0;
}
