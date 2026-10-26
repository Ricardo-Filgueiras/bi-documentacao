## O que muda

<!-- Uma ou duas frases: o que este pull request corrige ou acrescenta e por quê. -->

## Checklist

- [ ] Os testes passam: `PYTHONUTF8=1 python -m unittest discover -s documentacao-bi/scripts/tests`.
- [ ] `claude plugin validate . --strict` passa.
- [ ] Se mudei instruções, scripts ou modelos, testei a skill de verdade com `claude --plugin-dir .` num portal de teste.
- [ ] **Se este PR deve chegar a quem usa o plugin, subi a versão em todos os lugares** (o plugin só atualiza quando o `version` muda): `.claude-plugin/plugin.json`, `SKILL.md`, primeira entrada do `CHANGELOG.md`, `README.md` e `referencias/relatorio-de-teste.md`.
- [ ] O `CHANGELOG.md` descreve a mudança.
- [ ] Uma situação nova que apareceu no uso foi registrada em `referencias/armadilhas.md`.

## Higiene (obrigatório)

- [ ] Nenhum nome de projeto, de pessoa ou de organização, nenhum dado de negócio, credencial real, caminho de usuário ou de máquina foi incluído (nem em exemplo, teste ou comentário).
- [ ] Exemplos e fixtures são sintéticos.
- [ ] Se descobri um termo que nunca deve aparecer no kit, acrescentei o **hash** dele a `documentacao-bi/scripts/tests/termos_proibidos.sha256` (`python documentacao-bi/scripts/tests/test_plugin.py --hash "termo"`), sem escrever o termo em nenhum arquivo.
