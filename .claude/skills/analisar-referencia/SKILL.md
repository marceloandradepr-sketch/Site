---
name: analisar-referencia
description: Analisa um vídeo de referência para o canal de psicanálise do usuário usando o skill watch. Use quando o usuário pedir para analisar, dissecar ou estudar um vídeo de referência, ou passar uma URL de vídeo com esse objetivo.
argument-hint: "[URL do vídeo] [opcional: views, retenção, observações]"
allowed-tools: Bash, Read, Skill
---

# Analisar vídeo de referência

Argumentos recebidos: $ARGUMENTS

## Passos

1. Extraia a URL (ou caminho local) dos argumentos. Se não houver, peça ao usuário.
2. Use o skill `watch` nesse vídeo. Se o skill `watch` não estiver instalado, avise que ele vem do plugin `https://github.com/bradautomates/claude-video` (Claude Code, não funciona em Chat nem Cowork) e pare.
3. Se o usuário informou desempenho (views, retenção, comentários), use isso na análise. Se não informou, diga que a análise descreve a estrutura, mas não prova por que o vídeo performou.
4. Produza a análise abaixo.

## Regras

- Analise como o vídeo funciona, não resuma o conteúdo.
- Baseie cada afirmação em evidência (timestamp, frame ou trecho da fala). O que não puder ser confirmado, escreva "não confirmado". Não invente métricas.
- Escreva em português do Brasil. Nunca use travessões, use pontos ou vírgulas.
- Seja direto e crítico. Se o vídeo for ruim, diga.

## Estrutura da resposta

1. **FICHA**: duração, formato (vertical ou horizontal), tipo (talking head, narração com imagens, animação, entrevista, outro), número aproximado de cortes.
2. **GANCHO (0 a 5 segundos)**: transcreva a primeira frase. Classifique: pergunta, afirmação contraintuitiva, promessa, história, dado, provocação. Diga o que aparece na tela e qual emoção ou curiosidade ele aciona.
3. **ESTRUTURA**: blocos com timestamp (gancho, desenvolvimento, virada, conclusão, CTA) e a função de cada um na retenção.
4. **RITMO E EDIÇÃO**: frequência média de cortes, texto na tela, legendas, trilha, zoom, B-roll. Onde o ritmo acelera ou desacelera e por quê.
5. **LINGUAGEM**: tom, grau de jargão, como conceitos complexos são traduzidos, exemplos do cotidiano, 3 frases representativas do estilo.
6. **CONTEÚDO PSI**: conceito ou autor abordado, profundidade, e se há simplificação que distorce a teoria. Aponte imprecisões conceituais e deixe claro o grau de confiança.
7. **FECHAMENTO E CTA**: como termina, que ação pede, se o final recompensa quem assistiu até o fim.
8. **O QUE FUNCIONA E O QUE FALHA**: três pontos fortes e três fracos, cada um com evidência.
9. **ADAPTAÇÃO PARA O MEU CANAL**: não proponha copiar. Liste 3 princípios reaproveitáveis e 2 elementos a evitar para não perder identidade própria. Termine com uma ideia de vídeo original do usuário usando um desses princípios, com exemplo concreto do tema.

## Comparação entre vídeos

Se o usuário pedir para comparar análises anteriores, aponte apenas padrões que se repetem em 3 ou mais vídeos e diga quais vídeos sustentam cada padrão.
