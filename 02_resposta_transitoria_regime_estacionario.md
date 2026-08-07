# Modelagem e Controle (ESTA020-17) — Aula 2

## Análise de Resposta Transitória e de Regime Estacionário


## Índice

1. [Equações diferenciais lineares de 1ª ordem não homogêneas](#1-equações-diferenciais-lineares-de-1ª-ordem-não-homogêneas)
2. [Equações diferenciais lineares de 2ª ordem não homogêneas](#2-equações-diferenciais-lineares-de-2ª-ordem-não-homogêneas)
3. [Forma padrão de 2ª ordem](#3-forma-padrão-de-2ª-ordem)
4. [Especificações da resposta transitória (entrada degrau)](#4-especificações-da-resposta-transitória-entrada-degrau)
5. [Resposta ao impulso](#5-resposta-ao-impulso)
6. [Síntese geral](#6-síntese-geral)
7. [Referências bibliográficas](#7-referências-bibliográficas)

---

## 1. Equações diferenciais lineares de 1ª ordem não homogêneas

### 1.1 Formulação

Considere a equação diferencial linear de primeira ordem e **não homogênea**:

```math
\frac{dx(t)}{dt} = \alpha x(t) + r(t) \Rightarrow \frac{dx(t)}{dt} - \alpha x(t) = r(t) \qquad(1)
```

na qual $r(t) \neq 0$, $\forall t \geq 0$, com condição inicial $x(0)=x_0$.

### 1.2 Estratégia de solução: homogênea + particular

Define-se $x_p(t)$ como uma solução particular da equação completa, e $x_h(t)$ como a solução da equação **homogênea** (quando $r(t)=0$, já obtida na Aula 1: $x_h(t) = x_h(0)e^{\alpha t}$).

A soma $x(t) = x_h(t) + x_p(t)$ é solução de (1), pois:

$$\frac{dx_h(t)}{dt} - \alpha x_h(t) + \frac{dx_p(t)}{dt} - \alpha x_p(t) = 0 + r(t)$$

Como $x_h$ satisfaz a equação homogênea, o primeiro par de termos é nulo, restando exatamente $r(t)$. Além disso, é sempre possível ajustar $x_h(0)$ para satisfazer qualquer condição inicial completa $x(0) = x_h(0)+x_p(0)$.

> **O problema se resume, portanto, a encontrar $x_p(t)$, que depende da forma de $r(t)$.**

### 1.3 Caso particular: entrada degrau

$$r(t) = \begin{cases} E & t \geq 0 \\ 0 & t < 0 \end{cases}$$

Propõe-se $x_p(t) = K$ (constante). Em regime permanente, $dx_p/dt = 0$:

$$-\alpha K = E \Rightarrow K = -\frac{E}{\alpha}$$

Solução geral:

$$x(t) = x_h(t) + x_p(t) = x_h(0)e^{\alpha t} + K = x_h(0)e^{\alpha t} - \frac{E}{\alpha} \qquad (2)$$

Com $x(0) = x_h(0) - E/\alpha \Rightarrow x_h(0) = x(0) + E/\alpha$.

### 1.4 Constante de tempo $\tau$

Para sistemas **estáveis** ($\alpha < 0$), define-se a **constante de tempo**:

$$\tau = -\frac{1}{\alpha} > 0$$

Ela corresponde ao instante em que a resposta atinge aproximadamente **63,2%** do seu valor de regime permanente. Avaliando (2) em $t=\tau=-1/\alpha$, com $x(0)=0$:

$$x(\tau) = x_h(0)e^{\alpha\tau} - \frac{E}{\alpha} = \left(x(0)+\frac{E}{\alpha}\right)e^{\alpha(-1/\alpha)} - \frac{E}{\alpha} = \frac{E}{\alpha}e^{-1} - \frac{E}{\alpha} = \frac{E}{\alpha}(e^{-1}-1) = -0{,}6321\frac{E}{\alpha}$$

**Exemplo (Figura 1):** $\alpha=-1$, $x_0=0$, $E=2$ → $\tau = 1\,\text{s}$ e $x(\tau) = 1{,}2642$.

**Marcos clássicos de resposta ao degrau, em múltiplos de $\tau$:**

| $t$ | $1\tau$ | $2\tau$ | $3\tau$ | $4\tau$ | $5\tau$ |
|---|---|---|---|---|---|
| % do valor final | 63,2% | 86,5% | 95,0% | 98,2% | 99,3% |

> Regra prática: após ~4 a 5 constantes de tempo, o sistema é considerado praticamente em regime permanente.

---

## 2. Equações diferenciais lineares de 2ª ordem não homogêneas

### 2.1 Formulação

$$\frac{d^2x(t)}{dt^2} + a\frac{dx(t)}{dt} + bx(t) = r(t) \qquad (3)$$

com $r(t)\neq0$, $\forall t\geq0$, e condições iniciais $x(0)=x_0$, $dx(0)/dt = dx_0/dt$.

Pela mesma lógica de superposição, $x(t) = x_h(t)+x_p(t)$ é solução de (3), pois:

$$\frac{d^2x_h(t)}{dt^2}+a\frac{dx_h(t)}{dt}+bx_h(t) + \frac{d^2x_p(t)}{dt^2}+a\frac{dx_p(t)}{dt}+bx_p(t) = 0+r(t)$$

sendo sempre possível encontrar uma solução para (3) para quaisquer condições iniciais $x(0)=x_h(0)+x_p(0)$ e $dx(0)/dt = dx_h(0)/dt + dx_p(0)/dt$.

### 2.2 Entrada degrau, solução particular

Com $r(t)=E$ constante, propõe-se $x_p(t)=K$. Em regime permanente, $d^2x_p/dt^2 = dx_p/dt = 0$:

$$bK = E \Rightarrow K = \frac{E}{b}$$

### 2.3 Ponto-chave: estabilidade é propriedade do sistema, não da entrada

> "O comportamento qualitativo da solução geral $x(t)=x_h(t)+x_p(t)$ varia com as raízes da equação característica, sendo assintoticamente estável apenas quando elas tiverem parte real negativa."

A entrada $r(t)$ (via $K=E/b$) afeta apenas **para onde** o sistema converge — não **se** ele converge. Exemplos:

| Exemplo | Raízes | $K=E/b$ | Estável? |
|---|---|---|---|
| Fig. 2 | $\alpha_1=2,\ \alpha_2=3$ | — | Instável (diverge) |
| Fig. 3 | $\alpha_1=-2,\ \alpha_2=-3$, $E=1$ | $1/6=0{,}1667$ | Assint. estável |
| Fig. 5 | $\alpha_1=-2,\ \alpha_2=-3$, $E=12$ | $12/6=2$ | Assint. estável |
| Fig. 6 | $2\pm j7$ | — | Instável, oscilação crescente |
| Fig. 7 | $-2\pm j7$, $E=159$ | $159/53=3$ | Assint. estável, oscilação amortecida |

---

## 3. Forma padrão de 2ª ordem

Esta é a parametrização **canônica** usada no restante da disciplina:

$$\frac{d^2x(t)}{dt^2} + 2\xi\omega_n\frac{dx(t)}{dt} + \omega_n^2 x(t) = \omega_n^2 r(t) \qquad (4)$$

onde:
- $\omega_n$ = **frequência natural não amortecida**
- $\xi$ = **fator (coeficiente) de amortecimento**

### 3.1 Raízes da equação característica

Para $r(t)=0$, propondo $x(t)=e^{\alpha t}$:

$$\alpha^2 e^{\alpha t} + 2\xi\omega_n\alpha e^{\alpha t} + \omega_n^2 e^{\alpha t} = 0 \Rightarrow \alpha^2 + 2\xi\omega_n\alpha + \omega_n^2 = 0$$

$$\alpha = \frac{-2\xi\omega_n \pm \sqrt{4\xi^2\omega_n^2 - 4\omega_n^2}}{2} = \frac{-2\xi\omega_n \pm \sqrt{4\omega_n^2(\xi^2-1)}}{2}$$

$$\alpha = -\xi\omega_n \pm \omega_n\sqrt{\xi^2-1} \Rightarrow \boxed{\alpha = -\xi\omega_n \pm j\omega_n\sqrt{1-\xi^2}}$$

### 3.2 Os três regimes em função de $\xi$

| $\xi$ | Raízes | Regime | Resposta |
|---|---|---|---|
| $0 < \xi < 1$ | Complexas conjugadas | **Subamortecido** | Oscilatória amortecida |
| $\xi = 1$ | Reais e duplas | **Criticamente amortecido** | Sem oscilação, resposta mais rápida possível sem overshoot |
| $\xi > 1$ | Reais e distintas | **Superamortecido** | Sem oscilação, resposta mais lenta |

### 3.3 Soluções para entrada degrau ($r(t)=E$)

**Subamortecido ($0<\xi<1$):**

$$x(t) = E - Ee^{-\xi\omega_n t}\left(\cos\omega_d t + \frac{\xi}{\sqrt{1-\xi^2}}\text{sen}\,\omega_d t\right) \qquad (5)$$

$$x(t) = E - E\frac{e^{-\xi\omega_n t}}{\sqrt{1-\xi^2}}\,\text{sen}\left(\omega_d t + \text{tg}^{-1}\left(\frac{\sqrt{1-\xi^2}}{\xi}\right)\right), \quad t\geq 0 \qquad (6)$$

na qual $\omega_d = \omega_n\sqrt{1-\xi^2}$ é a **frequência natural amortecida** — a frequência real da oscilação observada (sempre menor que $\omega_n$).

**Criticamente amortecido ($\xi=1$):**

$$x(t) = E - Ee^{-\omega_n t}(1+\omega_n t), \quad t\geq 0 \qquad (7)$$

**Superamortecido ($\xi>1$):**

$$x(t) = E + E\frac{\omega_n}{2\sqrt{\xi^2-1}}\left(\frac{e^{-\alpha_1 t}}{\alpha_1}-\frac{e^{-\alpha_2 t}}{\alpha_2}\right), \quad t\geq 0 \qquad (8)$$

### 3.4 A família de curvas (Figura 8)

Com $\omega_n=5\,\text{rad/s}$ fixo e $\xi$ variando de $0$ a $2$:

- **$\xi=0$**: oscilação **sem amortecimento**, sustentada para sempre — caso "estável, mas não assintoticamente" (análogo ao pêndulo sem atrito da Aula 1)
- **$\xi$ pequeno (0,1–0,3)**: muito overshoot, oscilação demorando a morrer
- **$\xi \approx 0{,}7$**: bom compromisso entre velocidade e overshoot (valor clássico de projeto)
- **$\xi=1$**: sobe o mais rápido possível **sem** ultrapassar o valor final
- **$\xi>1$ (ex.: 2,0)**: sobe mais lentamente, sem oscilar

---

## 4. Especificações da resposta transitória (entrada degrau)

O desempenho do sistema de 2ª ordem na forma padrão pode ser especificado por grandezas no domínio do tempo, a partir da resposta a uma entrada degrau.

### 4.1 Tempo de atraso $t_d$

Tempo necessário para que a resposta transitória alcance **metade** do valor de regime permanente pela primeira vez.

### 4.2 Tempo de subida $t_r$

Tempo necessário para que a resposta passe de $0\%$ a $100\%$ do valor de regime permanente. Resolvendo a equação (6) para $x(t_r)=E$:

$$E = E\left[1 - \frac{e^{-\xi\omega_n t_r}}{\sqrt{1-\xi^2}}\text{sen}\left(\omega_d t_r + \text{tg}^{-1}\left(\frac{\sqrt{1-\xi^2}}{\xi}\right)\right)\right]$$

$$\Rightarrow \text{sen}\left(\omega_d t_r + \text{tg}^{-1}\left(\frac{\sqrt{1-\xi^2}}{\xi}\right)\right) = 0 \Rightarrow \omega_d t_r + \text{tg}^{-1}\left(\frac{\sqrt{1-\xi^2}}{\xi}\right) = \pi$$

$$\boxed{t_r = \frac{\pi - \text{tg}^{-1}\left(\dfrac{\omega_d}{\xi\omega_n}\right)}{\omega_d}}$$

(usando $\text{tg}^{-1}(\sqrt{1-\xi^2}/\xi) = \text{tg}^{-1}(\omega_n\sqrt{1-\xi^2}/(\xi\omega_n)) = \text{tg}^{-1}(\omega_d/(\xi\omega_n))$)

### 4.3 Tempo de pico $t_p$

Tempo necessário para que a resposta alcance o **primeiro pico** de sobressinal. Derivando (5):

$$\frac{dx(t)}{dt} = E\xi\omega_n e^{-\xi\omega_n t}\left(\cos\omega_d t + \frac{\xi}{\sqrt{1-\xi^2}}\text{sen}\,\omega_d t\right) + Ee^{-\xi\omega_n t}\left(\omega_d\,\text{sen}\,\omega_d t - \frac{\xi\omega_d}{\sqrt{1-\xi^2}}\cos\omega_d t\right)$$

Igualando a zero e simplificando (usando $\omega_d = \omega_n\sqrt{1-\xi^2}$), os termos em $\cos\omega_d t$ se cancelam, restando:

$$Ee^{-\xi\omega_n t}\text{sen}\,\omega_d t\left(\frac{\omega_n}{\sqrt{1-\xi^2}}\right) = 0$$

Logo, para $t=t_p$: $\text{sen}\,\omega_d t_p = 0 \Rightarrow \omega_d t_p = 0,\pi,2\pi,3\pi,\ldots$. Como $t_p$ corresponde ao **primeiro** pico:

$$\boxed{t_p = \frac{\pi}{\omega_d}}$$

### 4.4 Máximo sobressinal $M_p$

Valor máximo de pico da curva de resposta, medido a partir do valor de regime permanente, ocorrendo em $t_p$:

$$M_p = \frac{x(t_p)-E}{E}$$

Substituindo $t_p=\pi/\omega_d$ na equação (5) (com $\cos\pi=-1$, $\text{sen}\,\pi=0$):

$$M_p = \frac{-Ee^{-\xi\omega_n\pi/\omega_d}\left(\cos\pi + \dfrac{\xi}{\sqrt{1-\xi^2}}\text{sen}\,\pi\right)}{E} = -e^{-\xi\omega_n\pi/\omega_d}(-1) = e^{-\xi\omega_n\pi/\omega_d}$$

Como $\omega_n/\omega_d = 1/\sqrt{1-\xi^2}$:

$$\boxed{M_p = e^{-\frac{\xi\pi}{\sqrt{1-\xi^2}}}}$$

> **Observação central:** $M_p$ depende **apenas de $\xi$**, não de $\omega_n$. Isso permite ao projetista escolher $\xi$ para controlar o *quanto* o sistema ultrapassa o valor final, independentemente de quão rápida é a resposta.

### 4.5 Tempo de acomodação $t_s$

Tempo necessário para que a resposta alcance (e permaneça) numa faixa de $2\%$ ou $5\%$ em torno do valor de regime permanente.

Da equação (6), as **envoltórias** da resposta transitória são:

$$E \pm E\frac{e^{-\xi\omega_n t}}{\sqrt{1-\xi^2}}$$

A taxa de decaimento depende da constante de tempo $T = 1/(\xi\omega_n)$. Para $0<\xi<1$:

| Critério | $t_s$ |
|---|---|
| 2% | $t_s = 4T = \dfrac{4}{\xi\omega_n}$ |
| 5% | $t_s = 3T = \dfrac{3}{\xi\omega_n}$ |

> **Implicação prática:** como $\xi$ é determinado unicamente pela especificação de $M_p$, e $t_s$ depende do produto $\xi\omega_n$, o tempo de acomodação acaba sendo determinado, na prática, pela escolha de $\omega_n$ — os dois parâmetros de projeto ($\xi$ para overshoot, $\omega_n$ para velocidade) têm papéis quase desacoplados.

### 4.6 Exemplo numérico completo (Figura 12)

Dados: $\xi=0{,}6$, $\omega_n=5{,}0\,\text{rad/s}$, $E=1$ (degrau unitário).

$$\omega_d = \omega_n\sqrt{1-\xi^2} = 5{,}0\times\sqrt{1-0{,}6^2} = 4{,}0\,\text{rad/s}$$

$$t_r = \frac{\pi - \text{tg}^{-1}(4{,}0/3{,}0)}{4{,}0} = 0{,}554\,\text{s}$$

$$t_p = \frac{\pi}{4{,}0} = 0{,}785\,\text{s}$$

$$t_s = \frac{4}{0{,}6\times5{,}0} = 1{,}33\,\text{s} \quad \text{(critério 2\%)}$$

$$M_p = e^{-\frac{0{,}6\pi}{\sqrt{1-0{,}6^2}}} = 0{,}0948 = 9{,}48\%$$

---

## 5. Resposta ao impulso

### 5.1 Definição da entrada impulso

$$r(t) = \begin{cases} \lim\limits_{t_0\to0}\dfrac{E}{t_0} & 0<t<t_0 \\ 0 & t<0 \text{ ou } t_0<t \end{cases}$$

Ou seja, um pulso infinitesimalmente estreito, infinitamente alto, cuja área total é $E$.

### 5.2 Soluções nos três regimes (condições iniciais nulas)

**Subamortecido ($0<\xi<1$):**

$$x(t) = \frac{\omega_n}{\sqrt{1-\xi^2}}e^{-\xi\omega_n t}\,\text{sen}\left(\omega_n\sqrt{1-\xi^2}\,t\right), \quad t\geq 0 \qquad (9)$$

**Criticamente amortecido ($\xi=1$):**

$$x(t) = \omega_n^2 t\,e^{-\omega_n t}, \quad t\geq 0 \qquad (10)$$

**Superamortecido ($\xi>1$):**

$$x(t) = \frac{\omega_n}{2\sqrt{\xi^2-1}}e^{-(\xi-\sqrt{\xi^2-1})\omega_n t} - \frac{\omega_n}{2\sqrt{\xi^2-1}}e^{-(\xi+\sqrt{\xi^2-1})\omega_n t}, \quad t\geq 0 \qquad (11)$$

### 5.3 Tempo de pico e valor de pico (resposta ao impulso, subamortecido)

Derivando (9) e igualando a zero:

$$t_p = \frac{\text{tg}^{-1}\left(\dfrac{\sqrt{1-\xi^2}}{\xi}\right)}{\omega_n\sqrt{1-\xi^2}}$$

Substituindo em (9):

$$x(t_p) = \omega_n\,e^{-\frac{\xi}{\sqrt{1-\xi^2}}\text{tg}^{-1}\left(\frac{\sqrt{1-\xi^2}}{\xi}\right)}$$

### 5.4 Conexão elegante entre impulso e degrau

A resposta ao impulso é, por propriedade geral de sistemas lineares, a **derivada** da resposta ao degrau. Isso gera uma relação geométrica direta (Figura 14):

> A área sob a curva de resposta ao impulso unitário, de $t=0$ até o instante do primeiro zero, é igual a $1+M_p$. O tempo de pico $t_p$ da resposta ao degrau unitário corresponde ao instante em que a resposta ao impulso unitário **cruza o eixo do tempo pela primeira vez**.

Essa propriedade permite "ler" o sobressinal $M_p$ e o tempo de pico $t_p$ da resposta ao degrau diretamente na curva de resposta ao impulso, sem resolver a equação da resposta ao degrau.

---

## 6. Síntese geral

### 6.1 Quadro-resumo das especificações (entrada degrau, $0<\xi<1$)

| Especificação | Símbolo | Fórmula |
|---|---|---|
| Tempo de atraso | $t_d$ | resposta atinge 50% do valor final |
| Tempo de subida | $t_r$ | $\dfrac{\pi - \text{tg}^{-1}(\omega_d/\xi\omega_n)}{\omega_d}$ |
| Tempo de pico | $t_p$ | $\dfrac{\pi}{\omega_d}$ |
| Máximo sobressinal | $M_p$ | $e^{-\xi\pi/\sqrt{1-\xi^2}}$ |
| Tempo de acomodação (2%) | $t_s$ | $\dfrac{4}{\xi\omega_n}$ |
| Tempo de acomodação (5%) | $t_s$ | $\dfrac{3}{\xi\omega_n}$ |

### 6.2 Conexão com a Aula 1

- A **estabilidade** (Aula 1) continua determinada exclusivamente pelas raízes da equação característica (parte real negativa ⇒ assintoticamente estável), **independente da entrada** $r(t)$.
- A entrada $r(t)$ (degrau, impulso) afeta apenas o **valor de regime permanente** e a **forma da resposta transitória**, não a classificação de estabilidade.
- A forma padrão $(\xi,\omega_n)$ é a ponte entre a análise qualitativa de estabilidade e o **projeto de controladores**: especificações de desempenho (overshoot, tempo de acomodação, tempo de subida) são a "linguagem" usada para especificar o comportamento desejado de um sistema controlado, e $\xi$ e $\omega_n$ podem ser ajustados (via projeto de controlador) para atendê-las.

---

## 7. Referências bibliográficas

- **OGATA, K.** *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- **BOYCE, W. E.; DIPRIMA, R. C.** *Equações Diferenciais Elementares e Problemas de Valores de Contorno*. 8ª ed. LTC, 2006.
- **ZILL, D. G.** *Equações Diferenciais*. 3ª ed., vol. 1. Pearson Makron Books, 2006.
- **ZILL, D. G.** *Equações Diferenciais com Aplicações em Modelagem*. Thomson, 2003.

---

*Material elaborado como notas de estudo, a partir dos slides da disciplina ESTA020-17 (Modelagem e Controle) — UFABC.*