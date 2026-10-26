# bi-documentacao

Repositório: <https://github.com/Ricardo-Filgueiras/bi-documentacao> (privado)

Skill e plugin do Claude Code para criar e manter a documentação de projetos Power BI (PBIP) num portal único em MkDocs. Tudo o que é preciso está aqui, na forma de uma **skill**: `documentacao-bi/` (versão 0.3.1, em teste).

Origem: revisão do conselho de arquitetura da documentação (2026-10).

## O que tem aqui

```
.claude-plugin/              ← plugin.json e marketplace.json
.github/                     ← workflow de testes e template de pull request
documentacao-bi/             ← a skill
├── SKILL.md                    ← instruções para o agente
├── CHANGELOG.md                ← versões da skill
├── referencias/
│   ├── padrao.md               ← índice do padrão
│   ├── padrao-estrutura.md, padrao-escrita.md, padrao-paginas.md,
│   │   padrao-git.md, padrao-mkdocs.md  ← o padrão por tema, com o porquê de cada regra
│   ├── armadilhas.md           ← situação inesperada → decisão tomada
│   ├── distribuicao.md         ← plugin, versão, atualização e release
│   ├── decisao-mkdocs.md       ← critérios para manter ou trocar o MkDocs
│   ├── modo-projeto-existente.md
│   ├── modo-projeto-novo.md
│   ├── niveis.md               ← o que entra agora e o que fica para depois
│   ├── educacao-mantenedores.md
│   └── relatorio-de-teste.md   ← o que o agente devolve ao fim de cada sessão
├── modelos/
│   ├── portal/                 ← raiz do portal: mkdocs.yml, pyproject.toml, gitignore, README, docs/
│   ├── metodologia/            ← dataops.md e versionamento-git.md, já genéricos e corrigidos
│   ├── projeto/                ← páginas de um projeto, com o menu (.nav.yml)
│   ├── migracao/               ← diagnóstico e plano de migração (modo projeto existente)
│   └── itens/                  ← modelo de guia, de pasta de medidas e de medida
└── scripts/
    ├── levantamento.py         ← contagens, dependências entre medidas e --preflight
    ├── gerar_paginas.py        ← gera modelo-de-dados.md e medidas-dax/ direto do modelo
    ├── extrair_etl.py          ← gera etl-python.md das docstrings dos scripts Python
    ├── comparar_portal.py      ← mostra o que mudou nos modelos desde que o portal foi criado
    └── tests/                  ← testes dos scripts + PBIP de exemplo (fixture)
```

## Como instalar

**Opção recomendada: plugin** (versionado, com atualização). Este repositório é, ao mesmo tempo, o plugin (`.claude-plugin/plugin.json`) e o marketplace (`.claude-plugin/marketplace.json`). Em cada máquina ou repositório de portal:

```bash
claude plugin marketplace add Ricardo-Filgueiras/bi-documentacao
claude plugin install documentacao-bi@bi-documentacao --scope project
```

A skill passa a existir como `/documentacao-bi:documentacao-bi`. Para atualizar, veja `documentacao-bi/referencias/distribuicao.md` (a atualização só chega quando o campo `version` do `plugin.json` muda). Para testar uma mudança antes de lançar: `claude --plugin-dir <pasta deste repositório>`.

**Alternativa: copiar a pasta.** Copie `documentacao-bi/` para `<portal>/.claude/skills/documentacao-bi/`. Funciona, mas cada cópia envelhece sozinha.

Depois, em qualquer das opções:

1. **Repositório num caminho curto, fora do OneDrive** (por exemplo `C:\repos\<portal>`).
2. Crie a pasta `<portal>/.agents/relatorios-skill/` para os relatórios de teste.
3. Abra o Claude Code na raiz do portal e peça, por exemplo: *"Use a skill documentacao-bi para documentar este projeto. É um projeto existente."*
4. O agente faz primeiro o **diagnóstico** (só leitura) e o **plano de migração**, e espera a sua aprovação antes de alterar qualquer coisa.

## Como trazer o resultado de volta

Ao fim de cada sessão, o agente do projeto novo escreve um relatório em `.agents/relatorios-skill/AAAA-MM-DD-sessao-N.md`. Traga esse arquivo para quem mantém a skill. Com ele, a skill é corrigida e ganha uma versão nova (0.4.0, …). Com o plugin, quem usa atualiza com um comando; se você copiou a pasta, copie de novo.

## Como contribuir e lançar uma versão

Mudanças entram por pull request; o template lembra do que conferir. O workflow `testes` roda os testes em Windows e Linux. Para rodar localmente:

```bash
PYTHONUTF8=1 python -m unittest discover -s documentacao-bi/scripts/tests
claude plugin validate . --strict
```

O plugin só atualiza para quem o usa quando o campo `version` do `plugin.json` muda; o passo a passo do release está em `documentacao-bi/referencias/distribuicao.md`. Nada de nome de projeto, dado de negócio ou credencial entra neste repositório: um teste confere termos proibidos por hash.

## O que ainda depende de você

- **Nome do projeto (slug):** o agente vai perguntar. O mesmo nome vale para `src/<slug>/` e `docs/projetos/<slug>/`.
- **Mudar as pastas do Power BI para `src/<slug>/`:** se precisar, é você quem faz, num commit só para isso. O agente orienta e confere.
- **Commits e pull request:** o agente não faz commit. Você revisa e abre o PR.
# bi-documentacao
