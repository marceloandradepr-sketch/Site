# Changelog

## v2.2 — 2026-08-07 — Validação externa (GPT-5.5) e ferramental

Primeira rodada com outro modelo, que era a pendência principal da v3. Corpus de 10 textos (4.659 palavras) gerados no GPT-5.5, nos mesmos 10 gêneros do v1/v2 e sob as mesmas 5 condições de prompt, com temas novos. Um chat limpo por texto, sem follow-up, sem mencionar estilo no prompt. Os textos não acompanham o repositório.

### O que sobreviveu à troca de modelo

O tell estrutural, e mais forte do que antes. Parágrafo médio: humano 51,9 palavras, Claude v1 25,4, Claude v2 28,3, **GPT-5.5 18,7**. A tese central da v2.1 é a única parte da skill que não depende de qual modelo escreveu.

Também sobreviveram a família "ressaltar" (1,29 no GPT contra 0,00 humano), o gerúndio pós-vírgula, o léxico comercial e os registros de suporte e press release.

### O que era do Claude, não do português

Deram **zero** no GPT-5.5 e davam 0,5 a 1,4 por mil no Claude v1: "conta com", "cada vez mais", "através de", gerundismo, tendência vaga em gerúndio, atribuição evasiva, falsa causalidade. As regras não estão erradas; estavam apresentadas como "slop em pt-BR" quando descrevem um modelo. `references/frases.md` agora traz taxa por corpus.

### Padrões novos

1. **Contraste binário em cinco formas novas** (1,50 no GPT, taxa humana zero): modal ("não deve ser X"), pronominal ("não é aquele que X. É aquele que Y."), causal ("não é porque X. É porque Y."), contrafactual ("X, quando deveria Y") e aposta pós-posta ("Não uma estratégia."). Uma thread do corpus tem **7 reversões em 414 palavras** e só 1 casava com as regras anteriores. O padrão nº 1 do repo estava sub-especificado.
2. **"Por isso" em cadeia** (2,36 no GPT contra 0,29 humano). O conectivo do GPT, ausente da lista, que era montada em cima do "Além disso" do Claude.
3. **Hedge com sinal invertido.** Claude 2,04, humano 4,95, GPT-5.5 7,73. O humano fica no meio: hedge de menos é tell de um modelo, hedge demais é tell do outro. Documentado como diagnóstico, não como corte.
4. **Anúncio de estrutura fora do acadêmico** ("Neste artigo, você encontrará..."). A família só estava registrada na variante de paper.

### Correções

- **"experiência" saiu da lista frasal.** Taxa humana 3,44 por mil, acima dos três corpora de IA. Humano usa mais que máquina. Vira nota contextual.
- **"completo/completa" sozinho** dava falso positivo em português normal ("a fôrma completa"). Restrito às colocações comerciais.
- **`não se trata apenas de X` não era detectado** por nenhuma das duas entradas listadas — a combinação escapava das duas.

### Sobre a medição

As contagens desta rodada saíram de scripts de apoio (39 regex, uma por família, mais média de parágrafo), mantidos fora do repositório junto com os corpora. O repositório continua sendo só a skill em markdown.

Vale registrar três coisas que a medição automatizada corrigiu, porque afetam as listas:

1. **Regex de duas ou mais palavras não atravessa quebra de linha.** As contagens anteriores, feitas por grep em markdown com wrap, subestimavam qualquer padrão de mais de uma palavra ("deixou de ser um / diferencial e se tornou" era invisível).
2. **50 das taxas registradas à mão estavam erradas.** Nenhuma por muito, mas o limiar depende delas.
3. **"não se trata apenas de X" não casava com nenhuma das duas entradas listadas.** É a forma mais comum do padrão nº 1.

### Separação atual, em famílias acima do limiar por 1000 palavras

| Corpus | Flags por 1000 palavras | Parágrafo médio |
|---|---|---|
| Humano | 0,21 | 51,9 |
| Claude v2 | 5,44 | 28,3 |
| GPT-5.5 | 5,58 | 18,7 |
| Claude v1 | 15,26 | 25,4 |

### Ressalvas

O corpus GPT tem 10 textos e 4.659 palavras, um quinto do corpus humano: serve para achar padrão, não para fixar taxa. Quem classificou o que era slop fui eu, conhecendo as regras — os hits são objetivos, a leitura não. Gemini continua pendente.

Uma hipótese que a rodada não confirmou nem derrubou: no Claude, pedir "tom humano" produz espontaneidade performada em 100% dos casos; no GPT-5.5 apareceu na resenha e não na crônica pessoal, que saiu limpa. Pode depender do registro. São 2 textos.

## v2.1 — 2026-06-12 — Calibração com corpus de controle humano

Coletados 11 textos humanos em pt-BR (~23.750 palavras), todos pré-2022 ou de autoria humana verificável: Manual do Usuário (tech, 4), Scream & Yell (crítica musical, 2), crônicas de Medium (2), Clube dos Poupadores (finanças, 1), PratoFundo (gastronomia, 2). Coleta via curl + extração local (`../corpus-humano/extrair.py`) — WebFetch foi descartado porque o modelo intermediário parafraseia a prosa. Achados em [docs/achados-corpus-humano.md](docs/achados-corpus-humano.md).

Resultados aplicados à skill:

- **Limiares de densidade com número.** "Densidade é o tell" virou calibração: padrões com taxa humana > 0 ("de forma [adj]" 0,21/1000, "cada vez mais" 0,17, "através de" 0,25) flagram a partir de ~3-4× a base; padrões com taxa humana zero ("não é à toa", "vem + gerúndio" vago, conclusão rotulada, "faz toda a diferença", "verdadeiro [X]") são discriminadores quase perfeitos — duas ocorrências num texto são evidência forte.
- **Tell estrutural novo:** parágrafo de IA tem média de 26-29 palavras; humano, 54, com variabilidade maior. Texto inteiro em parágrafos escaneáveis de 2-3 frases é fôrma.
- **Regra 13 (anti-tells):** sete marcas de humanidade ausentes do slop (digressão sem volta, palpite assumido, referência cravada, autocontradição em primeira pessoa, frase torta a favor do ritmo, final sem cerimônia) — documentadas como direção de reescrita, não como checklist fabricável.
- Confirmação independente do achado v2: no slop espontâneo, as taxas frasais caem para perto das humanas; a detecção pesa sobre estrutura, registro e fôrma.

Limitações: corpus humano enviesado para opinião/crônica de autores experientes; sem gêneros comerciais humanos (e-commerce, email real), cujas taxas-base podem ser maiores.

## v2 — 2026-06-12 — Teste adversarial e slop de registro

### Metodologia

Segunda rodada empírica, desenhada para encontrar o que a v1 **não** detectava:

1. **Corpus v2 adversarial:** 32 textos (~10.500 palavras) em 12 gêneros deliberadamente ausentes do v1 — press release, notícia, resenha, roteiro YouTube, thread X, suporte ao cliente, jurídico, acadêmico, casual/fórum, landing page, newsletter, colecionismo/vinil — sob 5 condições de prompt: seco, briefing detalhado, persona, **"tom humano e natural"**, limite de palavras.
2. **Teste adversarial:** skill v1 aplicada como detector sobre o corpus v2; tudo que escapou foi classificado (frase nova / estrutura nova / padrão de registro / padrão de condição) e medido. Achados completos em [docs/achados-corpus-v2.md](docs/achados-corpus-v2.md).
3. **Atualização:** só entrou na skill o que foi medido no corpus ou derivado conceitualmente de um escape medido (ex.: a regra do contraste passou a cobrir reversão sem negação porque a versão positiva escapou 3/3).

### Taxa de cobertura (sobre o corpus v2)

| | Antes (v1) | Depois (v2) |
|---|---|---|
| Slop detectado / slop identificado | ~90 / ~274 (**~35%**) | ~271 / ~274 (**~95%**) |
| Jurídico | ~15% | coberto (seção dedicada) |
| Acadêmico | ~15% | coberto (seção dedicada) |
| YouTube/thread | ~20% | coberto (liturgia de plataforma + fôrmas de gênero) |
| Suporte | ~25% | coberto (corporativês de desculpa) |

**Ressalvas de leitura:** (a) a medida pós-update é *in-sample* — as regras novas foram extraídas do mesmo corpus em que foram medidas; o teste verdadeiro será o corpus externo (GPT/Gemini), ainda pendente; (b) cobertura ≠ completude: mede recall contra este corpus, não contra todo slop possível; (c) o residual de ~3 hits são instâncias isoladas abaixo do limiar de densidade da skill.

### Mudanças

**SKILL.md**

- Regra 2 reescrita: contraste binário cobre reversão **com ou sem negação** ("é mais do que um X. É Y.")
- Novas regras 11 (registro × público) e 12 (espontaneidade fabricada + slop dentro de aspas)
- Quick checks: 20 → 29

**references/frases.md**

- Nota metodológica: "listas fixas envelhecem; famílias não" ("Em resumo": 16 hits v1, 0 no v2 — migrou para "Resumindo:", "Diante do exposto")
- 8 categorias gerais novas: conclusões rotuladas (família), anúncios de alívio ("A boa notícia?"), conspiração do silêncio, falsa franqueza, falsa intimidade ("aquele/aquela [X]"), hype casual, imperativos de conforto, promessa de simplicidade
- Bloco novo **Slop de registro** (6 dialetos): jurídico, acadêmico, corporativo/press, suporte, engajamento de plataforma, colecionismo/nicho

**references/estruturas.md**

- Linhas novas em tabelas existentes: reversão positiva, pontuação dramática palavra-a-palavra ("Todo. Santo. Dia."), gancho "Mas será que...?"
- 4 seções novas: anáforas triplas, autenticidade fabricada (condição "tom humano"), slop dentro de aspas, fôrmas de gênero

**references/exemplos.md**

- 6 transformações novas (9-14) com trechos reais do corpus v2: jurídico, suporte, press release/aspas, falsa franqueza, liturgia de thread, acadêmico

### Descobertas-chave da rodada

1. **O slop migra com o registro.** A densidade dos padrões v1 caiu nos gêneros novos e um vocabulário inteiro por registro apareceu. Cobertura da v1 fora do seu domínio: 15-25%.
2. **Reviravolta do "outrossim":** o v1 refutou registro empolado como tell — mas não tinha texto jurídico. No registro jurídico, o empolado domina. Tell corrigido: **registro em fôrma × público errado**.
3. **Pedir "tom humano" não remove o slop — troca a pele dele.** Surge a performance de espontaneidade: franqueza anunciada, "kkk" calculado, "EDIT:" fabricado, estrutura de redação intacta sob o verniz. 100% dos textos da condição D exibiram o padrão.
4. **O contraste binário tem forma positiva** que escapa de qualquer busca por negação.
5. **O slop se esconde em discurso direto** (citações executivas fabricadas), onde revisor baixa a guarda.

### Pendências para a v3

- Corpus externo multi-modelo (GPT, Gemini) via prompts prontos no repositório de trabalho (não incluídos aqui) — validação held-out da taxa de ~95% e seção "padrões por modelo"
- Re-teste adversarial sobre o corpus externo

## v1 — 2026-06-11 — Versão inicial

- Skill construída empiricamente a partir de corpus de 24 textos em 8 gêneros (blog, e-commerce, SEO, LinkedIn, tutorial, email, FAQ, institucional). Achados em [docs/achados-corpus-v1.md](docs/achados-corpus-v1.md).
- SKILL.md (10 regras, 20 checks, pontuação 5×10 com corte em 35/50), frases.md (18 categorias), estruturas.md (16 padrões), exemplos.md (8 transformações).
