# Achados v2 — Teste Adversarial da Skill zero-lero (ex-stop-slop-ptbr)

**Data:** 2026-06-12
**Corpus v2:** 32 textos Claude (~10.500 palavras), 12 gêneros, 5 condições de prompt (A seco, B briefing, C persona, D "tom humano", E limite de palavras). Textos externos (GPT/Gemini) pendentes para segunda rodada.
**Método:** scan mecânico com os padrões da skill atual (detecção) → scan de candidatos + leitura estrutural (escapes) → classificação e taxa de cobertura.

---

## 1. Taxa de cobertura da skill atual

| Medida | Valor |
|---|---|
| Hits de padrões cobertos pela skill | ~90 |
| Hits de slop que escapou (frases mensuráveis) | ~150 |
| Escapes estruturais (não-greppáveis, por leitura) | ~25 instâncias |
| **Cobertura aproximada** | **~35-40%** |

**Leitura crucial:** a skill cobre bem o slop de *blog/produto/SEO* (domínio do corpus v1), mas o slop **migra com o registro**. Nos gêneros novos, a densidade dos padrões v1 cai (ex.: "em resumo/em suma": 16 hits no v1, **zero** no v2 — substituído por "Resumindo:", "Recapitulando:", "Diante do exposto") e um vocabulário inteiro de slop por registro aparece sem cobertura.

Cobertura estimada por registro:

| Registro | Cobertura | Motivo |
|---|---|---|
| Press release | ~50% | molduras e contrastes cobertos; clichê corporativo não |
| Notícia | ~55% | atribuição evasiva coberta; resto relativamente limpo |
| Resenha | ~45% | benefício vago coberto; fórmulas de veredito não |
| Jurídico | **~15%** | registro empolado inteiro fora da skill |
| Acadêmico | **~15%** | fórmulas acadêmicas inteiras fora |
| YouTube/Thread | **~20%** | liturgia de engajamento fora |
| Suporte | **~25%** | corporativês de desculpas fora (gerundismo coberto) |
| Casual/condição D | **~30%** | falsa franqueza e casual calculado fora |
| Landing | ~40% | urgência coberta; anáforas e conspiração não |

---

## 2. Escapes — Frases novas (não listadas em frases.md)

### 2.1 "A boa notícia" (6/6 — o escape mais distribuído)

"A boa notícia? Não precisa ser assim." / "A boa notícia é que o seu pedido já está em rota" / "Já adianto a boa notícia:". Anúncio de alívio — primo do "O melhor de tudo?" que a skill já lista, mas formulação não coberta. Apareceu em 6 gêneros diferentes.

### 2.2 Contraste positivo "mais do que" (3/3)

> "O Futuro no Bolso é **mais do que** um programa de educação financeira. É um investimento no futuro do país." (press-03)
> "Morar no Residencial Vivere é **muito mais do que** adquirir um imóvel." (v1, também escapou lá)

Mesma mecânica do contraste binário, **sem negação** — escapa da regra atual, que busca "não é/não se trata". Lacuna de regex e de conceito: a regra deve cobrir reversão telegrafada com ou sem "não".

### 2.3 Falsa franqueza (4/4 dos textos de condição D)

"Vou ser sincero:", "Vou abrir o jogo:", "Confesso que", "uma verdade que precisa ser dita", "A verdade é dura, mas". **Assinatura da condição "tom humano e natural"**: quando o prompt pede pra não parecer IA, o modelo *performa* honestidade em vez de tê-la. Presente em 100% dos textos D analisados. O escape mais valioso da rodada.

### 2.4 Conspiração do silêncio (7/5)

"o que ninguém te conta", "ninguém fala disso", "que poucos sabem", "as escolas não querem que você saiba", "o ponto que ninguém tá discutindo", "um segredo que poucos conhecem". Variante dramática da atribuição evasiva: autoridade por exclusividade fabricada.

### 2.5 Anáforas triplas de negação e ruptura (6/4)

- "Sem reserva, sem estudo, sem noção." / "Sem perguntas, sem burocracia." / "Sem rasgos, sem escritas, sem mofo."
- "Chega de travar. Chega de entender a letra... Chega de adiar o seu sonho."

Tríade retórica com palavra-âncora repetida. Estrutura nova: a skill cobre tríades de itens, não anáfora.

### 2.6 Falsa intimidade "aquele/aquela [X]" (6/5)

"aquela angústia de segunda-feira", "aquele toque dourado que faz toda a diferença", "aquela vida que de fora parece resolvida", "aquele amigo que". Pressupõe experiência compartilhada que o texto nunca estabeleceu. Em inglês existe primo ("that feeling when"), mas não está na skill.

### 2.7 Hype casual (6/4)

"muda o jogo", "entrega demais", "muda tudo", "absurdo" (como elogio), "surpreendentemente bem". Inflação de significância em registro informal — a lista atual de inflação é toda formal.

### 2.8 Imperativos de conforto (3/3)

"respira. A gente resolve.", "Confia no processo.", "Calma." Condescendência embalada de empatia.

### 2.9 Revelação com dois-pontos (3/2)

"Resultado: ansiedade e decisão emocional.", "Spoiler: quem ganhou dinheiro foi o assessor.", "Tradução: hora extra não remunerada." Rótulo + dois-pontos + punchline.

### 2.10 "Simples assim" e a família "sem fricção" (5/4)

"Simples assim.", "sem mistério", "sem segredo", "sem pegadinha", "sem letra miúda". Promessa de simplicidade como tique.

### 2.11 Gancho "Mas será que...?" (4/2)

"Mas será que ele entrega tudo isso mesmo?", "Mas será que essa modalidade veio realmente para ficar?" Pergunta-gancho de resenha/blog, prima da retórica já coberta mas formulação não listada.

### 2.12 Variantes de conclusão não listadas

"Resumindo:", "Recapitulando:", "Diante do exposto, conclui-se que", "Veredito". A lista atual ("Em resumo/Em suma/Em conclusão") deu **zero** hits no v2 — as variantes capturaram tudo. Lista precisa virar família.

---

## 3. Escapes — Estruturas novas (não cobertas em estruturas.md)

1. **Pontuação dramática palavra-a-palavra:** "Todo. Santo. Dia." / "Uma coisa de cada vez. Sempre." — fragmentação dentro da frase, não entre frases.
2. **Depoimentos fabricados:** bloco ⭐⭐⭐⭐⭐ + aspas + nome próprio + profissão ("— Camila R., analista de marketing"). Landing pages 3/3.
3. **Artefatos de autenticidade fabricada (condição D):** "EDIT: não esperava tanta resposta", P.S. confessional ("eu leio todas as respostas, de verdade"), "kkk" posicionado, "né?" estratégico. O modelo fabrica os *metadados* da espontaneidade.
4. **Liturgia de fecho de thread:** recapitulação com ✅ + "Salva essa thread 🔖" + "RT pra alcançar mais gente" — fecho em três atos idêntico em todas as threads.
5. **Esqueleto de resenha em fôrma:** título com pergunta → "Vamos direto ao ponto" → seções fixas → "Veredito"/"Vale a pena?" → "Nota: X/10". A fôrma inteira é o tell.
6. **Aspas executivas com slop embutido:** citações de CEO em press release carregando contraste binário e inflação ("Não é apenas um investimento na PagueJá. É um investimento no potencial empreendedor do Nordeste"). O slop se esconde dentro de discurso direto, onde o leitor baixa a guarda.
7. **Contraste binário positivo** ("mais do que X, é Y") — ver 2.2; exige atualização da regra estrutural, não só da lista.

---

## 4. Escapes — Slop de registro (o achado central da v2)

### 4.1 Jurídico (17 hits / 2 textos — cobertura atual ~15%)

"Cumpre esclarecer", "insta salientar", "outrossim", "em que pese", "o referido diploma legal", "nos termos da legislação vigente", "no tocante às", "há que se considerar", "faz-se necessário", "diante do exposto, conclui-se que".

**Reviravolta metodológica:** o v1 refutou "outrossim/registro empolado" como tell — mas o corpus v1 não tinha texto jurídico. No registro jurídico, o empolado É o tell dominante: a IA imita "juridiquês de petição" mesmo quando o público declarado é leigo. O tell não é a palavra; é **registro empolado + público errado**.

### 4.2 Acadêmico (14 hits / 2 textos — cobertura ~15%)

"O presente estudo/trabalho", "a literatura aponta" (atribuição evasiva acadêmica), "busca-se compreender", "espera-se que os achados contribuam", "no contexto da contemporaneidade", "tece as considerações finais", "acerca de" em densidade, anúncio de estrutura ("o artigo está estruturado da seguinte forma").

### 4.3 Corporativo/press release (8 hits / 3 textos)

"reforça seu compromisso", "marca um novo capítulo", "líder em soluções", "consolidando seu papel como agente de transformação", "Estamos extremamente felizes e honrados", "trajetória de crescimento acelerado", boilerplate "Sobre a [empresa]" com "nasceu com a missão de".

### 4.4 Suporte/atendimento (10 hits / 2 textos)

"Lamentamos profundamente", "sinceras desculpas", "compreendemos perfeitamente a sua frustração", "o transtorno causado", "fugiu ao nosso controle", "sua satisfação é a nossa maior prioridade", "tomar as devidas providências", "permanecemos à disposição". Corporativês de desculpa: empatia em fôrma, zero responsabilidade específica.

### 4.5 YouTube/engajamento (26 hits / 10 arquivos — o escape mais volumoso)

"Fala, galera!", "já deixa o like", "se inscreve no canal", "ativa o sininho", "bora lá", "fica até o final porque", "cola comigo", "abre o fio 👇", "salva essa thread". Liturgia de plataforma: a IA reproduz o ritual completo e na ordem canônica, sempre.

### 4.6 Colecionismo/vinil (13 hits / 3 textos)

"presença obrigatória em qualquer coleção que se preze", "joia musical", "questão de completismo", "versão definitiva", "icônica", "lendário", "cobiçada prensagem", "é também um investimento". Slop de nicho: reverência de catálogo.

---

## 5. Padrões por condição de prompt

| Condição | Efeito observado |
|---|---|
| A (seco) | Slop v1 clássico, densidade máxima — confirma v1 |
| B (briefing) | Slop cai ~30%, mas fôrma estrutural permanece (seções iguais, fecho motivacional) |
| C (persona) | **Slop de registro**: persona ativa o dialeto slopado da profissão (jurídico, acadêmico, copywriter) |
| D ("tom humano") | **Falsa franqueza + autenticidade fabricada**: o slop não some, troca de pele — "vou ser sincero", "kkk" calculado, EDIT falso, estrutura perfeita sob verniz casual |
| E (limite) | Menor incidência geral; compressão mata enchimento (amostra pequena: 1 texto) |

**Conclusão da condição D (a mais valiosa):** pedir "tom humano" remove o slop *formal* (molduras, conectivos) mas gera uma camada nova — a performance de espontaneidade. Os tells: confissão anunciada, imperfeição calculada (kkk, né?), metadados fabricados (EDIT, P.S.), e a estrutura intacta por baixo (intro + 3 pontos + moral). Texto humano de verdade é estruturalmente mais bagunçado.

## 6. Padrões por modelo

Pendente: corpus externo (GPT/Gemini) não gerado nesta rodada. Seção reservada para a segunda update. Os 32 textos v2 são todos Claude — padrões aqui podem ser idiossincrasias deste modelo; comparação multi-modelo dirá quais são universais.

---

## 7. Top 10 lacunas por frequência (para a Fase 4)

| # | Lacuna | Hits | Tipo |
|---|---|---|---|
| 1 | Liturgia de engajamento YouTube/thread | 26/10 | registro |
| 2 | Juridiquês empolado ("cumpre esclarecer", "outrossim", "diante do exposto") | 17/3 | registro |
| 3 | Academiquês ("o presente estudo", "a literatura aponta", "faz-se necessário") | 14/2 | registro |
| 4 | Corporativês de desculpa (suporte) | 10/2 | registro |
| 5 | Clichê de press release ("reforça seu compromisso", "novo capítulo") | 8/3 | registro |
| 6 | Conspiração do silêncio ("o que ninguém te conta") | 7/5 | frase |
| 7 | "A boa notícia?" e anúncios de alívio | 6/6 | frase |
| 8 | Falsa intimidade "aquele/aquela [X]" | 6/5 | frase |
| 9 | Anáforas triplas ("sem X, sem Y, sem Z" / "Chega de...") | 6/4 | estrutura |
| 10 | Falsa franqueza ("vou ser sincero") + autenticidade fabricada (EDIT, kkk) | 4/4 + estrutural | condição D |

Menções honrosas que entram na atualização: contraste positivo "mais do que" (conceitual, corrige regra existente), pontuação dramática palavra-a-palavra, depoimentos fabricados, variantes de conclusão ("Resumindo:", "Diante do exposto"), hype casual ("muda o jogo"), imperativos de conforto ("respira"), revelação com dois-pontos ("Spoiler:"), slop de colecionismo, aspas executivas com slop embutido, "Mas será que...?".
