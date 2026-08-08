# Controle Proporcional-Derivativo


## Índice

1. [Controle proporcional (P)](#1-controle-proporcional-p)
2. [Controle proporcional-derivativo (PD)](#2-controle-proporcional-derivativo-pd)
3. [Panorama comparativo](#3-panorama-comparativo)
4. [Exemplo — sistema massa-mola-amortecedor com controle PD](#4-exemplo--sistema-massa-mola-amortecedor-com-controle-pd)
5. [Síntese geral](#5-síntese-geral)

---

## 1. Controle proporcional (P)

### 1.1 Formulação

Considere a equação diferencial linear de segunda ordem não homogênea na forma padrão:

$$\ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + \omega_n^2x(t) = \omega_n^2u(t) \tag{1}$$

na qual $\omega_n$ é a frequência natural não amortecida e $\xi$ é o fator de amortecimento.

A ação de controle proporcional é definida como:

$$u(t) = k_pe(t)$$

na qual $k_p$ é o **ganho proporcional** e, para o sinal de referência a ser rastreado $r(t)$, o erro é dado por:

$$e(t) = r(t) - x(t)$$

Logo:

$$u(t) = k_pe(t) = k_pr(t) - k_px(t) \tag{2}$$

### 1.2 Efeito sobre a equação diferencial

Substituindo (2) em (1):

$$\ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + \omega_n^2x(t) = \omega_n^2(k_pr(t)-k_px(t))$$

$$\Rightarrow \ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + \omega_n^2x(t) + \omega_n^2k_px(t) = \omega_n^2k_pr(t)$$

$$\Rightarrow \ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + (\omega_n^2+\omega_n^2k_p)x(t) = \omega_n^2k_pr(t)$$

> **Observação central:** o controle proporcional **não altera** o coeficiente de $\dot{x}(t)$ (o termo de amortecimento $2\xi\omega_n$), mas **altera** o coeficiente de $x(t)$ — de $\omega_n^2$ para $\omega_n^2(1+k_p)$. É uma mudança na "rigidez efetiva" do sistema.

### 1.3 Erro de regime permanente (entrada degrau)

Considere que o sinal de referência $r(t)$ seja a função degrau:

$$r(t) = \begin{cases}E & t\geq0\\0 & t<0\end{cases}$$

resultando na solução particular $x_p(\infty)=K$. Assim:

$$\ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + (\omega_n^2+\omega_n^2k_p)x(t) = \omega_n^2k_pE \tag{3}$$

Em regime permanente, $\ddot{x}(\infty)=\dot{x}(\infty)=0$:

$$(\omega_n^2+\omega_n^2k_p)K = \omega_n^2k_pE \Rightarrow K = \frac{\omega_n^2k_pE}{\omega_n^2(1+k_p)} \Rightarrow \boxed{K = \frac{k_pE}{1+k_p}}$$

> Se o ganho proporcional $k_p$ for suficientemente alto ($k_p\gg1$), o erro de regime permanente será aproximadamente nulo, ou seja, $K\approx E$ — mas **nunca exatamente nulo** para $k_p$ finito.

### 1.4 Efeito sobre a estabilidade — equação característica

A equação característica de (3) é:

$$\alpha^2 + 2\xi\omega_n\alpha + (\omega_n^2+\omega_n^2k_p) = 0$$

cujas raízes são:

$$\alpha = \frac{-2\xi\omega_n\pm\sqrt{4\xi^2\omega_n^2-4(\omega_n^2+\omega_n^2k_p)}}{2} = \frac{-2\xi\omega_n\pm\sqrt{4\omega_n^2(\xi^2-1-k_p)}}{2}$$

$$\Rightarrow \alpha = -\xi\omega_n\pm\omega_n\sqrt{\xi^2-1-k_p} \Rightarrow \boxed{\alpha = -\xi\omega_n\pm j\omega_n\sqrt{1-\xi^2+k_p}}$$

> **Valores altos do ganho proporcional $k_p$ tornam o sistema controlado muito oscilatório**, pois a raiz quadrada fica mais negativa (o argumento sob a raiz cresce), aumentando a parte imaginária das raízes da equação característica. **A parte real, $-\xi\omega_n$, não muda com $k_p$** — o controle proporcional não altera o amortecimento absoluto do sistema.

> **Trade-off central do controle P puro:** reduzir o erro de regime permanente exige $k_p$ grande, mas isso torna o sistema mais oscilatório (maior overshoot), sem melhorar o tempo de acomodação (que depende só da parte real, inalterada).

---

## 2. Controle proporcional-derivativo (PD)

### 2.1 Formulação

A ação de controle de um controlador proporcional-derivativo é definida como:

$$u(t) = k_pe(t) + k_d\dot{e}(t)$$

na qual $k_p$ é o ganho proporcional e $k_d$ é o **ganho derivativo**.

Com $e(t)=r(t)-x(t)$:

$$u(t) = k_pe(t)+k_d\dot{e}(t) = k_pr(t)-k_px(t)+k_d\dot{r}(t)-k_d\dot{x}(t) \tag{4}$$

### 2.2 Efeito sobre a equação diferencial

Substituindo (4) em (1):

$$\ddot{x}(t)+2\xi\omega_n\dot{x}(t)+\omega_n^2x(t) = \omega_n^2(k_pr(t)-k_px(t)+k_d\dot{r}(t)-k_d\dot{x}(t))$$

$$\Rightarrow \ddot{x}(t)+2\xi\omega_n\dot{x}(t)+\omega_n^2x(t)+\omega_n^2k_px(t)+\omega_n^2k_d\dot{x}(t) = \omega_n^2k_pr(t)+\omega_n^2k_d\dot{r}(t)$$

$$\Rightarrow \boxed{\ddot{x}(t) + (2\xi\omega_n+\omega_n^2k_d)\dot{x}(t) + (\omega_n^2+\omega_n^2k_p)x(t) = \omega_n^2k_pr(t)+\omega_n^2k_d\dot{r}(t)}$$

> **Diferença crucial em relação ao controle P:** agora o coeficiente de $\dot{x}(t)$ **também muda** — de $2\xi\omega_n$ para $2\xi\omega_n+\omega_n^2k_d$. O termo derivativo atua diretamente sobre o amortecimento do sistema, algo que o proporcional sozinho não conseguia fazer.

### 2.3 Erro de regime permanente (entrada degrau)

Considere $r(t)=E$ (degrau), resultando em $x_p(\infty)=K$ e $\dot{r}(t)=0$:

$$\ddot{x}(t)+(2\xi\omega_n+\omega_n^2k_d)\dot{x}(t)+(\omega_n^2+\omega_n^2k_p)x(t) = \omega_n^2k_pE \tag{5}$$

Em regime permanente, $\ddot{x}_p(\infty)=\dot{x}_p(\infty)=0$:

$$(\omega_n^2+\omega_n^2k_p)K = \omega_n^2k_pE \Rightarrow \boxed{K = \frac{k_pE}{1+k_p}}$$

> **Resultado importante:** expressão **idêntica** à do controle proporcional puro! O termo derivativo **não contribui em nada** para o erro de regime permanente — em regime permanente, com entrada constante, $\dot{e}(t)\to0$, e o termo $k_d\dot{e}(t)$ desaparece. No controle proporcional-derivativo, ocorre apenas o efeito da ação de controle proporcional em regime permanente.

### 2.4 Efeito sobre a estabilidade — equação característica

A equação característica de (5) é:

$$\alpha^2 + (2\xi\omega_n+\omega_n^2k_d)\alpha + (\omega_n^2+\omega_n^2k_p) = 0$$

cujas raízes são:

$$\alpha = \frac{-(2\xi\omega_n+\omega_n^2k_d)\pm\sqrt{(2\xi\omega_n+\omega_n^2k_d)^2-4(\omega_n^2+\omega_n^2k_p)}}{2}$$

Expandindo e simplificando o discriminante:

$$\alpha = \frac{-(2\xi\omega_n+\omega_n^2k_d)\pm\sqrt{4\omega_n^2(\xi^2+\xi\omega_nk_d-1-k_p)+\omega_n^4k_d^2}}{2}$$

$$\Rightarrow \alpha = \frac{-(2\xi\omega_n+\omega_n^2k_d)}{2} \pm j\frac{\omega_n\sqrt{4(1+k_p-\xi^2-\xi\omega_nk_d)-\omega_n^2k_d^2}}{2}$$

### 2.5 A ideia central do método PD

| | Controle P | Controle PD |
|---|---|---|
| Parte real das raízes | $-\xi\omega_n$ (fixa, não depende de $k_p$) | $-\dfrac{2\xi\omega_n+\omega_n^2k_d}{2}$ (**depende de $k_d$**) |
| Parte imaginária | Cresce só com $k_p$ | Depende de $k_p$ **e** $k_d$ |

> O valor elevado do ganho proporcional $k_p$, necessário para diminuir o erro de regime permanente, pode ser **compensado** com um valor suficientemente elevado do ganho derivativo $k_d$, de maneira que a parte imaginária das raízes da equação característica não seja muito elevada e, consequentemente, o sistema controlado não seja muito oscilatório.

### 2.6 Tempo de acomodação

Relembrando da Aula 2:

$$t_s = \frac{4}{\xi\omega_n}$$

que depende da **parte real** da raiz da equação característica. Como agora essa parte real é $-\dfrac{2\xi\omega_n+\omega_n^2k_d}{2}$ (em vez de $-\xi\omega_n$ fixo):

> **O tempo de acomodação do sistema controlado por PD é determinado pelo valor do ganho derivativo $k_d$.**

---

## 3. Panorama comparativo

| Ganho | O que ajusta | Efeito |
|---|---|---|
| $k_p$ | Erro de regime permanente | $k_p\uparrow$ ⟹ erro $\downarrow$ (nunca zero); também aumenta a "rigidez" ($\omega_n^2\to\omega_n^2(1+k_p)$), tornando o sistema mais oscilatório |
| $k_d$ | Amortecimento / tempo de acomodação | $k_d\uparrow$ ⟹ parte real mais negativa ⟹ decaimento mais rápido, compensando a oscilação introduzida por $k_p$ alto |

> A lógica de projeto do controlador PD: usa-se $k_p$ para "puxar" o sistema para perto da referência, e $k_d$ para "domar" a oscilação que isso introduz — os dois ganhos atuando sobre aspectos praticamente independentes da resposta (regime permanente *vs.* transitório/amortecimento), de forma análoga ao desacoplamento entre $M_p$ (via $\xi$) e $t_s$ (via $\omega_n$) visto na Aula 2.

---

## 4. Exemplo — sistema massa-mola-amortecedor com controle PD

**Enunciado:** sistema mecânico massa-mola-amortecedor (Figura 1), linear e invariante no tempo, com entrada $u(t)$ = força externa aplicada na massa e saída $w(t)$ = deslocamento da massa. Massa $m=3{,}0\,\text{kg}$. Em malha aberta (Aula 3), para $M_p=14{,}7\%$ e $t_s=0{,}5\,\text{s}$, obteve-se $k=712\,\text{N/m}$ e $b=48{,}1\,\text{Ns/m}$. Determinar os ganhos $k_p$ e $k_d$ de forma que $M_p=30\%$ e $t_s=0{,}5\,\text{s}$ para entrada degrau unitário. Repetir o projeto para $M_p=30\%$ e $t_s=1{,}0\,\text{s}$.

*(Fonte da figura original: OGATA, K. Engenharia de Controle Moderno, 4ª ed., Pearson & Prentice Hall, 2005.)*

### 4.1 Modelagem com o controlador PD

Da 2ª lei de Newton (igual à Aula 3):

$$\sum_{i=1}^3\vec{F}_i = m\vec{a} \Rightarrow -kw(t)-b\dot{w}(t)+ku(t) = m\ddot{w}(t)$$

$$\ddot{w}(t) = -\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)+\frac{k}{m}u(t) \tag{6}$$

O erro é $e(t)=r(t)-w(t)$ e o sinal de controle PD:

$$u(t) = k_pe(t)+k_d\dot{e}(t) = k_pr(t)-k_pw(t)+k_d\dot{r}(t)-k_d\dot{w}(t)$$

Como $r(t)$ é degrau, $\dot{r}(t)=0$:

$$u(t) = k_pr(t) - k_pw(t) - k_d\dot{w}(t) \tag{7}$$

Substituindo (7) em (6):

$$\ddot{w}(t) = -\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)+\frac{k}{m}(k_pr(t)-k_pw(t)-k_d\dot{w}(t))$$

$$\Rightarrow \ddot{w}(t) = -\left(\frac{k+kk_p}{m}\right)w(t) - \left(\frac{b+kk_d}{m}\right)\dot{w}(t) + \frac{kk_p}{m}r(t) \tag{9}$$

ou, equivalentemente:

$$\ddot{w}(t) = -\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)+\frac{k}{m}(k_pe(t)-k_d\dot{w}(t))$$

### 4.2 Diagrama de blocos (Figura 2)

O diagrama do sistema mecânico com o controlador PD e entrada de referência em degrau mostra: o erro $e(t)=r(t)-w(t)$ passa por $k_p$; a realimentação de $\dot{w}(t)$ passa por $k_d$; ambos se somam à entrada do sistema mecânico ($k/m$), que já possui suas próprias realimentações internas de $b/m$ e $k/m$ (a dinâmica original em malha aberta) — a representação gráfica exata da equação (9).

### 4.3 Erro de regime permanente

Como $\dot{w}(\infty)=0$, $\ddot{w}(\infty)=0$, $r(\infty)=E$ e $w(\infty)=K$, pela equação (9):

$$0 = -\left(\frac{k+kk_p}{m}\right)K + \frac{kk_p}{m}E \Rightarrow -(k+kk_p)K+kk_pE = 0 \Rightarrow K = \frac{kk_pE}{k+kk_p}$$

$$\Rightarrow \boxed{K = \frac{k_pE}{1+k_p}} \tag{10}$$

> Confirma exatamente a previsão teórica: o erro de regime permanente depende só de $k_p$, igual ao caso do controle P puro.

### 4.4 Isolando $k_p$ e $k_d$ a partir da forma padrão

Comparando a equação (1) com a equação (9):

$$\ddot{w}(t)+2\xi\omega_n\dot{w}(t)+\omega_n^2w(t) = \omega_n^2u(t)$$

$$\ddot{w}(t) = -\omega_n^2w(t)-2\xi\omega_n\dot{w}(t)+\omega_n^2u(t) = -\left(\frac{k+kk_p}{m}\right)w(t)-\left(\frac{b+kk_d}{m}\right)\dot{w}(t)+\frac{kk_p}{m}r(t)$$

de maneira que:

$$\omega_n^2 = \frac{k+kk_p}{m} \Rightarrow \boxed{k_p = \frac{m\omega_n^2-k}{k}} \tag{11}$$

$$2\xi\omega_n = \frac{b+kk_d}{m} \Rightarrow \boxed{k_d = \frac{2m\xi\omega_n-b}{k}} \tag{12}$$

Essas duas fórmulas são o núcleo do método: dado um par $(\xi,\omega_n)$ — obtido a partir de $(M_p,t_s)$ desejados — calculam-se diretamente os ganhos do controlador.

---

### 4.5 Caso A — $M_p=30\%$, $t_s=0{,}5\,\text{s}$

**Passo 1 — de $M_p$ para $\xi$:**

$$\xi = \sqrt{\frac{(\ln(M_p))^2}{(\ln(M_p))^2+\pi^2}} = \sqrt{\frac{(\ln(0{,}30))^2}{(\ln(0{,}30))^2+\pi^2}} = 0{,}358$$

**Passo 2 — de $t_s$ para $\omega_n$:**

$$t_s = \frac{4}{\xi\omega_n} \Rightarrow \omega_n = \frac{4}{t_s\xi} = \frac{4}{0{,}5\times0{,}358} = 22{,}4\,\text{rad/s}$$

**Passo 3 — ganhos:**

$$k_p = \frac{m\omega_n^2-k}{k} = \frac{3{,}0\times22{,}4^2-712}{712} \Rightarrow k_p = 1{,}11$$

$$k_d = \frac{2m\xi\omega_n-b}{k} = \frac{2\times3{,}0\times0{,}358\times22{,}4-48{,}1}{712} \Rightarrow k_d = 0$$

> **O ganho do controlador derivativo é nulo, pois o tempo de acomodação é o mesmo do projeto do sistema em malha aberta.** O sistema em malha aberta (Aula 3) já tinha $t_s=0{,}5\,\text{s}$; como o novo projeto pede o mesmo $t_s$, nenhuma correção de amortecimento é necessária — apenas $M_p$ mudou (de 14,7% para 30%), responsabilidade exclusiva de $k_p$ (via $\omega_n$, que mudou de 15,4 para 22,4 rad/s). O controlador se reduz, na prática, a um controle puramente proporcional.

**Erro de regime permanente:**

$$K = \frac{k_pE}{1+k_p} = \frac{1{,}11\times E}{1+1{,}11} \Rightarrow K = 0{,}526\times E$$

**Figuras 3 e 4** (posição e velocidade da massa, resposta ao degrau unitário, $k_p=1{,}11$, $k_d=0$, $w_0=0$, $\dot{w}_0=0$): a Figura 3 mostra claramente o overshoot ($M_p$, pico $\approx0{,}68\,\text{m}$ em torno de $t\approx0{,}15\,\text{s}$, valor final $\approx0{,}526\,\text{m}$) e o tempo de acomodação $t_s\approx0{,}5\,\text{s}$ marcados sobre a curva — validação visual direta do projeto. A Figura 4 mostra a velocidade oscilando e convergindo a zero, como esperado.

---

### 4.6 Caso B — $M_p=30\%$ (mesmo), $t_s=1{,}0\,\text{s}$ (dobrado)

Mantendo $\xi=0{,}358$ (depende só de $M_p$, que não mudou):

$$\omega_n = \frac{4}{t_s\xi} = \frac{4}{1{,}0\times0{,}358} \Rightarrow \omega_n = 11{,}2\,\text{rad/s}$$

**Ganhos:**

$$k_p = \frac{m\omega_n^2-k}{k} = \frac{3{,}0\times11{,}2^2-712}{712} \Rightarrow k_p = -0{,}472$$

$$k_d = \frac{2m\xi\omega_n-b}{k} = \frac{2\times3{,}0\times0{,}358\times11{,}2-48{,}1}{712} \Rightarrow k_d = -0{,}0338$$

> **Ganhos negativos:** como o novo $t_s$ é maior (resposta mais lenta desejada) e $\omega_n$ menor que o $\omega_n$ original de malha aberta (15,4 rad/s), o controlador precisa efetivamente "amolecer" o sistema (reduzir a rigidez e o amortecimento efetivos) em vez de reforçá-los — daí os ganhos negativos.

**Erro de regime permanente:**

$$K = \frac{k_pE}{1+k_p} = \frac{-0{,}472\times E}{1-0{,}472} \Rightarrow K = -0{,}894\times E$$

**Atenção ao sinal:** o valor de regime permanente $K$ é negativo mesmo com $E$ positivo — a massa se estabiliza numa posição oposta à direção "natural" ingênua, consequência direta de $k_p<0$.

### 4.7 O efeito da condição inicial (Figuras 8 e 10)

Mesma dinâmica ($k_p=-0{,}472$, $k_d=-0{,}0338$), com duas condições iniciais diferentes:

| Figura | $w_0$ | $\dot{w}_0$ | Comportamento |
|---|---|---|---|
| Fig. 8 | $0\,\text{m}$ | $0$ | Parte do repouso na origem, desce até $K\approx-0{,}894\,\text{m}$ |
| Fig. 10 | $0{,}5\,\text{m}$ | $0$ | Parte de $0{,}5\,\text{m}$, converge para o **mesmo** $K\approx-0{,}894\,\text{m}$ |

> **Conexão direta com a Aula 1 (Lyapunov):** demonstração visual da definição de estabilidade assintótica — não importa o ponto de partida $x_0$ (aqui, $w_0$); desde que dentro de uma vizinhança razoável, a trajetória converge para o mesmo ponto de equilíbrio $K$. As Figuras 8 e 10 são, literalmente, duas trajetórias diferentes convergindo ao mesmo $x_e$, exatamente como ilustrado na Figura 1 da Aula 1 ("Assintoticamente estável").

---

## 5. Síntese geral

### 5.1 O que o exemplo demonstra na prática

1. **O método de projeto é sistemático e repetível:** $(M_p,t_s)\to(\xi,\omega_n)\to(k_p,k_d)$ — as mesmas quatro equações (inversão de $M_p$, fórmula de $t_s$, e as equações 11–12) resolvem qualquer especificação.
2. **$k_p$ e $k_d$ podem ser negativos** — não há exigência de sinal positivo; o sinal reflete se o controlador precisa "reforçar" ou "afrouxar" a dinâmica natural do sistema em relação às novas metas.
3. **Quando as especificações coincidem com as do sistema em malha aberta**, o ganho correspondente ($k_d$, no Caso A) simplesmente se anula — o controlador só atua onde há, de fato, uma diferença a corrigir.
4. **A convergência independe da condição inicial** (dentro da faixa testada) — confirmação prática e visual da estabilidade assintótica discutida na Aula 1.

### 5.2 Conexão com as aulas anteriores

- A **forma padrão de 2ª ordem** (Aula 2) é reaproveitada como "molde" para identificar $\xi$ e $\omega_n$ efetivos do sistema controlado.
- As **fórmulas de $M_p$ e $t_s$** (Aula 2) são usadas tanto para análise quanto, agora, para **projeto inverso** dos ganhos do controlador.
- Os **autovalores/raízes da equação característica** (Aulas 1–3) continuam sendo o critério de estabilidade — agora calculados em função dos ganhos de controle.
- O comportamento da trajetória para diferentes condições iniciais reforça diretamente as **definições de estabilidade de Lyapunov** (Aula 1).

---

## Referências

- OGATA, K. *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 4*. Slides de aula, UFABC, 2021.

---

*Material elaborado como notas de estudo, a partir dos slides da disciplina ESTA020-17 (Modelagem e Controle) — UFABC.*