# Zero-Lero

Skill em português brasileiro que acha e remove os tiques de texto gerado por IA: "é importante ressaltar", "não se trata de X, trata-se de Y", o gerúndio de benefício ("...otimizando o seu dia a dia"), o parágrafo-fôrma de três frases, o fecho motivacional que ninguém pediu.

Existe skill equivalente em inglês, a [stop-slop](https://github.com/hardikpandya/stop-slop), do Hardik Pandya. Peguei o formato dela emprestado e joguei o conteúdo fora: o slop em pt-BR tem vícios que não existem em inglês (gerundismo, "conta com", "não é à toa que", a família inteira do "vale ressaltar"), então precisei de corpus próprio. Cada regra daqui carrega a frequência que eu medi.

## Exemplo

**Antes** (slop típico de blog):

> No mundo atual, cada vez mais conectado e dinâmico, o marketing digital deixou de ser um diferencial e se tornou uma necessidade. É importante ressaltar que não se trata apenas de vender mais. Trata-se de construir relacionamentos duradouros e significativos.

**Depois:**

> Pequenas empresas sem presença digital perdem clientes para concorrentes que aparecem primeiro na busca e respondem mais rápido no WhatsApp.

Tem mais 13 transformações comentadas em [references/exemplos.md](references/exemplos.md).

## Instalação

No Claude Code, clone para a pasta de skills:

```bash
git clone https://github.com/ViniciusStanula/Zero-Lero.git ~/.claude/skills/zero-lero
```

Depois é só chamar `/zero-lero` com o texto ou o caminho do arquivo. Ela também ativa sozinha quando você pede pra escrever, revisar ou editar prosa em pt-BR.

Em qualquer outro LLM funciona igual, porque é markdown puro. Cole o [SKILL.md](SKILL.md) no contexto e peça a revisão. Para passe profundo, cole junto os arquivos de [references/](references/).

## Como usar

Tem dois modos, e eles pedem doses diferentes.

**Revisando.** Você dá o texto, ela devolve cada ocorrência com citação, nome do padrão e correção sugerida, mais a pontuação. Quem decide o que aceitar é você: metade das vezes o padrão é voz deliberada do autor e fica.

**Escrevendo.** Com a skill no contexto, o texto já sai sem os vícios, mas cuidado com a mão pesada. Prompt que proíbe tudo gera texto picotado, que é slop ao contrário. Na geração eu veto só os 2-3 padrões de maior frequência e limpo o resto depois, na revisão.

A pontuação vai de 1 a 10 em cinco dimensões: Objetividade, Ritmo, Confiança no leitor, Autenticidade e Densidade. Abaixo de 35/50 vale outra passada. Ela serve pra forçar julgamento, e não pra ser gabaritada.

## O que a skill detecta

[references/frases.md](references/frases.md) tem 26 categorias de frases e expressões com frequência medida. A família "vale ressaltar", por exemplo, aparece 29× mais em slop do que em texto humano. No mesmo arquivo estão os 6 dialetos de registro que o slop veste conforme o gênero: juridiquês, academiquês, corporativês de press release, corporativês de desculpa (o do suporte), liturgia de plataforma (YouTube e threads) e reverência de nicho.

[references/estruturas.md](references/estruturas.md) tem os 20 padrões que Ctrl+F não acha: contraste binário (com e sem negação), falsa agência, gerúndio pós-vírgula, anáfora tripla, fôrmas de gênero, autenticidade fabricada. Essa última é a que aparece quando você pede "tom humano" pro modelo: "vou ser sincero", "kkk" calculado, "EDIT:" falso.

Os limiares são calibrados por padrão. Os que humano também usa ("de forma [adj]", "cada vez mais") só flagram por densidade. Os de taxa humana zero ("não é à toa", conclusão rotulada, "faz toda a diferença") flagram na segunda ocorrência.

Cada padrão carrega a taxa nos quatro corpora, e as quatro colunas não dizem a mesma coisa. "Conta com" e gerundismo são vícios do Claude e dão zero no GPT-5.5; "por isso" em cadeia e as formas modais do contraste binário são do GPT e quase somem no Claude. A tabela completa está em [references/frases.md](references/frases.md).

## Metodologia

Quatro rodadas, com os números no [CHANGELOG.md](CHANGELOG.md).

**v1, corpus de slop.** Gerei 24 textos em 8 gêneros sem nenhum freio anti-slop, contei os padrões por grep e li tudo procurando estrutura. As regras saíram das contagens. [Achados](docs/achados-corpus-v1.md).

**v2, teste adversarial.** Gerei outros 32 textos em 12 gêneros novos, sob 5 condições de prompt, e rodei a v1 como detector em cima deles. Capturou 35%. O slop tinha migrado junto com o registro e a v1 não sabia jurídico nem acadêmico nem thread. Tudo que escapou virou regra, e a cobertura foi pra ~95%, medida in-sample. [Achados](docs/achados-corpus-v2.md).

**v2.1, calibração humana.** Juntei 11 textos de blogs brasileiros pré-2022, quase 24 mil palavras, pra ter taxa-base humana por padrão. Daí saíram os limiares numéricos e a regra 13, a lista do que humano faz e IA não faz. [Achados](docs/achados-corpus-humano.md).

**v2.2, validação externa.** Gerei 10 textos no GPT-5.5, nos mesmos gêneros e condições, com temas novos, e passei as regras neles. Aqui a coisa ficou interessante, porque separou o que é vício de português do que é vício de modelo.

Cinco coisas que eu não esperava. Pedir "tom humano e natural" não remove o slop no Claude, só troca a pele dele por uma performance de espontaneidade — mas no GPT-5.5 a crônica pessoal saiu limpa e só a resenha performou, então talvez dependa do registro. O contraste binário tem versão positiva ("é mais do que X. É Y.") que passa batido por quem busca a negação, e mais cinco formas que eu só vi quando li um modelo diferente: uma thread do GPT tem sete reversões em 414 palavras e a skill pegava uma. "Experiência", que eu listava como léxico comercial inflado, aparece **mais** em texto humano do que em qualquer corpus de IA. Hedge não tem direção: o humano fica no meio, o Claude afirma demais e o GPT hedgeia tudo. E o parágrafo de IA tem um terço do tamanho do humano, 18,7 palavras contra 51,9 no GPT-5.5, o que faz do texto escaneável e fofinho o tell mais robusto que eu tenho.

## Limitações

O corpus GPT-5.5 tem 4.659 palavras, um quinto do corpus humano: serve para achar padrão, não para fixar taxa. Gemini continua pendente. A taxa de ~95% de cobertura da v2 segue in-sample, medida no corpus de onde as regras saíram — a v2.2 não a remediu, mostrou que parte das listas era específica do Claude. E quem julgou o que era slop nos textos do GPT fui eu, conhecendo as regras: as contagens são objetivas, a leitura não.

O corpus humano pesa demais para opinião e crônica de autor experiente, então gênero comercial escrito por gente pode ter taxa-base bem maior do que a que eu medi.

O slop também envelhece. Entre a v1 e a v2, "Em resumo" sumiu (16 ocorrências viraram 0) e reapareceu como "Resumindo:" e "Diante do exposto". As listas vão ficar velhas; o método de re-teste adversarial está no CHANGELOG justamente pra ser repetido.

Os corpora não vêm no repositório. O de controle humano tem texto de terceiros, usado só para análise.

Duas coisas que a skill nunca faz: alterar fato, número, nome ou compromisso ao limpar o texto, e passar por cima do guia de voz do cliente ou do estilo deliberado do autor.

## Licença e créditos

[MIT](LICENSE). Formato e sistema de pontuação inspirados na [stop-slop](https://github.com/hardikpandya/stop-slop) de Hardik Pandya, também MIT. Os padrões pt-BR são todos empíricos, com a metodologia completa no [CHANGELOG.md](CHANGELOG.md).
