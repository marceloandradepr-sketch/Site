# Achados — Extração de Padrões do Corpus de AI Slop em pt-BR

**Data:** 2026-06-11
**Corpus:** 24 textos (5 blog, 5 e-commerce, 4 SEO, 4 LinkedIn, 3 tutorial, 3 email, 2 FAQ, 1 institucional), ~8.500 palavras, gerados deliberadamente sem regras anti-slop.
**Método:** geração livre → contagem mecânica (grep, case-insensitive) → leitura estrutural. Frequência reportada como `ocorrências / arquivos atingidos` sobre 24 arquivos.

---

## 1. Frases e expressões recorrentes (frequência no corpus)

### 1.1 Editorializing — a família "ressaltar" (21 hits / 16 arquivos — o padrão nº 1 do pt-BR)

"É importante ressaltar", "vale ressaltar", "vale destacar", "é importante destacar", "vale lembrar", "é fundamental". Presente em 2/3 do corpus, em todos os tipos de texto.

> "É importante ressaltar que o marketing digital não é apenas uma tendência passageira." (blog-01)
> "Vale ressaltar que o código pode levar até 48 horas para ser atualizado." (faq-01)

Equivalente direto do "it's important to note" inglês, mas com produtividade morfológica maior: o pt-BR flexiona o padrão em dezenas de variantes (ressaltar/destacar/frisar/salientar/lembrar/mencionar × é importante/vale/cabe/cumpre/é válido).

### 1.2 Conectivos em cadeia (33 hits combinados)

- "Além disso": 16 / 14 — quase um por texto.
- "Em primeiro lugar / Em seguida / Por fim": 13 / 6 — esqueleto sequencial exposto.
- "Dessa forma / Nesse sentido / Por conseguinte": 4 / 2.
- "Ademais / Outrossim": 1 / 1 — raro até no slop; registro empolado aparece menos que o esperado. O tell real é "Além disso" em densidade, não "outrossim".

> "Além disso, os custos são significativamente menores... Ademais, é possível mensurar cada resultado... Por conseguinte, os índices de satisfação vem crescendo." (blog-01/02)

### 1.3 Molduras temporais de abertura (10 / 9)

"No mundo atual", "Nos dias de hoje", "No cenário atual", "Em um mundo cada vez mais [X]", "Em meio à correria do dia a dia". **9 dos 24 textos abrem ou contextualizam assim.** Equivalente nativo do "In today's world".

> "No mundo atual, cada vez mais conectado e dinâmico, o marketing digital deixou de ser um diferencial e se tornou uma necessidade." (blog-01 — frase de abertura)

### 1.4 "Cada vez mais" (8 / 6)

Intensificador vazio onipresente, frequentemente dentro da própria moldura temporal ("em um mercado cada vez mais competitivo").

### 1.5 "Conta com" (12 / 7 — slop de produto)

Verbo universal de descrição comercial. ecommerce-05 (imóvel) sozinho tem 6 ocorrências.

> "o apartamento conta com 3 quartos... a cozinha conta com bancada... a varanda gourmet conta com churrasqueira... o condomínio conta com piscina..." (ecommerce-05)

### 1.6 Falsa causalidade dramática: "não é à toa / não é por acaso / não é para menos" (9 / 9)

Um por arquivo em 9 arquivos — distribuição perfeitamente regular, assinatura de máquina.

> "Não é à toa que as empresas que investem em marketing digital vem ganhando destaque." (blog-01)

### 1.7 Contraste binário "Não se trata de X. Trata-se de Y." (13 / 7)

Versão nativa do "It's not X. It's Y.". Aparece também como "não é apenas X, é Y" e "deixou de ser X e se tornou Y" (10 / 8).

> "Não se trata apenas de vender mais. Trata-se de construir relacionamentos duradouros." (blog-01)
> "O home office não é apenas uma mudança de local de trabalho. É uma mudança completa de mentalidade." (blog-02)
> "deixou de ser um diferencial e se tornou uma necessidade" / "deixou de ser opcional" / "deixou de ser uma opção e se tornou uma necessidade" — 3 textos diferentes, fórmula idêntica.

### 1.8 Conclusões rotuladas: "Em resumo / Em suma / Em conclusão" (11 / 11)

11 textos fecham com parágrafo iniciado por marcador de resumo, quase sempre sob heading "## Conclusão" (8 headings no corpus).

### 1.9 Hipérbole de impacto: "faz toda a diferença" (8 / 7)

> "A consistência visual... faz toda a diferença." / "O vapor faz toda a diferença no resultado final." / "pequenos gastos invisíveis... fazem toda a diferença."

### 1.10 Verbos de benefício vago (corpus inteiro)

- "proporcionar/proporcionando": 12 / 7 — "proporcionando liberdade total", "proporciona retorno de energia"
- "garantir/garantindo": 19 / 9 — "garantindo uma imersão completa", "garante ventilação constante"
- "otimizar/impulsionar/potencializar/agregar": 14 / 9 — "otimizando o seu tempo", "agregando elegância e sofisticação"
- "facilitar/facilitando": 9 / 8 — "facilitando o seu dia a dia"

Quase sempre em **cláusula de gerúndio pós-vírgula** (ver §2.6).

### 1.11 Gerundismo (4 / 3 — concentrado em email marketing)

> "Estaremos oferecendo descontos de até 70%..." / "estaremos aplicando um desconto exclusivo..." / "Estaremos liberando ofertas relâmpago..." / "Estaremos disponibilizando também condições especiais..." (email-01/02/03)

Baixa frequência global mas 100% de presença no gênero email — tell de gênero, não de corpus.

### 1.12 "Através de" (5 / 4)

Muleta instrumental no lugar de "por", "com", "via": "através das redes sociais", "através de conteúdos relevantes", "através da qualidade do nosso produto".

### 1.13 Inflação de significância

- "verdadeiro/verdadeira [X]": 5 / 5 — "uma verdadeira revolução", "um verdadeiro tesouro natural", "um verdadeiro desafio"
- "divisor de águas": 2 / 2
- "desempenha um papel fundamental": 6 / 3
- "veio para ficar / caminho sem volta": 3 / 2
- "próximo nível / outro patamar": 7 / 4 — "eleve sua experiência sonora ao próximo nível"

### 1.14 Tom promocional-turístico (11 / 5)

"deslumbrante", "de tirar o fôlego" (2× no mesmo texto), "inesquecível", "imperdível", "encanta", "impressionante". Concentrado em blog-05 (turismo) e e-commerce — equivalente do "breathtaking/stunning/nestled".

> "paisagens deslumbrantes, cachoeiras cristalinas e uma energia única" / "vistas de tirar o fôlego" / "céus estrelados de tirar o fôlego" (blog-05)

### 1.15 Atribuição evasiva (8 / 4 + 4 / 4 de falsa agência)

"Estudos mostram", "Pesquisas indicam", "Especialistas apontam", "A ciência comprova" — zero fontes nomeadas no corpus inteiro.

> "Estudos apontam que transtornos mentais estão entre as principais causas de afastamento." (blog-04)

### 1.16 Tendência vaga em gerúndio: "vem + -ndo" (8 / 8)

"vem ganhando destaque", "vem crescendo de forma alarmante", "vem se valorizando", "vem conquistando adeptos". Movimento sem agente nem dado.

### 1.17 Léxico comercial inflado (alta densidade)

| Termo | Hits / arquivos | Exemplo |
|---|---|---|
| "transformar/transformação/transformadora" | 21 / 13 | "experiência transformadora", "jornada de transformação digital" |
| "completo/completa" | 16 / 12 | "guia completo", "plataforma completa", "imersão completa" |
| "ideal para / perfeito para" | 13 / 8 | "o parceiro perfeito para seus treinos" |
| "oportunidade" | 12 / 6 | "oportunidades como essa só aparecem uma vez por ano" |
| "experiência" | 9 / 5 | "experiência sonora", "experiência única" |
| "jornada" | 8 / 7 | "sua jornada como barista", "jornada digital" |
| "exclusivo" | 8 / 6 | "cupom exclusivo", "comunidade exclusiva" |
| "dia a dia" | 9 / 8 | "facilitando o seu dia a dia" |

"Jornada" para qualquer atividade ("jornada como barista") é tradutês de "journey".

### 1.18 CTAs e fechos de engajamento (12 / 9)

"Gostou? Compartilhe!", "Deixe sua opinião nos comentários!", "Conta aqui nos comentários 👇", "Continue acompanhando nosso blog". Mais os fechos motivacionais: "Pense nisso.", "Sua mente agradece!", "O seu eu do futuro agradece!", "Seus pés agradecem" — a fórmula "[coisa] agradece" apareceu 3× espontaneamente.

### 1.19 Urgência fabricada (email/e-commerce)

"Corra!", "Não perca!", "Não deixe para depois", "estoque limitado", "as vagas são limitadas", "aproveite enquanto dá tempo" — 8+ hits / 6 arquivos, com "P.S." de escassez em 3 de 3 emails.

---

## 2. Padrões estruturais recorrentes

### 2.1 Contraste binário (§1.7) — universal, idêntico ao inglês

Quatro realizações em pt-BR: "Não se trata de X. Trata-se de Y." / "Não é (apenas) X. É Y." / "deixou de ser X e se tornou Y" / "X não é tudo. Y é tudo." (linkedin-01).

### 2.2 Lista negativa

> "Ele batia todas as metas. Entregava antes do prazo. Tecnicamente, era impecável. Mas tinha um problema." (linkedin-01)
> "Você não precisa saber programar. Não precisa de diploma em tecnologia. Precisa apenas de curiosidade." (linkedin-02)

### 2.3 Fragmentação dramática (assinatura do LinkedIn pt-BR)

Parágrafos de uma linha, frases de 1-3 palavras empilhadas:

> "Mas tinha um problema. / Ele destruía a equipe ao redor dele." (linkedin-01)
> "Ignoram. Resistem. Torcem para que passe." / "Aprendem. Testam. Integram na rotina." (linkedin-02 — tríades espelhadas)
> "Simples assim? Sim. Fácil? Não." (linkedin-02)

### 2.4 Pergunta retórica como setup (58 linhas com "?" no corpus)

Três usos: abertura ("Você já parou para pensar...?" — 3 / 3), heading-pergunta ("Por que investir em marketing digital?"), e pergunta-autorespondida comercial ("O melhor de tudo? Ele acompanha um estojo..." — 3 / 3). LinkedIn fecha com pergunta de engajamento em 4 de 4 posts.

### 2.5 Falsa agência

> "Os dados nos mostram o caminho a seguir e revelam oportunidades escondidas." (blog-01)
> "O mercado exige cada vez mais autenticidade." (blog-01) / "O mercado de trabalho recompensa quem entende as novas demandas." (blog-02)
> "A cultura organizacional sofre... A comunicação se torna mais desafiadora. O sentimento de pertencimento se enfraquece." (blog-02 — três falsas agências em sequência)

### 2.6 Cláusula de gerúndio pós-vírgula (equivalente pt-BR do ", ensuring convenience")

O padrão estrutural mais denso do corpus de e-commerce: vírgula + gerúndio de benefício vago fechando a frase.

> "...até 40 horas de reprodução, **proporcionando liberdade total** para o seu dia a dia."
> "...conexão rápida e sem falhas, **elevando sua experiência a outro patamar**."
> "...8 programas pré-definidos, **otimizando o seu tempo na cozinha**."
> "...controles touch intuitivos, **facilitando o seu dia a dia**."

Praticamente todo bullet de produto do corpus termina assim. Interpretação vazia colada ao fato.

### 2.7 Bullet com bold lead-in + dois pontos (50 ocorrências)

`- **Rótulo:** frase que reformula o rótulo.` Presente em 15+ arquivos, sempre em grupos de 3-5. Formatting tell idêntico ao inglês.

### 2.8 Tríades

Listas e headings em grupos de 3 por toda parte: "três pilares fundamentais", "conforto, estilo e performance", "eduquem, inspirem ou entretenham", "sofisticação, conforto e praticidade". A tríade espelhada do linkedin-02 (§2.3) é o caso extremo.

### 2.9 Esqueleto retórico exposto

"Em primeiro lugar... Em seguida... Por fim..." (13 / 6) + heading "## Conclusão" (8) + parágrafo final "Em resumo/Em suma" (11 / 11). O texto anuncia a própria estrutura — meta-comentário estrutural.

### 2.10 Aberturas imperativas comerciais (7)

"Imagine acordar todos os dias...", "Descubra um novo nível...", "Transforme a sua cozinha...", "Chegou o tênis que...", "Apresentamos o Residencial...". E-commerce abre 5 de 5 assim.

### 2.11 Correlações "seja... seja" / "tanto... quanto" (5)

"seja durante o treino, no trabalho ou relaxando em casa", "tanto para empresas quanto para colaboradores" — embalagem de abrangência universal ("serve para todos").

### 2.12 Voz passiva + particípio de design

"foi pensado para", "desenvolvido com tecnologia de ponta", "cuidadosamente projetado", "cada detalhe foi cuidadosamente pensado" (12 / 7). A passiva esconde quem projetou; "cuidadosamente" intensifica sem informar.

---

## 3. Padrões de ritmo

1. **Parágrafo de 2-3 frases uniformes**: blogs e SEO mantêm parágrafos de comprimento quase idêntico do início ao fim — nenhum parágrafo longo, nenhuma frase de 30+ palavras seguida de uma curta.
2. **Fim de seção punchy**: praticamente toda seção fecha com sentença curta de efeito ("A primeira impressão é a que fica.", "Os resultados falam por si.", "O risco é todo nosso.").
3. **Pergunta-resposta imediata**: nenhuma pergunta fica sem resposta na frase seguinte ("Adivinha quem está saindo na frente?", "Simples assim? Sim.").
4. **LinkedIn metronômico invertido**: só frases curtas — a monotonia é de staccato, não de legato. Linha em branco entre cada frase.
5. **Fecho motivacional universal**: 20 dos 24 textos terminam em exortação ou CTA ("Comece hoje mesmo!", "Vamos escrevê-la juntos?", "Bom apetite!"). Nenhum texto termina num fato.

---

## 4. Padrões específicos do pt-BR (ausentes na skill original em inglês)

| # | Padrão | Evidência no corpus | Observação |
|---|---|---|---|
| 1 | Família "ressaltar" com produtividade morfológica | 21 / 16 | Mais frequente e mais variado que "it's important to note"; precisa de regex de família, não lista fixa |
| 2 | Gerundismo ("estaremos oferecendo") | 4 / 3, 100% dos emails | Tell de gênero comercial; inexiste em inglês |
| 3 | Cláusula de gerúndio pós-vírgula | dezenas, e-commerce | Equivalente estrutural do ", ensuring X", mas com verbos próprios: proporcionando, garantindo, otimizando, agregando, facilitando, elevando |
| 4 | "Conta com" | 12 / 7 | Verbo-cola de descrição de produto; sem equivalente direto no slop EN ("boasts" é primo, não gêmeo) |
| 5 | "Não é à toa que" | 9 / 9 | Falsa causalidade; distribuição 1-por-texto = assinatura mecânica |
| 6 | "Vem + gerúndio" de tendência vaga | 8 / 8 | "vem ganhando destaque" — movimento sem agente nem número |
| 7 | "Através de" instrumental | 5 / 4 | Hipercorreção que IA reproduz |
| 8 | "Cada vez mais" | 8 / 6 | Intensificador vazio; em EN "increasingly" é advérbio flagrado, em pt-BR é locução que escapa de filtro de "-mente" |
| 9 | Moldura "No mundo atual / Nos dias de hoje" | 10 / 9 | Abertura padrão de blog/SEO |
| 10 | "[coisa] agradece" | 3 textos | "Sua mente agradece", "Seus pés agradecem", "O seu eu do futuro agradece" — fecho-fórmula brasileiro |
| 11 | "Veio para ficar" | 3 / 2 | Clichê de tendência |
| 12 | "Deixou de ser X e se tornou Y" | 3 textos, fórmula idêntica | Variante de arco de transformação |
| 13 | Tradutês: "jornada", "no fim das contas/no final do dia", "divisor de águas" | 8+2+2 | Calcos de journey / at the end of the day / game-changer |
| 14 | Pergunta de engajamento + "Deixe nos comentários 👇" | 4 / 4 LinkedIn, 3 blogs | Vocativo de engajamento |
| 15 | Advérbios: "-mente" em densidade + locuções | "completamente", "cuidadosamente", "significativamente", "extremamente" + "de forma [adj]" (14+ hits: "de forma natural e orgânica", "de forma consistente") | **"de forma [adjetivo]" é o advérbio disfarçado do pt-BR** — escapa de regra "-mente" |
| 16 | Eco nominal de "-ção" | "a criação e distribuição de conteúdos relevantes para a atração e conversão" (seo-02) | Cadeia abstrata |
| 17 | Mesóclise/registro empolado | 0 hits | **Hipótese da Fase 1 refutada** — IA atual não escorrega pra mesóclise; o tell de registro é o "Além disso" formal, não "outrossim" |

### Hipóteses refutadas pelo corpus

- **"Ademais/Outrossim" como tell central**: 1 hit. O conectivo-tell real é "Além disso" em densidade.
- **Mesóclise**: zero. Descartar da skill.
- **Queísmo/cosismo**: não emergiu como padrão mensurável.

---

## 5. Síntese para a Fase 4

**Top 10 por frequência (entram no scan mecânico do SKILL.md):**

1. Família "ressaltar/destacar" (21)
2. Léxico de transformação ("transformar", "jornada", "experiência") (38 combinados)
3. Verbos de benefício vago + gerúndio pós-vírgula ("proporcionando", "garantindo", "otimizando") (45+ combinados)
4. "Além disso" + cadeia sequencial (29)
5. "Não se trata de X / não é apenas X" — contraste binário (23)
6. Bullet bold lead-in (50 instâncias)
7. "Conta com" (12)
8. Conclusão rotulada "Em resumo/Em suma" + heading Conclusão (19)
9. Moldura temporal "No mundo atual" + "cada vez mais" (18)
10. "Não é à toa" (9, distribuição mecânica)

**Estruturais (entram em estruturas.md):** contraste binário, fragmentação dramática de LinkedIn, pergunta retórica setup/autorespondida, falsa agência, gerúndio pós-vírgula, gerundismo, tríades, esqueleto exposto, abertura imperativa, passiva de design, "de forma [adj]".

**Ritmo:** parágrafos uniformes, fim punchy, staccato de LinkedIn, fecho motivacional universal.
