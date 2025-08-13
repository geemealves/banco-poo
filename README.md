# Banco Digital – Projeto de POO (DIO)

Simulação de um **sistema bancário de console** para consolidar conceitos de Programação Orientada a Objetos (POO): **abstração, encapsulamento, herança, polimorfismo** e **reuso de código**. O projeto inclui criação de clientes e contas (corrente, poupança, investimento), **depósitos, saques, transferências (PIX)**, registro de **histórico de transações** e um **menu interativo**.

---

## 🎯 Objetivos de Aprendizagem

* Aplicar conceitos de POO com herança e composição.
* Implementar entidades, serviços e repositórios em memória.
* Usar enums e records para modelagem mais expressiva.
* Construir um menu de fluxo interativo via console.
* Documentar de forma clara e publicar no GitHub.

---

## 🏗️ Arquitetura e Conceitos de POO

**Entidades (modelo):**

* `Conta` (abstrata)

  * Atributos: `numero`, `titular`, `saldo`, `historico`
  * Métodos: `depositar`, `sacar`, `transferir`, `exibirDetalhes()` (abstrato)
* `ContaCorrente`, `ContaPoupanca`, `ContaInvestimento` (herdam de `Conta`)

  * `ContaInvestimento` inclui `investir(valor)`
* `Cliente` (possui várias contas – *composição*)
* `Transacao` (record) – `tipo`, `valor`, `dataHora`
* `TipoTransacao` (enum) – `DEPOSITO`, `SAQUE`, `PIX`, `INVESTIMENTO`

**Repositórios (em memória):**

* `RepositorioClientes` – CRUD simples de clientes
* `RepositorioContas` – busca por número, listagem

**Serviço:**

* `ServicoBancario` – orquestra criação de clientes/contas e operações

**Menu (console):**

* `Main` – interface de texto para interação

**Mapeamento POO:**

* **Abstração:** `Conta` define o essencial das contas.
* **Encapsulamento:** atributos privados/protegidos + getters/setters quando necessário.
* **Herança:** contas específicas estendem `Conta`.
* **Polimorfismo:** operações tratam `Conta` de forma geral (corrente/poupança/investimento).
* **Composição:** `Cliente` *tem* uma coleção de `Conta`; `Conta` *tem* uma coleção de `Transacao`.

---

## 🗂️ Estrutura de Pastas Sugerida

```
src/
 └── br/com/banco
      ├── Main.java
      ├── modelo/
      │     ├── Conta.java
      │     ├── ContaCorrente.java
      │     ├── ContaPoupanca.java
      │     ├── ContaInvestimento.java
      │     ├── Cliente.java
      │     ├── Transacao.java
      │     └── TipoTransacao.java
      ├── repositorio/
      │     ├── RepositorioClientes.java
      │     └── RepositorioContas.java
      └── servico/
            └── ServicoBancario.java

images/               # (opcional) capturas de tela do menu
README.md
.gitignore
LICENSE (opcional)
```

> O projeto é **Java puro** (sem build tool). Se preferir, você pode criar um `pom.xml` (Maven) ou `build.gradle` (Gradle). A execução abaixo considera compilação com `javac`.

---

## ✅ Pré‑requisitos

* **Java 17+** instalado e no PATH
* (Opcional) **Lombok** se você decidir usar anotações (este projeto funciona sem Lombok)

Verifique a versão:

```bash
java -version
javac -version
```

---

## ▶️ Como Compilar e Executar

**Linux/macOS (bash):**

```bash
# dentro da raiz do projeto
find ./src -name "*.java" > sources.txt
mkdir -p out
javac -d out @sources.txt
java -cp out br.com.banco.Main
```

**Windows (PowerShell):**

```powershell
# dentro da raiz do projeto
Get-ChildItem -Recurse -Filter *.java | % FullName | Set-Content sources.txt
New-Item -ItemType Directory -Force -Path out | Out-Null
javac -d out @sources.txt
java -cp out br.com.banco.Main
```

> Se preferir IDE (IntelliJ/Eclipse/VS Code), importe o projeto como **Java Project** e defina `br.com.banco.Main` como classe principal.

---

## 🧪 Exemplo de Uso (Fluxo)

1. **Criar cliente:** informe nome e CPF.
2. **Criar conta:** escolha tipo (corrente/poupança/investimento) e número da conta.
3. **Operações:**

   * **Depositar**: crédito no saldo + registro em `historico`
   * **Sacar**: débito se houver saldo + registro
   * **PIX**: `transferir` de uma conta para outra
   * **Investir** (conta investimento): debita e registra transação de investimento
4. **Consultar histórico:** listar as `Transacao` com data/hora e tipo

---

## 🧱 Decisões de Projeto

* **Sem persistência**: repositórios em memória para foco em POO.
* **Record + Enum**: `Transacao` como `record` reduz boilerplate e `TipoTransacao` dá segurança de tipo.
* **Responsabilidades claras**: menu em `Main`, regras no `ServicoBancario`, dados em `repositorio/`.

---

## 🧰 .gitignore sugerido

```gitignore
# Build
out/
bin/
target/

# IDEs
*.iml
.idea/
.vscode/
.project
.classpath
.settings/

# SO
.DS_Store
Thumbs.db
```

---

## 🧭 Roteiro de Entrega (Checklist)

* [ ] Código compila e roda pelo console
* [ ] README completo com instruções e imagens
* [ ] Estrutura de pacotes organizada
* [ ] Commits com mensagens claras
* [ ] Repositório **público** no GitHub
* [ ] Link enviado na plataforma (DIO)

---

## 📄 Licença

Este projeto pode ser distribuído sob a licença **MIT**. Crie um arquivo `LICENSE` ou utilize o botão “Add license” no GitHub.

---

## 📚 Recursos Úteis

* Documentação Java: [https://docs.oracle.com/en/java/](https://docs.oracle.com/en/java/)
* GitHub Docs (Markdown): [https://docs.github.com/en](https://docs.github.com/en)
* Git (básico): `git init`, `git add .`, `git commit -m`, `git push`
