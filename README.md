<div align="center">

# ♟️ Chess System

**Um jogo de xadrez completo, jogado direto no terminal, feito em Java puro.**

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Eclipse](https://img.shields.io/badge/Eclipse-IDE-2C2255?style=for-the-badge&logo=eclipseide&logoColor=white)
![OOP](https://img.shields.io/badge/Paradigma-POO-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Plataforma-Terminal-black?style=for-the-badge&logo=gnometerminal&logoColor=white)
![License](https://img.shields.io/badge/Licen%C3%A7a-MIT-green?style=for-the-badge)

[![Stars](https://img.shields.io/github/stars/CarlosLacerda/chess-system-java?style=flat-square&logo=github)](https://github.com/CarlosLacerda/chess-system-java/stargazers)
[![Forks](https://img.shields.io/github/forks/CarlosLacerda/chess-system-java?style=flat-square&logo=github)](https://github.com/CarlosLacerda/chess-system-java/network/members)
[![Last commit](https://img.shields.io/github/last-commit/CarlosLacerda/chess-system-java?style=flat-square&logo=git&logoColor=white)](https://github.com/CarlosLacerda/chess-system-java/commits)
[![Issues](https://img.shields.io/github/issues/CarlosLacerda/chess-system-java?style=flat-square)](https://github.com/CarlosLacerda/chess-system-java/issues)
![Top language](https://img.shields.io/github/languages/top/CarlosLacerda/chess-system-java?style=flat-square&color=ED8B00)

[Funcionalidades](#-funcionalidades) •
[Como executar](#-como-executar) •
[Como jogar](#-como-jogar) •
[Arquitetura](#-arquitetura) •
[Estrutura](#-estrutura-do-projeto)

</div>

---

## 📖 Sobre o projeto

O **Chess System** é um jogo de xadrez para dois jogadores executado no console. O projeto foi desenvolvido com foco em **Programação Orientada a Objetos**, separando a camada genérica de tabuleiro (`boardgame`) das regras específicas do xadrez (`chess`), e aplicando conceitos como herança, polimorfismo, classes abstratas, encapsulamento e tratamento de exceções.

O tabuleiro é renderizado com **cores ANSI** e, ao selecionar uma peça, as casas para onde ela pode se mover são destacadas em azul.

## ✨ Funcionalidades

- ✅ Tabuleiro 8x8 com todas as peças na posição inicial
- ✅ Movimentação correta de todas as peças: **Rei, Rainha, Torre, Bispo, Cavalo e Peão**
- ✅ Destaque visual dos **movimentos possíveis** da peça selecionada
- ✅ Alternância de turnos entre **brancas** e **pretas**
- ✅ Lista de **peças capturadas** por cor
- ✅ Detecção de **xeque** e **xeque-mate**
- ✅ Proibição de movimentos que deixem o próprio rei em xeque
- ✅ Movimentos especiais:

| Movimento | Descrição |
|---|---|
| 🏰 **Roque** | Pequeno (lado do rei) e grande (lado da dama) |
| 👻 **En passant** | Captura especial do peão |
| 👑 **Promoção** | O peão que chega ao fim do tabuleiro vira Bispo, Cavalo, Torre ou Rainha |

## 🧰 Tecnologias

- **Java 21**
- **Java Collections & Streams**
- **ANSI escape codes** para cores e limpeza de tela
- **Eclipse IDE** (projeto configurado para Eclipse)

## 🚀 Como executar

### Pré-requisitos

- [JDK 21](https://adoptium.net/) ou superior instalado
- Um terminal com suporte a cores ANSI (a maioria dos terminais modernos)

### Clonando o repositório

```bash
git clone https://github.com/CarlosLacerda/chess-system-java.git
cd chess-system-java
```

### Pelo terminal

```bash
# Compilar
mkdir -p bin
javac -d bin $(find src -name "*.java")

# Executar
java -cp bin application.Program
```

> 💡 No **Windows (PowerShell)**:
> ```powershell
> mkdir bin -Force
> javac -d bin (Get-ChildItem -Recurse src -Filter *.java).FullName
> java -cp bin application.Program
> ```

### Pelo Eclipse

1. `File` → `Import` → `General` → `Existing Projects into Workspace`
2. Selecione a pasta do projeto
3. Clique com o botão direito em `Program.java` → `Run As` → `Java Application`

> ⚠️ O console interno do Eclipse não interpreta bem os códigos ANSI. Para uma experiência melhor, rode pelo terminal ou instale o plugin *ANSI Escape in Console*.

## 🎮 Como jogar

1. O jogo começa com as **brancas**.
2. Informe a posição de **origem** da peça (ex: `e2`).
3. O tabuleiro mostrará em azul os movimentos possíveis.
4. Informe a posição de **destino** (ex: `e4`).
5. Repita alternando entre os jogadores até o **xeque-mate**.

```text
8 r n b q k b n r
7 p p p p p p p p
6 - - - - - - - -
5 - - - - - - - -
4 - - - - - - - -
3 - - - - - - - -
2 P P P P P P P P
1 R N B Q K B N R
  a b c d e f g h

Turn : 1
Waiting player: WHITE

Source: e2
```

As posições vão de **a1 a h8**. Entradas inválidas ou movimentos ilegais exibem uma mensagem de erro e pedem a jogada novamente.

### Legenda das peças

| Letra | Peça |
|:---:|---|
| `K` | Rei (King) |
| `Q` | Rainha (Queen) |
| `R` | Torre (Rook) |
| `B` | Bispo (Bishop) |
| `N` | Cavalo (Knight) |
| `P` | Peão (Pawn) |

Peças brancas aparecem em **branco** e peças pretas em **amarelo**.

## 🏗️ Arquitetura

O projeto é dividido em três camadas com responsabilidades bem definidas:

```text
┌──────────────────────────────────────────────┐
│  application   →  Interface com o usuário    │
│                   (Program, UI)              │
├──────────────────────────────────────────────┤
│  chess         →  Regras do xadrez           │
│                   (ChessMatch, ChessPiece,   │
│                    pieces/*)                 │
├──────────────────────────────────────────────┤
│  boardgame     →  Camada genérica de         │
│                   tabuleiro (Board, Piece,   │
│                   Position)                  │
└──────────────────────────────────────────────┘
```

### Conceitos aplicados

- **Abstração e herança** — `Piece` → `ChessPiece` → `King`, `Queen`, `Rook`, `Bishop`, `Knight`, `Pawn`
- **Polimorfismo** — cada peça implementa seu próprio `possibleMoves()`
- **Encapsulamento** — o tabuleiro e as peças expõem apenas o necessário
- **Exceções personalizadas** — `BoardException` e `ChessException`
- **Programação funcional** — uso de Streams e lambdas para filtrar peças em campo
- **Matrizes** — `boolean[][]` para representar movimentos possíveis

## 📁 Estrutura do projeto

```text
chess-system-java/
├── src/
│   ├── application/
│   │   ├── Program.java         # Loop principal do jogo
│   │   └── UI.java              # Impressão do tabuleiro e leitura de entrada
│   ├── boardgame/
│   │   ├── Board.java           # Tabuleiro genérico
│   │   ├── BoardException.java
│   │   ├── Piece.java           # Peça abstrata
│   │   └── Position.java        # Posição (linha, coluna)
│   └── chess/
│       ├── ChessMatch.java      # Regras, turnos, xeque e xeque-mate
│       ├── ChessPiece.java      # Peça de xadrez (cor, contagem de movimentos)
│       ├── ChessPosition.java   # Posição em notação de xadrez (a1–h8)
│       ├── ChessException.java
│       ├── Color.java           # WHITE / BLACK
│       └── pieces/
│           ├── King.java
│           ├── Queen.java
│           ├── Rook.java
│           ├── Bishop.java
│           ├── Knight.java
│           └── Pawn.java
└── README.md
```
## 🤝 Contribuindo

Contribuições são bem-vindas!

1. Faça um fork do projeto
2. Crie uma branch: `git checkout -b feature/minha-feature`
3. Commit suas mudanças: `git commit -m 'feat: minha feature'`
4. Push para a branch: `git push origin feature/minha-feature`
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença **MIT**. Veja o arquivo `LICENSE` para mais detalhes.

---

<div align="center">

Feito com ☕ e Java por [Carlos Lacerda](https://github.com/CarlosLacerda)

⭐ Se gostou do projeto, deixa uma estrela!

</div>
