<!-- Modelo do plano de migração do modo "projeto existente" (Etapa 2). Copie para .agents/plano-migracao-<slug>.md. O plano é um documento vivo: depois de cada passo, o agente atualiza a "Situação de execução" e a data da conferência. Assim ele serve de linha do tempo do que foi feito e do que falta. Apague os blocos que não se aplicam e os comentários. -->
# Plano de migração: <slug>

Data: AAAA-MM-DD (revisado em <data>, ver "Revisões"). Situação: **<aprovado / aprovado em parte / em execução / concluído>**. Modo: projeto existente. Nível: <1>.

## Situação de execução (conferida em AAAA-MM-DD)

Uma linha por passo. O agente atualiza esta tabela a cada passo, depois de conferir no Git e no projeto o que foi feito.

| Passo | Situação | Conferência |
|---|---|---|
| A1 | feito / pendente / feito fora do plano | o que o agente verificou (commit, arquivo, comando) |

## Decisões já tomadas

| # | Decisão | Quem |
|---|---|---|
| 1 | <decisão> | desenvolvedor |

## Revisões

- **Revisão N (AAAA-MM-DD):** o que mudou no plano e por quê. Revisão nova entra no topo, e as antigas não são reescritas.

## Regras que valem em todos os passos

- O agente não altera nada dentro de `*.SemanticModel/` e `*.Report/`. O que mexe no Power BI é feito pelo desenvolvedor; o agente orienta e confere.
- O agente não faz commit, push nem branch. Exceção: a tag da linha de base, com autorização explícita.
- Um passo, um commit do desenvolvedor, e só depois a validação: o `mkdocs build --strict` falha em páginas novas ainda não commitadas.
- Após cada passo: `uv run mkdocs build --strict` e `git status --porcelain -- src/<slug>`.

## Passos

A coluna **Quem** diz quem executa: *desenvolvedor* ou *agente*.

### Bloco A: Preparar o repositório

| Passo | O que | Quem | Nível |
|---|---|---|---|
| A1 | Commit das mudanças pendentes do Power BI, com mensagem própria. | desenvolvedor | 1 |
| A2 | Commit de qualquer outra mudança pendente (documentação, `.gitignore`). | desenvolvedor | 1 |
| A3 | Tag anotada `<slug>/baseline-pre-documentacao` sobre o commit do A2, com autorização. Sem autorização, registre o hash do commit usado como linha de base. | agente | 1 |

### Bloco B: Mudar arquivos de lugar (só se não estiverem onde o padrão pede)

| Passo | O que | Quem | Nível |
|---|---|---|---|
| B1 | Mover o Power BI (e os dados de apoio) num commit só para isso. | desenvolvedor | 1 |
| B2 | Atualizar caminhos e parâmetros, abrir o projeto e atualizar os dados para provar que carrega. Commit próprio. | desenvolvedor | 1 |
| B3 | Conferir que os arquivos são idênticos aos da linha de base (`git diff -M --numstat`: só renomeações e ajustes de caminho). | agente | 1 |

### Bloco C: Estrutura do portal

| Passo | O que | Quem | Nível |
|---|---|---|---|
| C1 | Copiar de `modelos/portal/`: `docs/.nav.yml`, `docs/changelog.md`, `docs/stylesheets/extra.css`, `docs/projetos/.nav.yml`. | agente | 1 |
| C2 | Copiar `modelos/metodologia/` para `docs/metodologia/`. | agente | 1 |
| C3 | `mkdocs.yml`: mostrar a diferença para o modelo e propor a fusão, sem sobrescrever. | agente | 1 |
| C4 | `pyproject.toml`: acrescentar as dependências e rodar `uv sync`. | agente | 1 |
| C5 | `docs/index.md`: entrada do portal. O conteúdo anterior é aproveitado no `readme.md` do projeto. | agente | 1 |

### Bloco D: Páginas do projeto (uma por vez, com revisão)

Pasta de destino: `docs/projetos/<slug>/`. Cada página é conferida contra o script de levantamento e contra o código. O que não estiver nos arquivos vira `!!! pendente`.

| Passo | Página | Origem | Ação |
|---|---|---|---|
| D1 | `.nav.yml` do projeto | modelo | criar |
| D2 | `modelo-de-dados.md` e `medidas-dax/` | gerador | gerar com `gerar_paginas.py`; levar descrições existentes para acima do bloco `gerado` |
| D3 | `fontes-de-dados.md` | <origem> | <criar / adaptar> |
| D4 | `regras-de-negocio.md` | <origem> | |
| D5 | `guias-do-relatorio/` | relatório | |
| D6 | `escopo.md` | <origem> | |
| D7 | `guia-do-desenvolvedor.md` | <origem> | |
| D8 | `readme.md` | <origem> | |
| D9 | `decisoes-tecnicas.md` | histórico do Git | |
| D10 | `changelog.md` | <origem> | |
| D11 | `arquivo/index.md` | diagnóstico | |
| D12 | `como-usar.md` | | |
| D13 | `pendencias.md` | todas as páginas | reunir os `!!! pendente` |

### Bloco E: Fechamento

| Passo | O que | Quem | Nível |
|---|---|---|---|
| E1 | Tirar do portal as páginas antigas já migradas, depois de conferir de onde cada uma foi para (checklist "o que se perde"). Só com decisão do desenvolvedor. | agente | 1 |
| E2 | `mkdocs build --strict` sem avisos, `gerar_paginas.py --check` com código 0, e `src/<slug>/` igual à linha de base. | agente | 1 |
| E3 | Entrada de migração no changelog do projeto e uma linha no `docs/changelog.md` do portal. | agente | 1 |
| E4 | Resumo, checklist do PR, pauta de validação de negócio e relatório de teste. | agente | 1 |

## Fora deste plano

Itens dos níveis 2 e 3 (`niveis.md`) e decisões separadas, cada um com o motivo.

## Decisões abertas

| # | Decisão | Proposta do agente |
|---|---|---|
| 1 | | |
