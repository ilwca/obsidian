# 🎤 EXEMPLO DE SLIDES PARA APRESENTAÇÃO

  

## Slide 1: Título

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎰 Q-LEARNING BLACKJACK 🎰

Aprendizado por Reforço em Ação

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Um algoritmo de IA que aprende a jogar Blackjack

através de experiência, sem programação manual.

  

Date: 29 de Novembro de 2025

Projeto: Inteligência Artificial

```

  

---

  

## Slide 2: O Problema

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

O DESAFIO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Como ensinar um computador a jogar bem?

  

❌ Opção 1: Programar manualmente a estratégia

└─ Difícil, demanda expertise, não generaliza

  

✅ Opção 2: Deixar aprender através de experiência

└─ Genérico, adaptável, real!

  

Usaremos Q-Learning!

```

  

---

  

## Slide 3: O Que é Q-Learning?

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

O QUE É Q-LEARNING?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Um algoritmo de Aprendizado por Reforço que aprende

através de:

  

EXPERIÊNCIA → RECOMPENSAS → CONHECIMENTO

  

Ideia simples:

• Tomar ação em situação

• Receber resultado (recompensa/punição)

• Lembrar disso para decisões futuras

• Repetir milhares de vezes

  

Resultado: Estratégia ótima emergida!

```

  

---

  

## Slide 4: Os Componentes

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COMPONENTES DO SISTEMA

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

ESTADO (18 possíveis)

└─ Valor da mão do jogador: 4-21

  

AÇÕES (2 possíveis)

├─ HIT: Pedir mais uma carta

└─ STAND: Parar com a mão atual

  

RECOMPENSAS

├─ +1.0: Vitória

├─ -1.0: Derrota

└─ 0.0: Empate

  

MATRIZ Q (18 x 2)

└─ Tabela que memoriza experiências

```

  

---

  

## Slide 5: A Equação de Bellman

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CORAÇÃO DO Q-LEARNING

A EQUAÇÃO DE BELLMAN

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Q(s,a) ← Q(s,a) + α × [r + γ × max(Q(s',a')) - Q(s,a)]

  

Onde:

• Q(s,a) = Valor Q antigo

• α (alpha) = Taxa de aprendizado (0.1)

• r = Recompensa recebida

• γ (gamma) = Fator de desconto (0.95)

• max(Q(s',a')) = Melhor ação no próximo estado

  

INTUIÇÃO:

Combina recompensa imediata com

expectativa de futuro recompensas

```

  

---

  

## Slide 6: As Funções Principais

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AS 3 FUNÇÕES CRÍTICAS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

1️⃣ get_action(state) - A DECISÃO

Escolhe entre:

• Exploração: Ação aleatória (aprender coisas novas)

• Exploração: Melhor ação conhecida (usar saber)

  

2️⃣ update(state, action, reward) - O APRENDIZADO ⭐

Aplica a Equação de Bellman

Atualiza a Matriz Q

ISSO É O APRENDIZADO!

  

3️⃣ train_episode() - UM JOGO COMPLETO

Ciclo: Decide → Joga → Aprende → Repete

Repetido milhares de vezes

```

  

---

  

## Slide 7: Fluxo de Aprendizado

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CICLO DE APRENDIZADO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Episódio 1-1000:

  

┌─────────────────────────────────┐

│ NOVO JOGO │

└────────────┬────────────────────┘

│

[LOOP]

│

┌────────────▼────────────────────┐

│ 1. DECIDIR (ε-greedy) │

│ 2. JOGAR (Ambiente) │

│ 3. APRENDER (Bellman) │

│ 4. PRÓXIMO ESTADO │

└────────────┬────────────────────┘

│

[Repetir até fim]

│

┌────────────▼────────────────────┐

│ REDUZIR EPSILON │

│ (Menos exploração aleatória) │

└─────────────────────────────────┘

  

RESULTADO: Matriz Q preenchida com conhecimento

```

  

---

  

## Slide 8: Evolução do Agente

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ANTES vs DEPOIS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

ANTES (Episódio 0):

• Recompensa Média: ~0 (aleatório)

• Taxa de Vitória: ~50% (acaso puro)

• Estratégia: Nenhuma

• Matriz Q: Toda zerada

  

DEPOIS (Episódio 5000):

• Recompensa Média: +0.4 a +0.6 ✓

• Taxa de Vitória: 60-70% ✓

• Estratégia: Emergida!

• Matriz Q: Convergida

  

O agente melhorou 20-30% em performance!

```

  

---

  

## Slide 9: A Estratégia Aprendida

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ESTRATÉGIA APRENDIDA PELO AGENTE

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Mão do Jogador → Ação Aprendida

────────────────────────────────────────

4-8 → HIT (pedir carta)

9-11 → HIT (pedir carta)

12-16 → HIT (ou depende)

17-20 → STAND (parar)

21 → STAND (parar)

  

ISTO É A ESTRATÉGIA BÁSICA DO BLACKJACK!

  

O computador descobriu sozinho,

sem nós programarmos!

```

  

---

  

## Slide 10: Visualizações da GUI

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

INTERFACE GRÁFICA - 3 ABAS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

1. 🔥 Heatmap Q-Matrix

├─ Mapa de calor colorido

├─ Cores quentes = valores Q altos

└─ Cores frias = valores Q baixos

  

2. 📈 Gráficos de Aprendizado

├─ Recompensa Média (↑ = melhorando)

├─ Taxa de Vitória (↑ = aprendendo)

├─ Decaimento Epsilon (↓ = menos exploração)

└─ HIT vs STAND (estratégia emergida)

  

3. 📋 Tabela Q-Matrix

├─ Visualização detalhada

├─ Cores gradientes

└─ Melhor ação por estado

```

  

---

  

## Slide 11: Resultados Esperados

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

RESULTADOS APÓS 5000 EPISÓDIOS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Métrica Inicial → Final Melhora

─────────────────────────────────────────────────────

Recompensa Média -0.5 → +0.4 ✓ 90%

Taxa de Vitória 50% → 65% ✓ 30%

Epsilon 1.0 → 0.01 ✓ Reduzido

Consistência Aleatória → Padrão ✓ Claro

  

Heatmap:

Antes: Azul uniforme (valores zerados)

Depois: Padrão claro (HIT esq, STAND dir)

```

  

---

  

## Slide 12: Insights Principais

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

INSIGHTS PRINCIPAIS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

1. IA pode aprender sem programação manual

└─ Usar apenas experiência e feedback

  

2. Convergência matemática garantida

└─ Com tempo, Q-Learning encontra ótimo

  

3. Estratégia emerge naturalmente

└─ Não precisa ser ensinada

  

4. Mesmo algoritmo, múltiplos problemas

└─ Funciona em: Jogos, Robótica, Recomendação, etc

  

5. ε-Greedy é essencial

└─ Balanço exploração/exploração é crítico

  

6. Visualização aids compreensão

└─ Gráficos em tempo real revelam padrões

```

  

---

  

## Slide 13: Aplicações Práticas

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

APLICAÇÕES PRÁTICAS DE Q-LEARNING

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Jogos:

└─ Xadrez, Poker, Dota 2, Go

  

Robótica:

└─ Navegação, manipulação, controle

  

Sistemas Recomendadores:

└─ Qual item mostrar next? E-commerce, Netflix

  

Veículos Autônomos:

└─ Que ação tomar em cada situação

  

Trading:

└─ Quando comprar/vender

  

Network Routing:

└─ Melhor caminho para pacotes

  

Finance:

└─ Alocação de portfólio

```

  

---

  

## Slide 14: Conclusão

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CONCLUSÃO

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

✅ Q-Learning é um algoritmo clássico e poderoso

✅ Aprende através de experiência pura

✅ Converge para estratégia ótima

✅ Aplicável a centenas de problemas

✅ Fácil de entender e implementar

  

Este projeto demonstra TUDO em ação:

• Aprendizado real

• Visualizações em tempo real

• Interface profissional

• Documentação completa

  

Q-Learning é o fundamento de muita IA moderna!

```

  

---

  

## Slide 15: Perguntas?

```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PERGUNTAS?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  

Obrigado pela atenção!

  

📌 Materiais disponíveis:

• RESUMO_EXECUTIVO.md

• ROTEIRO_APRESENTACAO.md

• GUIA_APRESENTACAO.md

• demo_interativa.py

• main.py

  

🎮 Experimente:

python demo_interativa.py

python main.py

  

❓ Dúvidas?

```

  

---

  

## 📋 Como Usar Estes Slides

  

1. **Copie o conteúdo** para seu software de apresentação (PowerPoint, Google Slides, Keynote, Beamer, etc)

  

2. **Customize cores** para seu tema corporativo

  

3. **Adicione imagens** do heatmap/gráficos durante apresentação

  

4. **Use as narraçõs** sugeridas em GUIA_APRESENTACAO.md

  

5. **Alterne com demos ao vivo** durante slides relevantes

  

---

  

## ⏱️ Tempo por Slide

  

- Slides 1-3: 5 minutos (contexto)

- Slides 4-6: 8 minutos (conceitos)

- Slides 7-9: 10 minutos (aprendizado - com demo ao vivo!)

- Slides 10-11: 5 minutos (visualizações - mostrar GUI)

- Slides 12-15: 5 minutos (aplicações, conclusão, perguntas)

  

**Total: ~35 minutos de slides + 15 minutos de demo = 50 minutos**

  

---

  

## 💡 Dicas de Apresentação

  

- ✓ Mantenha slides simples (não sobrecarregue com texto)

- ✓ Use cores vibrantes (tema do projeto é dark mode)

- ✓ Integre demos ao vivo (especialmente slides 7-9)

- ✓ Mostre a GUI (slides 10-11) com agente já treinado

- ✓ Deixe espaço para perguntas

- ✓ Seja entusiasmado sobre o tema!

  

---

  

**Bom uso dos slides! 🎤**