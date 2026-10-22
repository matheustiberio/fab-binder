# FaB Binder

Organizador da minha coleção de **Flesh and Blood**: um app web (PC e celular, sincronizado) que cruza o catálogo de cartas de cada set com as quantidades que eu tenho, e calcula na hora o que falta para fechar os playsets (wants).

Os dados das cartas vêm do [the-fab-cube/flesh-and-blood-cards](https://github.com/the-fab-cube/flesh-and-blood-cards).

## Como funciona

- **Catálogo** (`catalog/catalog.json`): estático, diz quais cartas existem e o playset de cada uma. É gerado pelo CLI.
- **Coleção** (Firestore): guarda só as minhas quantidades, com a chave `Nome|Pitch`.
- **Web** (PWA no Firebase Hosting): cruza o catálogo com a coleção sempre que abre.

## Estrutura

```
cli/                      CLI em C# (.NET 10) que gera o catálogo
  src/Exporter/
  tests/
  FabBinder.sln
catalog/                  collection.config.json e catalog.json gerado
web/                      frontend (PWA)
firebase/                 rules, índices e config dos emuladores
.github/workflows/        geração do catálogo e deploy
```

## CLI

```bash
dotnet run --project cli/src/Exporter -- -c Guardian
```

| Opção | Descrição |
|---|---|
| `-c`, `--class` | Filtra por classe |
| `-s`, `--set` | Filtra por set |
| `-b`, `--branch` | Branch do fab-cube (padrão: `develop`) |

Hoje a saída vai para o clipboard, no formato `Qtd;Nome;Pitch;Raridade;Tipo;Foiling;Playset;Id`.
