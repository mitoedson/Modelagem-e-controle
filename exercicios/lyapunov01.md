# Estabilidade de Lyapunov - Exercícios


## (1) Sistema linear estável: $\dot{x} = -2x$

**Passo 1: encontrar $x_e$**

$$-2x_e = 0 \Rightarrow x_e = 0$$

**Passo 2: solução analítica**

$$x(t) = x_0 e^{-2t}$$

**Passo 3: dado um $\xi$ qualquer, encontrar $\delta$**

Como $\alpha=-2<0$, $|e^{-2t}| \leq 1$ para todo $t\geq0$ (decaimento monótono). Logo:

$$|x(t)| = |x_0|\,|e^{-2t}| \leq |x_0|$$

Ou seja, a trajetória **nunca ultrapassa** o valor inicial em módulo. Então, para qualquer $\xi$ dado, basta escolher:

$$\delta = \xi$$

**Verificação numérica:** se $\xi = 0{,}5$, escolha $\delta=0{,}5$. Teste $x_0 = 0{,}4$ (dentro de $S(\delta)$):

$$x(t) = 0{,}4e^{-2t}$$

Em $t=0$: $x=0{,}4 \leq 0{,}5$ ✓. Como a função só decresce em módulo, $|x(t)|\leq 0{,}4 \leq \xi$ para todo $t$. **Estável** (e, na verdade, assintoticamente estável, pois $x(t)\to0$).

---

## (2) — Sistema linear instável: $\dot{x} = 2x$

**Solução:** $x(t) = x_0e^{2t}$, $x_e=0$.

**Tentando achar $\delta$ para $\xi=1$:** suponha $x_0 = 0{,}1$ (bem pequeno, dentro de qualquer $\delta$ razoável). Calculando quando $x(t)$ atinge $\xi=1$:

$$0{,}1\,e^{2t} = 1 \Rightarrow e^{2t}=10 \Rightarrow t = \frac{\ln10}{2} \approx 1{,}15\,\text{s}$$

Ou seja, **não importa quão pequeno seja $x_0$** (e portanto $\delta$), a trajetória sempre cresce sem limite e eventualmente ultrapassa qualquer $\xi$ escolhido. Não existe $\delta>0$ que funcione. **Instável** — exatamente como a definição prevê: "por menor que $\delta$ seja, sempre há uma trajetória que escapa de $S(\xi)$".

---

## (3) — Sistema marginalmente estável: $\dot{x} = 0 \cdot x$ (equilíbrio "neutro")

Aqui $\dot{x}=0$ para todo $x$, então **qualquer ponto é de equilíbrio**. Se $x_0$ é a condição inicial, a solução é trivialmente:

$$x(t) = x_0, \quad \forall t$$

Se você fixar $x_e = 0$ (um dos infinitos pontos de equilíbrio) e escolher $\xi$ qualquer, basta $\delta=\xi$: como $x(t)=x_0$ nunca muda, $|x(t)-x_e| = |x_0| \leq \delta = \xi$ sempre. **Estável**, mas claramente **não assintoticamente** (a trajetória não converge a $x_e=0$ a menos que já comece lá).

---

## (4) — Um caso não linear, para mostrar que $\delta$ pode ser *menor* que $\xi$

Considere $\dot{x} = -x + x^3$ (não linear), com $x_e=0$.

Perto da origem, o termo dominante é $-x$ (comportamento localmente estável), mas o termo $x^3$ "atrapalha" se $x$ crescer demais — na verdade, esse sistema tem outros pontos de equilíbrio em $x_e=\pm1$ (onde $-x+x^3=0$), que atuam como "barreiras".

**Intuição sem resolver a EDO completa:** se você escolher $\xi = 0{,}9$ (menor que a distância até os outros equilíbrios, $x=\pm1$), você **não pode** escolher $\delta=\xi=0{,}9$ ingenuamente — precisa escolher um $\delta$ mais conservador (menor), porque perto de $x=0{,}9$ o termo $x^3$ já começa a competir com $-x$, mudando o comportamential. Nesse caso:

$$\delta < \xi$$

Esse é o tipo de sistema em que **$\delta$ e $\xi$ não coincidem** — ao contrário do Exemplo 1, onde a dinâmica linear permitiu $\delta=\xi$ diretamente. Fica evidente aqui por que a análise formal (via função de Lyapunov $V(x)$, que vocês verão a seguir) é necessária: para sistemas não lineares, geralmente **não dá pra "adivinhar"** o $\delta$ olhando só a solução — dado que $x(t)$ raramente tem forma fechada.

---

## Quadro-resumo dos quatro exemplos

| Exemplo | Sistema | $x_e$ | Relação $\delta$–$\xi$ | Classificação |
|---|---|---|---|---|
| 1 | $\dot x=-2x$ | 0 | $\delta=\xi$ (qualquer $\xi$) | Assint. estável |
| 2 | $\dot x=2x$ | 0 | Nenhum $\delta$ funciona | Instável |
| 3 | $\dot x=0$ | 0 | $\delta=\xi$ | Estável (não assint.) |
| 4 | $\dot x=-x+x^3$ | 0 | $\delta<\xi$ (perto de outros equilíbrios) | Assint. estável (localmente) |
