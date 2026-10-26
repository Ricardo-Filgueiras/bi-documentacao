<!-- Modelo do diagnóstico do modo "projeto existente" (Etapa 1). Copie para .agents/diagnostico-<slug>.md. Só leitura: nenhum arquivo do projeto é alterado para produzi-lo. Substitua o que está entre <>, apague os comentários e escreva "não se aplica" (com o motivo) no que não existir. -->
# Diagnóstico: <Projeto>

Data: AAAA-MM-DD. Só leitura. Slug do projeto: `<slug>` (ou "ainda não definido; proposta: `<slug>`").

## 1. Estado do Git

- Branch, se está sincronizada com o remoto, tags existentes.
- Mudanças pendentes: liste os arquivos e diga de onde vêm (por exemplo, salvar o projeto no Power BI Desktop). Pergunte ao desenvolvedor o que são antes de seguir.
- Como o repositório começou (por exemplo, com `.pbix` antes do PBIP): confira o início do histórico.

## 2. Onde estão os arquivos do Power BI

Pasta, nome do `.pbip` e das pastas `.SemanticModel` e `.Report`, e onde ficam os dados de apoio. Diga se o caminho segue `src/<slug>/` ou tem níveis a mais.

## 3. Caminho do repositório

Caminho da raiz, maior caminho versionado (em caracteres) e se está no OneDrive. Limite de alerta: ~240 caracteres.

## 4. Documentação existente

| Arquivo | Linhas | O que cobre | Data | Segue o padrão? |
|---|---:|---|---|---|
| | | | | sim / parcial / não |

Observações: números que não batem entre páginas, páginas que descrevem algo diferente do código, pipeline de publicação que existe só no nome (por exemplo, um arquivo de CI vazio).

## 5. Inventário do projeto

Saída de `levantamento.py` (cite o comando e a data).

| Indicador | Valor |
|---|---|
| Tabelas | |
| Colunas (calculadas) | |
| Relacionamentos (inativos) | |
| Medidas | |
| Medidas por pasta de exibição | |
| Medidas sem pasta | |
| Medidas com `///` | |
| Guias do relatório (ocultas) | |
| Visuais | |

Lembre que "sem uso" é o que o script detecta, não uma conclusão: confirme com o desenvolvedor antes de afirmar.

## 6. Comparação com o padrão

| Página do padrão | Existe hoje? | Onde | Situação |
|---|---|---|---|
| `readme.md` | | | aproveitável / adaptar / refazer / criar |
| `escopo.md` | | | |
| `como-usar.md` | | | |
| `regras-de-negocio.md` | | | |
| `guias-do-relatorio/` | | | |
| `modelo-de-dados.md` | | | |
| `medidas-dax/` | | | |
| `fontes-de-dados.md` | | | |
| `decisoes-tecnicas.md` | | | |
| `guia-do-desenvolvedor.md` | | | |
| `pendencias.md` | | | |
| `changelog.md` | | | |
| `arquivo/index.md` | | | |

Estrutura do portal:

| Item | Situação |
|---|---|
| `mkdocs.yml` | existe e está fora do padrão (propor fusão) / não existe |
| `docs/.nav.yml`, `docs/metodologia/`, `docs/stylesheets/extra.css`, `docs/changelog.md` | |
| `docs/projetos/<slug>/` e `src/<slug>/` | |
| `pyproject.toml` | |

## 7. Pontos para decisão do desenvolvedor

Numere cada decisão, com a proposta do agente quando houver. As respostas entram na tabela "Decisões já tomadas" do plano de migração.

1. Slug do projeto.
2. Onde ficam os arquivos do Power BI e dos dados.
3. O que fazer com mudanças pendentes antes da linha de base.
4. Portal com vários projetos ou um só.
5. <outros pontos que o diagnóstico levantou>
