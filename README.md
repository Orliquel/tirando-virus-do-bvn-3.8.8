# Tirando vírus do BvN 3.8.8

Registro comunitário da análise de segurança dos arquivos associados ao jogo **Bleach vs. Naruto 3.8.8**. O objetivo é identificar quais componentes são maliciosos e documentar evidências verificáveis; separar ou modificar o jogo ainda não faz parte do escopo.

**Documentação organizada por um agente de IA do Orliquel (Codex), acompanhando a investigação solicitada por Orliquel.** As conclusões são provisórias e devem ser conferidas contra as evidências citadas.

## Situação

Há evidências fortes para tratar o executável como malicioso: o Microsoft Defender registrou detecções em cópias do arquivo, e 46 de 69 mecanismos do VirusTotal o sinalizaram. Isso é uma contagem de detecções, não uma probabilidade. A família exata, o payload e a função de cada componente da extração ainda não foram determinados.

O executável não está neste repositório. Também não publicamos arquivos da extração, relatórios brutos ou caminhos locais. A análise dinâmica controlada permanece sem resultado coletado; ausência de relatório não significa que o arquivo esteja limpo.

## Evidências e próximos passos

- [Estado atual e evidências](docs/estado-atual.md)
- [Como contribuir com segurança](CONTRIBUTING.md)
- [Registro do arquivo no VirusTotal](https://www.virustotal.com/gui/file/4281AA82E909EE9825436397897371788A10955AE53A0449140017B22CF8FE93/behavior)

Ajuda com fontes confiáveis, interpretação de indicadores e revisão da documentação é bem-vinda por Issues e Pull Requests. Não envie executáveis, arquivos compactados suspeitos, dumps ou dados pessoais.
