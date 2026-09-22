# Achados — Corpus de Controle Humano

**Data:** 2026-06-12
**Corpus:** 11 textos humanos em pt-BR, ~23.750 palavras, todos publicados antes de 2022 (pré-ChatGPT) ou em fontes de autoria humana verificável. Coletados como cópia local para análise interna; cada arquivo carrega fonte, URL e data no header. Não republicar.

| Gênero | Textos | Fontes |
|---|---|---|
| Tech/opinião | 4 | Manual do Usuário (Rodrigo Ghedin), 2016-2019 |
| Música/crítica | 2 | Scream & Yell (André Forastieri, Marcelo Costa), ~2002 |
| Crônica/pessoal | 2 | Medium (Kleber Bordinhão 2018, Marcelo Ferlin) |
| Finanças | 1 | Clube dos Poupadores (Leandro Ávila) |
| Gastronomia | 2 | PratoFundo (Vitor Hugo) |

**Nota de coleta:** WebFetch parafraseia (o modelo intermediário reescreve a prosa — inutilizável para análise de estilo). A coleta usou curl + extração local de HTML (`corpus-humano/extrair.py`), preservando o texto original palavra a palavra.

---

## 1. Taxas-base: densidade por 1.000 palavras

| Padrão | Slop v1 | Slop v2 | Humano | Razão v1/humano |
|---|---|---|---|---|
| Família "ressaltar/destacar" | 2,35 | 0,52 | 0,08 | **29×** |
| "Além disso" | 1,88 | 0,17 | 0,08 | **24×** |
| Contraste binário | 2,70 | 0,26 | 0,17 | 16× |
| Gerúndio de benefício | 2,11 | 0,09 | 0,08 | **26×** |
| Moldura temporal | 1,17 | 0,00 | 0,08 | 15× |
| "Não é à toa/por acaso" | 1,06 | 0,09 | **0,00** | ∞ |
| "Vem + gerúndio" de tendência | 0,94 | 0,26 | **0,00** | ∞ |
| Conclusão rotulada | 1,29 | 0,34 | **0,00** | ∞ |
| "Faz toda a diferença" | 0,94 | 0,09 | **0,00** | ∞ |
| "Verdadeiro [X]" | 0,47 | 0,17 | **0,00** | ∞ |
| "Conta com" | 1,41 | 0,43 | 0,13 | 11× |
| "De forma [adj]" | 1,41 | 0,52 | 0,21 | 7× |
| "Cada vez mais" | 0,94 | 0,17 | 0,17 | 6× |
| "Através de" | 0,59 | 0,09 | 0,25 | 2× |
| "Jornada"/"no fim das contas" | 1,17 | 0,43 | 0,04 | 29× |
| "Transform*" | 2,47 | 0,69 | 0,25 | 10× |
| CTA de engajamento | 0,94 | 1,12 | 0,17 | 6× |
| Atribuição evasiva | 1,06 | 0,60 | 0,04 | 25× |
| "A boa notícia"/"spoiler" | 0,47 | 0,34 | 0,04 | 11× |

### Leitura

**Discriminadores quase perfeitos (humano = 0,00):** "não é à toa", "vem + gerúndio" de tendência, conclusão rotulada, "faz toda a diferença", "verdadeiro [X]". Em ~24 mil palavras de texto humano variado, nenhuma ocorrência. Qualquer aparição já merece olhar; duas no mesmo texto são evidência forte.

**Padrões que humano também usa (calibrar por densidade, nunca por instância):** "através de" (0,25/1000 — Leandro Ávila usa naturalmente em registro didático), "de forma [adj]" (0,21), "cada vez mais" (0,17), contraste binário (0,17 — humano faz contraste retórico de vez em quando, e faz bem). **Instância isolada desses padrões é escrita normal.** O tell começa em ~3-4× a taxa humana.

**Confirmação da regra central da skill:** "densidade é o tell, não a instância" deixou de ser intuição e virou número. Limiar prático derivado: padrão com taxa humana > 0 → flagrar a partir de ~0,6-0,8/1000 (3-4× a base); padrão com taxa humana 0 → flagrar a partir da 2ª ocorrência.

**Slop espontâneo (v2) se aproxima do humano nas frases** — 0,17-0,69 contra 0,08-0,25 — o que confirma o achado do teste adversarial: em texto de IA não-encomendado, os tells frasais enfraquecem e o peso da detecção recai sobre **estrutura, registro e fôrma**.

---

## 2. Métricas estruturais: humano escreve mais longo e mais irregular

| Métrica | Slop v1 | Slop v2 | Humano |
|---|---|---|---|
| Tamanho médio de parágrafo (palavras) | 26,1 | 29,1 | **54,1** |
| Variabilidade de parágrafo (CV) | 0,61 | 0,60 | **0,69** |
| Tamanho médio de frase (palavras) | 12,0 | 13,9 | **19,5** |
| Variabilidade de frase (CV) | 0,49 | 0,61 | 0,62 |

O parágrafo humano tem o **dobro** do tamanho do parágrafo de IA e varia mais. A frase humana é ~50% mais longa. O "parágrafo curto e escaneável" que a IA produz por padrão — 2-3 frases, uma ideia, ponto — é em si um tell estrutural. Humano deixa a frase correr, subordina, encaixa parêntese, e o parágrafo acompanha o fôlego do argumento, não um template de legibilidade.

(Enviesamento reconhecido: blogs humanos de opinião favorecem parágrafo longo; um corpus humano de e-commerce equilibraria. Mas a direção do sinal é clara e consistente entre gêneros.)

## 3. Anti-tells: o que o humano faz que a IA não faz

Da leitura dos 11 textos — marcas de humanidade praticamente ausentes nos 56 textos de slop:

1. **Limite arbitrário com personalidade.** "Todo mundo tem um disco que mudou a sua vida. Ou dois, ou três. **Mais que cinco não vale.**" (Forastieri). A regra inventada na hora, sem justificativa, é assinatura humana — IA justificaria.
2. **Digressão que não volta.** Ghedin abre parêntese sobre Palmer Luckey e política, não amarra com o argumento, segue em frente. IA fecha todo loop que abre.
3. **Opinião sem hedge nem evidência.** "equipamentos simplórios podem ter retardado a consolidação da VR" — palpite assumido como palpite, sem "estudos mostram".
4. **Referência datada e específica.** Preço em real com data, nome de loja, esquina, edição. O slop genérico flutua fora do tempo ("nos dias de hoje"); o humano crava "R$ 19,90 por 15 minutos durante a semana, no Pátio Batel".
5. **Primeira pessoa com custo.** "Em 2016, escrevi argumentando [que viria enxurrada de conteúdo]" — o autor cita o próprio erro. IA não tem histórico para se contradizer.
6. **Frase torta que funciona.** Anacoluto, aposto empilhado, ritmo de fala. O humano erra a gramática a favor do ritmo; a IA acerta a gramática contra ele.
7. **Final sem cerimônia.** Vários textos humanos simplesmente param depois do último ponto de conteúdo. Sem recap, sem moral, sem CTA. O texto acaba porque o assunto acabou.

## 4. Implicações aplicadas à skill

1. Limiar numérico de densidade nas regras (3-4× a taxa humana; 2ª ocorrência para padrões de base zero).
2. Discriminadores quase perfeitos promovidos a "flagrar sempre".
3. Parágrafo curto uniforme adicionado como tell estrutural com número (26-29 vs 54 palavras).
4. Anti-tells documentados como direção de reescrita (não como checklist — humanidade não se fabrica por regra; ver "autenticidade fabricada").

## 5. Limitações

- 11 textos, 5 fontes, viés de gênero (opinião/crônica pesam mais que comercial). Texto humano comercial (e-commerce, email marketing real) ficou de fora — as taxas-base de gêneros comerciais humanos podem ser maiores.
- Fontes são autores experientes; texto humano amador fica entre o slop e este corpus.
- Coleta de 2026: páginas podem ter sido editadas desde a publicação original (risco baixo em arquivo estático).
