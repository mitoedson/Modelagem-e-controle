# Ressonância

## Índice

1. [Equações diferenciais lineares de segunda ordem homogêneas](#1-equações-diferenciais-lineares-de-segunda-ordem-homogêneas)
2. [Ressonância em um sistema não amortecido](#2-ressonância-em-um-sistema-não-amortecido)
3. [Ressonância em um sistema amortecido](#3-ressonância-em-um-sistema-amortecido)
4. [Exemplo — sistema massa-mola-amortecedor](#4-exemplo--sistema-massa-mola-amortecedor)
5. [Síntese geral](#5-síntese-geral)


## 1. Equações diferenciais lineares de segunda ordem homogêneas

Considere a equação diferencial linear de segunda ordem homogênea na forma padrão, dada por

$$\ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + \omega_n^2x(t) = 0 \qquad (1)$$

com condições iniciais $x(0)=x_0$ e $\dot{x}(0)=\dot{x}_0$ conhecidas, na qual $\omega_n$ é a frequência natural não amortecida e $\xi$ é o fator de amortecimento.

De acordo com os resultados anteriores (Aula 2), o comportamento dinâmico dos sistemas descritos pela equação diferencial (1) é definido pelas raízes da equação característica

$$\alpha^2+2\xi\omega_n\alpha+\omega_n^2=0$$

dadas por

$$\alpha = \frac{-2\xi\omega_n\pm\sqrt{4\xi^2\omega_n^2-4\omega_n^2}}{2} = \frac{-2\xi\omega_n\pm\sqrt{4\omega_n^2(\xi^2-1)}}{2}$$

$$\Rightarrow \alpha = \frac{-2\xi\omega_n\pm2\omega_n\sqrt{\xi^2-1}}{2} \Rightarrow \boxed{\alpha = -\xi\omega_n\pm j\omega_n\sqrt{1-\xi^2}}$$

---

## 2. Ressonância em um sistema não amortecido

### 2.1 Solução homogênea

Como visto anteriormente, quando $\alpha$ é uma raiz complexa conjugada da equação característica, a solução será dada por

$$x(t) = e^{-\xi\omega_nt}[(k_1+k_2)\cos\omega_nt+j(k_1-k_2)\text{sen}\,\omega_nt]$$

de maneira que as constantes $k_1$ e $k_2$ são determinadas a partir das condições iniciais.

Se o sistema for não amortecido, ou seja, $\xi=0$, então a equação (1) é dada por

$$\ddot{x}(t)+\omega_n^2x(t)=0 \qquad (2)$$

e as raízes da equação característica serão dadas por $\alpha=\pm j\omega_n$, ou seja, complexas conjugadas puramente imaginárias.

Assim,

$$x_h(t) = e^{-\xi\omega_nt}[(k_1+k_2)\cos\omega_nt+j(k_1-k_2)\text{sen}\,\omega_nt]$$
$$= e^{-0\times\omega_nt}[(k_1+k_2)\cos\omega_nt+j(k_1-k_2)\text{sen}\,\omega_nt]$$
$$= (k_1+k_2)\cos\omega_nt+j(k_1-k_2)\text{sen}\,\omega_nt$$
$$= c_1\cos\omega_nt+jc_2\text{sen}\,\omega_nt \qquad (3)$$

### 2.2 Solução particular para entrada senoidal

Considere que o sistema não amortecido seja também não homogêneo. Assim, da equação (2), para condições iniciais $x(0)=x_0$ e $\dot{x}(0)=\dot{x}_0$ conhecidas, temos que

$$\ddot{x}(t)+\omega_n^2x(t)=F_0\text{sen}\,\gamma t \qquad (4)$$

na qual $F_0$ é a amplitude e $\gamma$ é a frequência do sinal senoidal de entrada, que é diferente da frequência natural não amortecida do sistema, ou seja, $\gamma\neq\omega_n$.

Uma candidata à solução particular da equação (4) é dada por

$$x_p(t) = A\cos\gamma t+B\text{sen}\,\gamma t$$

cujas derivadas primeira e segunda são dadas, respectivamente, por

$$\dot{x}_p(t) = -A\gamma\text{sen}\,\gamma t+B\gamma\cos\gamma t \qquad \text{e} \qquad \ddot{x}_p(t) = -A\gamma^2\cos\gamma t-B\gamma^2\text{sen}\,\gamma t$$

Assim, da equação (4), temos que

$$\ddot{x}_p(t)+\omega_n^2x_p(t)=F_0\text{sen}\,\gamma t$$
$$\Rightarrow -A\gamma^2\cos\gamma t-B\gamma^2\text{sen}\,\gamma t+\omega_n^2(A\cos\gamma t+B\text{sen}\,\gamma t)=F_0\text{sen}\,\gamma t$$
$$\Rightarrow -A\gamma^2\cos\gamma t-B\gamma^2\text{sen}\,\gamma t+\omega_n^2A\cos\gamma t+\omega_n^2B\text{sen}\,\gamma t=F_0\text{sen}\,\gamma t$$
$$\Rightarrow A(\omega_n^2-\gamma^2)\cos\gamma t+B(\omega_n^2-\gamma^2)\text{sen}\,\gamma t=0\times\cos\gamma t+F_0\text{sen}\,\gamma t$$

Por comparação, $A(\omega_n^2-\gamma^2)\cos\gamma t=0\Rightarrow A=0$, pois $\omega_n^2-\gamma^2\neq0$, já que $\omega_n\neq\gamma\Rightarrow\omega_n^2\neq\gamma^2$, e

$$B(\omega_n^2-\gamma^2)\text{sen}\,\gamma t=F_0\text{sen}\,\gamma t \Rightarrow B(\omega_n^2-\gamma^2)=F_0 \Rightarrow B=\frac{F_0}{\omega_n^2-\gamma^2}$$

Logo, a solução particular da equação (4) é dada por

$$x_p(t) = A\cos\gamma t+B\text{sen}\,\gamma t = \frac{F_0}{\omega_n^2-\gamma^2}\text{sen}\,\gamma t \qquad (5)$$

Das equações (3) e (5), temos que

$$x(t)=x_h(t)+x_p(t)=c_1\cos\omega_nt+c_2\text{sen}\,\omega_nt+\frac{F_0}{\omega_n^2-\gamma^2}\text{sen}\,\gamma t$$

Assim, $x(0)=x_0=0\Rightarrow c_1=0$ e

$$\dot{x}(t)=-c_1\omega_n\text{sen}\,\omega_nt+c_2\omega_n\cos\omega_nt+\frac{\gamma F_0}{\omega_n^2-\gamma^2}\cos\gamma t$$

de maneira que, para $\dot{x}(0)=\dot{x}_0=0$, temos que

$$c_2\omega_n+\frac{\gamma F_0}{\omega_n^2-\gamma^2}=0 \Rightarrow c_2\omega_n=-\frac{\gamma F_0}{\omega_n^2-\gamma^2} \Rightarrow c_2=-\frac{\gamma F_0}{\omega_n(\omega_n^2-\gamma^2)}$$

### 2.3 Solução completa para $\gamma\neq\omega_n$

Portanto, para $\gamma\neq\omega_n$, a solução será

$$x(t) = c_1\cos\omega_nt+c_2\text{sen}\,\omega_nt+\frac{F_0}{\omega_n^2-\gamma^2}\text{sen}\,\gamma t$$
$$= -\frac{\gamma F_0}{\omega_n(\omega_n^2-\gamma^2)}\text{sen}\,\omega_nt+\frac{F_0}{\omega_n^2-\gamma^2}\text{sen}\,\gamma t$$

$$\Rightarrow \boxed{x(t) = \frac{F_0}{\omega_n(\omega_n^2-\gamma^2)}(-\gamma\,\text{sen}\,\omega_nt+\omega_n\text{sen}\,\gamma t)} \qquad (6)$$

> Embora a equação $\ddot{x}(t)+2\xi\omega_n\dot{x}(t)+\omega_n^2x(t)=F_0\text{sen}\,\gamma t$ não esteja definida para $\gamma=\omega_n$, é interessante observar que o seu valor limite quando $\gamma\to\omega_n$ pode ser obtido aplicando a regra de l'Hôpital. O processo limite é análogo à sintonizar a frequência do sinal senoidal de entrada $\gamma$ com a frequência natural não amortecida $\omega_n$.

### 2.4 O caso limite $\gamma=\omega_n$

Para $\gamma=\omega_n$, da equação (6), definimos a solução como

$$x(t) = \lim_{\gamma\to\omega_n}F_0\frac{-\gamma\,\text{sen}\,\omega_nt+\omega_n\text{sen}\,\gamma t}{\omega_n(\omega_n^2-\gamma^2)}$$

$$= \lim_{\gamma\to\omega_n}F_0\frac{\dfrac{d}{d\gamma}(-\gamma\,\text{sen}\,\omega_nt+\omega_n\text{sen}\,\gamma t)}{\dfrac{d}{d\gamma}(\omega_n^3-\omega_n\gamma^2)}$$

$$= \lim_{\gamma\to\omega_n}F_0\frac{-\text{sen}\,\omega_nt+\omega_nt\cos\gamma t}{-2\omega_n\gamma}$$

$$= F_0\frac{-\text{sen}\,\omega_nt+\omega_nt\cos\omega_nt}{-2\omega_n^2} \qquad (\gamma=\omega_n)$$

$$\Rightarrow \boxed{x(t) = \frac{F_0}{2\omega_n^2}\text{sen}\,\omega_nt-\frac{F_0}{2\omega_n}t\cos\omega_nt}$$

Assim, para $\gamma=\omega_n$, quando $t\to\infty$, $x(t)$ cresce indefinidamente e de forma oscilatória (segunda parcela de $x(t)$).

> **Ressonância** é a tendência de um sistema a oscilar em máxima amplitude em certas frequências, chamadas de **frequências ressonantes**. Nessas frequências, até mesmo forças periódicas de pequena amplitude podem fazer com que o sistema oscile em grandes amplitudes, pois faz com que o sistema acumule energia.

---

## 3. Ressonância em um sistema amortecido

### 3.1 Solução geral

Para sistemas lineares e invariantes no tempo de segunda ordem não homogêneos, na forma padrão, dada por

$$\ddot{x}(t)+2\xi\omega_n\dot{x}(t)+\omega_n^2x(t)=F_0\text{sen}\,\gamma t \qquad (7)$$

na qual $\omega_n$ é a frequência natural não amortecida e $\xi$ é o fator de amortecimento. A solução geral é

$$x(t) = \sqrt{c_1^2+c_2^2}\;e^{-\xi\omega_nt}\text{sen}\left(\sqrt{\omega_n^2-\xi^2\omega_n^2}\;t+\phi\right)+\frac{F_0}{\sqrt{(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2}}\text{sen}(\gamma t+\theta) \qquad (8)$$

na qual os ângulos de fase $\phi$ e $\theta$ são dados por

$$\text{sen}\,\phi=\frac{c_1}{\sqrt{c_1^2+c_2^2}} \qquad \cos\phi=\frac{c_2}{\sqrt{c_1^2+c_2^2}}$$

$$\text{sen}\,\theta=\frac{-2\xi\omega_n\gamma}{\sqrt{(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2}} \qquad \cos\theta=\frac{\omega_n^2-\gamma^2}{\sqrt{(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2}}$$

Após um tempo suficientemente grande, a primeira parcela da equação (8) decai exponencialmente (por conta do fator $e^{-\xi\omega_nt}$) e a solução se resume a

$$x(t) = \underbrace{\frac{F_0}{\sqrt{(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2}}}_{g(\gamma)}\text{sen}(\gamma t+\theta) = g(\gamma)\,\text{sen}(\gamma t+\theta) \qquad (9)$$

> Diferentemente do caso não amortecido, aqui a amplitude de regime permanente **não** cresce indefinidamente: ela é dada pela função $g(\gamma)$, que depende da frequência de excitação $\gamma$. O amortecimento $\xi$ garante que a resposta permaneça limitada mesmo quando $\gamma$ se aproxima de $\omega_n$.

### 3.2 Frequência de ressonância

$$g(\gamma) = \frac{F_0}{\sqrt{(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2}} = F_0[(\omega_n^2-\gamma^2)^2+4\xi^2\omega_n^2\gamma^2]^{-1/2} = F_0[\omega_n^4-2\omega_n^2\gamma^2+\gamma^4+4\xi^2\omega_n^2\gamma^2]^{-1/2}$$

Igualando-se a zero a derivada de $g(\gamma)$ em relação a $\gamma$:

$$\frac{dg(\gamma)}{d\gamma} = -\frac{1}{2}F_0[\omega_n^4-2\omega_n^2\gamma^2+\gamma^4+4\xi^2\omega_n^2\gamma^2]^{-3/2}(-4\omega_n^2\gamma+4\gamma^3+8\xi^2\omega_n^2\gamma)=0$$

$$= \frac{1}{2}F_0\frac{4\omega_n^2\gamma-4\gamma^3-8\xi^2\omega_n^2\gamma}{[\omega_n^4-2\omega_n^2\gamma^2+\gamma^4+4\xi^2\omega_n^2\gamma^2]^{3/2}}=0$$

e isolando-se $\gamma$, temos que

$$4\omega_n^2\gamma-4\gamma^3-8\xi^2\omega_n^2\gamma=0 \Rightarrow \gamma(4\omega_n^2-4\gamma^2-8\xi^2\omega_n^2)=0 \Rightarrow 4\omega_n^2-4\gamma^2-8\xi^2\omega_n^2=0$$

$$\Rightarrow \omega_n^2-\gamma^2-2\xi^2\omega_n^2=0 \Rightarrow \gamma^2=\omega_n^2(1-2\xi^2) \Rightarrow \boxed{\gamma_{ress}=\omega_n\sqrt{1-2\xi^2}}$$

Verifica-se que as amplitudes de $x(t)$ são limitadas e que os picos das oscilações ocorrerão na frequência de ressonância dada por

$$f_{ress}=\frac{\gamma_{ress}}{2\pi} \Rightarrow \boxed{f_{ress}=\frac{\omega_n\sqrt{1-2\xi^2}}{2\pi}}$$

> A frequência de ressonância $\gamma_{ress}$ só existe (é um número real) quando $1-2\xi^2>0$, ou seja, quando $\xi<1/\sqrt{2}\approx0{,}707$. Para amortecimentos acima desse valor, não há pico de ressonância: a amplitude $g(\gamma)$ decresce monotonicamente com $\gamma$.

---

## 4. Exemplo — sistema massa-mola-amortecedor

**Enunciado:** considere o sistema mecânico massa-mola-amortecedor, linear e invariante no tempo, cuja entrada $u(t)$ é a força externa aplicada na massa. A saída do sistema $y(t)$ é o deslocamento da massa $w(t)$, medido a partir da posição de equilíbrio. Para a massa $m=3{,}0\,\text{kg}$, a constante elástica da mola $k=712\,\text{N/m}$ e o coeficiente de amortecimento do amortecedor $b=48{,}1\,\text{Ns/m}$, para uma entrada degrau, temos que $M_p=14{,}7\%$ e $t_s=0{,}5\,\text{s}$.

Para o estudo de ressonância, considere uma entrada senoidal $u(t)=F_0\text{sen}\,\gamma t$.

*(Fonte da figura original: OGATA, K. Engenharia de Controle Moderno, 4ª ed., Pearson & Prentice Hall, 2005.)*

### 4.1 De $M_p$ e $t_s$ para $\xi$ e $\omega_n$

$$M_p=e^{-\frac{\xi\pi}{\sqrt{1-\xi^2}}} \Rightarrow \ln(M_p)=-\frac{\xi\pi}{\sqrt{1-\xi^2}} \Rightarrow (\ln(M_p))^2=\left(-\frac{\xi\pi}{\sqrt{1-\xi^2}}\right)^2$$

$$\Rightarrow (\ln(M_p))^2=\frac{\xi^2\pi^2}{1-\xi^2} \Rightarrow (\ln(M_p))^2(1-\xi^2)=\xi^2\pi^2 \Rightarrow (\ln(M_p))^2-(\ln(M_p))^2\xi^2=\xi^2\pi^2$$

$$\Rightarrow (\ln(M_p))^2=\xi^2(\ln(M_p))^2+\xi^2\pi^2 \Rightarrow (\ln(M_p))^2=\xi^2\left((\ln(M_p))^2+\pi^2\right) \Rightarrow \xi^2=\frac{(\ln(M_p))^2}{(\ln(M_p))^2+\pi^2}$$

$$\Rightarrow \xi=\sqrt{\frac{(\ln(M_p))^2}{(\ln(M_p))^2+\pi^2}} = \sqrt{\frac{(\ln(0{,}147))^2}{(\ln(0{,}147))^2+\pi^2}} \Rightarrow \boxed{\xi=0{,}521}$$

$$t_s=\frac{4}{\xi\omega_n} \Rightarrow \omega_n=\frac{4}{t_s\xi} = \frac{4}{0{,}5\times0{,}521} \Rightarrow \boxed{\omega_n=15{,}4\,\text{rad/s}}$$

As Figuras 2 e 3 apresentam o comportamento dinâmico do sistema massa-mola **sem** o amortecedor, ou seja, $b=0$, que resulta em $\xi=0$, respectivamente, sem ressonância e com ressonância. A Figura 4 apresenta o comportamento dinâmico do sistema massa-mola-amortecedor **com** ressonância.

### 4.2 Caso sem amortecimento ($\xi=0$)

> **Figura 2** — posição da massa $m$ do sistema massa-mola **sem** ressonância ($\gamma\neq\omega_n$): resposta oscilatória de amplitude limitada e "batimento" (envelope modulado), característica típica da soma de duas senoides de frequências próximas mas distintas ($\gamma$ e $\omega_n$), conforme a equação (6).
>
> **Figura 3** — posição da massa $m$ do sistema massa-mola **com** ressonância ($\gamma=\omega_n$): a amplitude cresce indefinidamente ao longo do tempo, exatamente como previsto pela equação do caso limite ($x(t)=\frac{F_0}{2\omega_n^2}\text{sen}\,\omega_nt-\frac{F_0}{2\omega_n}t\cos\omega_nt$), na qual o termo $t\cos\omega_nt$ domina para $t$ grande.

### 4.3 Caso com amortecimento ($\xi=0{,}521$)

> **Figura 4** — posição da massa $m$ do sistema massa-mola-amortecedor com ressonância: diferentemente do caso não amortecido, a amplitude **não** cresce indefinidamente — ela se estabiliza em regime permanente numa oscilação senoidal de amplitude constante, exatamente como previsto pela equação (9), $x(t)=g(\gamma)\,\text{sen}(\gamma t+\theta)$.

A frequência angular de ressonância será

$$\gamma_{ress}=\omega_n\sqrt{1-2\xi^2} = 15{,}4\sqrt{1-2\times0{,}521^2} \Rightarrow \gamma_{ress}=10{,}4\,\text{rad/s}$$

A frequência de ressonância será dada por

$$f_{ress}=\frac{\omega_n\sqrt{1-2\xi^2}}{2\pi} = \frac{15{,}4\sqrt{1-2\times0{,}521^2}}{2\pi} \Rightarrow f_{ress}=1{,}66\,\text{Hz}$$

A máxima amplitude de oscilação, na ressonância, será de

$$g_{max}=\frac{F_0}{\sqrt{(\omega_n^2-\gamma_{ress}^2)^2+4\xi^2\omega_n^2\gamma_{ress}^2}} = \frac{100/3}{\sqrt{(15{,}4^2-10{,}4^2)^2+4\times0{,}521^2\times15{,}4^2\times10{,}4^2}} \Rightarrow \boxed{g_{max}=0{,}158\,\text{m}}$$

> **Figura 5** — resposta em frequência $g(\gamma)$ do sistema massa-mola-amortecedor: a curva apresenta um pico bem definido em torno de $\gamma\approx10{,}4\,\text{rad/s}$ (a frequência de ressonância calculada), com $g(\gamma)$ decrescendo suavemente para frequências mais afastadas de $\gamma_{ress}$ — o comportamento típico de um filtro passa-faixa em torno da ressonância.

---

## 5. Síntese geral

### 5.1 Sistema não amortecido ($\xi=0$)

- Para $\gamma\neq\omega_n$: a resposta é a soma de duas senoides de amplitude limitada — comportamento oscilatório com batimento.
- Para $\gamma=\omega_n$ (ressonância exata): a amplitude cresce **indefinidamente** com $t$, de forma oscilatória, pois não há dissipação de energia — o sistema acumula energia continuamente.

### 5.2 Sistema amortecido ($\xi>0$)

- A resposta completa tem uma parcela transitória (que decai exponencialmente, com fator $e^{-\xi\omega_nt}$) e uma parcela de regime permanente, de amplitude $g(\gamma)$.
- A amplitude de regime permanente é **sempre limitada**, mesmo em $\gamma=\gamma_{ress}$, graças à dissipação de energia pelo amortecedor.
- A frequência de ressonância $\gamma_{ress}=\omega_n\sqrt{1-2\xi^2}$ é **menor** que $\omega_n$ e só existe para $\xi<1/\sqrt{2}$.

### 5.3 Conexão com as aulas anteriores

- A **equação característica** e as raízes complexas conjugadas (Aula 2) são o ponto de partida para toda a análise de ressonância.
- Os parâmetros $\xi$ e $\omega_n$ continuam sendo obtidos a partir das especificações de resposta transitória $M_p$ e $t_s$ (Aulas 2 e 3), agora aplicados ao estudo da resposta a uma **entrada senoidal** em vez de degrau.
- O conceito de **resposta em frequência** ($g(\gamma)$, Figura 5) introduzido aqui é a base para tópicos futuros de análise no domínio da frequência (diagramas de Bode, por exemplo).

---

## Referências

- OGATA, K. *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 5*. Slides de aula, UFABC, 2021.
