# Modelagem Matemática de Sistemas Dinâmicos no Espaço de Estado


## Índice

1. [Conceitos fundamentais](#1-conceitos-fundamentais)
2. [Forma geral no espaço de estado](#2-forma-geral-no-espaço-de-estado)
3. [Linearização e forma matricial](#3-linearização-e-forma-matricial)
4. [Sistemas lineares invariantes no tempo](#4-sistemas-lineares-invariantes-no-tempo)
5. [Exemplo âncora: 2ª ordem na forma padrão](#5-exemplo-âncora-2ª-ordem-na-forma-padrão)
6. [Autovalores de A — generalização da equação característica](#6-autovalores-de-a--generalização-da-equação-característica)
7. [Exemplo 1 — Sistema massa-mola-amortecedor](#7-exemplo-1--sistema-massa-mola-amortecedor)
8. [Exemplo 2 — Sistema mecânico com duas massas](#8-exemplo-2--sistema-mecânico-com-duas-massas)
9. [Síntese geral](#9-síntese-geral)

---

## 1. Conceitos fundamentais

### Estado

É o **menor conjunto de variáveis** tal que o conhecimento delas em $t=t_0$, juntamente com o conhecimento da entrada para $t\geq t_0$, determina completamente o comportamento do sistema para qualquer instante $t\geq t_0$.

### Variáveis de estado

É o menor conjunto de variáveis capaz de determinar o estado do sistema dinâmico. Se pelo menos $n$ variáveis $x_1(t), x_2(t),\ldots,x_n(t)$ são necessárias para descrever todo o comportamento de um sistema dinâmico, então essas $n$ variáveis formam um conjunto de variáveis de estado. É conveniente escolher grandezas **mensuráveis**.

### Vetor de estado

Se forem necessárias $n$ variáveis de estado para descrever completamente o comportamento de um sistema, então essas $n$ variáveis de estado são os $n$ componentes de um vetor $x(t)$, chamado de **vetor de estado**. Dado o estado em $t=t_0$ e a entrada $u(t)$ para $t\geq t_0$, o vetor de estado determina de forma única o estado do sistema para qualquer instante $t\geq t_0$.

### Espaço de estado

É o espaço $n$-dimensional cujos eixos coordenados são formados pelos eixos das variáveis de estado. Qualquer estado pode ser representado por **um ponto** no espaço de estado.

> **Conexão com a Aula 1:** é exatamente esse o espaço onde vivem as regiões $S(\delta)$ e $S(\xi)$ da análise de estabilidade de Lyapunov — o espaço de estado formaliza "quem são" os eixos desse espaço.

### A representação não é única

A representação de um determinado sistema no espaço de estado **não é única**, mas o número de variáveis de estado é o mesmo para qualquer uma das diferentes representações desse mesmo sistema.

### Regra prática: variáveis de estado ↔ integradores

O sistema dinâmico deve conter elementos que memorizem os valores da entrada para $t\geq t_1$. Os integradores em um sistema de controle de tempo contínuo servem como dispositivos de memória, de maneira que suas saídas podem ser escolhidas como variáveis de estado.

> **O número de variáveis de estado que definem completamente a dinâmica de um sistema é igual ao número de integradores existentes no sistema.**

### As três famílias de variáveis

A análise no espaço de estado envolve três tipos de variáveis presentes na modelagem de sistemas dinâmicos:

| Variável | Símbolo | Papel |
|---|---|---|
| Entrada | $u(t)$ | O que se aplica ao sistema (controle, referência) |
| Saída | $y(t)$ | O que se observa/mede do sistema |
| Estado | $x(t)$ | Memória interna do sistema |

Notação usada: $\dot{x}(t) = \dfrac{dx(t)}{dt}$ e $\ddot{x}(t) = \dfrac{d^2x(t)}{dt^2}$.

---

## 2. Forma geral no espaço de estado

Suponha um sistema com $r$ variáveis de entrada $u_1(t),\ldots,u_r(t)$ e $m$ variáveis de saída $y_1(t),\ldots,y_m(t)$ que envolva $n$ integradores. Isso define as $n$ variáveis de estado $x_1(t),\ldots,x_n(t)$. Assim:

$$\dot{x}_1(t) = f_1(x_1,\ldots,x_n;u_1,\ldots,u_r;t)$$
$$\dot{x}_2(t) = f_2(x_1,\ldots,x_n;u_1,\ldots,u_r;t)$$
$$\vdots$$
$$\dot{x}_n(t) = f_n(x_1,\ldots,x_n;u_1,\ldots,u_r;t)$$

As saídas $y_1(t),\ldots,y_m(t)$ do sistema são dadas por:

$$y_1(t) = g_1(x_1,\ldots,x_n;u_1,\ldots,u_r;t)$$
$$\vdots$$
$$y_m(t) = g_m(x_1,\ldots,x_n;u_1,\ldots,u_r;t)$$

> **Ideia fundamental:** descrever um sistema dinâmico de ordem $n$ através de $n$ equações diferenciais de **primeira ordem**, em vez de uma única equação de ordem $n$ (abordagem usada nas Aulas 1 e 2).

### Forma vetorial compacta

Definindo:

$$\dot{x}(t) = \begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\\\vdots\\\dot{x}_n(t)\end{bmatrix}, \quad f(x,u,t)=\begin{bmatrix}f_1(\cdots)\\f_2(\cdots)\\\vdots\\f_n(\cdots)\end{bmatrix}, \quad y(t)=\begin{bmatrix}y_1(t)\\y_2(t)\\\vdots\\y_m(t)\end{bmatrix}, \quad g(x,u,t)=\begin{bmatrix}g_1(\cdots)\\g_2(\cdots)\\\vdots\\g_m(\cdots)\end{bmatrix}, \quad u(t)=\begin{bmatrix}u_1(t)\\u_2(t)\\\vdots\\u_r(t)\end{bmatrix}$$

chega-se a:

$$\dot{x}(t) = f(x,u,t) \qquad (1) \quad \text{(equação de estado)}$$

$$y(t) = g(x,u,t) \qquad (2) \quad \text{(equação de saída)}$$

Se as funções vetoriais $f$ ou $g$ envolvem explicitamente o tempo $t$, o sistema é **variante no tempo**.

---

## 3. Linearização e forma matricial

Para as equações (1) e (2) linearizadas em torno de um ponto de operação:

$$\begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\\\vdots\\\dot{x}_n(t)\end{bmatrix} = \begin{bmatrix}a_{11}(t) & \cdots & a_{1n}(t)\\ \vdots & \ddots & \vdots \\ a_{n1}(t) & \cdots & a_{nn}(t)\end{bmatrix}\begin{bmatrix}x_1(t)\\\vdots\\x_n(t)\end{bmatrix} + \begin{bmatrix}b_{11}(t) & \cdots & b_{1r}(t)\\ \vdots & & \vdots \\ b_{n1}(t) & \cdots & b_{nr}(t)\end{bmatrix}\begin{bmatrix}u_1(t)\\\vdots\\u_r(t)\end{bmatrix}$$

$$y(t) = \begin{bmatrix}c_1(t) & \cdots & c_n(t)\end{bmatrix}\begin{bmatrix}x_1(t)\\\vdots\\x_n(t)\end{bmatrix} + \begin{bmatrix}d_{11}(t) & \cdots \\ \vdots & \end{bmatrix}\begin{bmatrix}u_1(t)\\\vdots\end{bmatrix}$$

ou, na forma vetorial-matricial:

$$\dot{x}(t) = A(t)x(t) + B(t)u(t)$$
$$y(t) = C(t)x(t) + D(t)u(t)$$

| Matriz | Nome | Dimensão |
|---|---|---|
| $A(t)$ | matriz de estado | $n\times n$ |
| $B(t)$ | matriz de entrada | $n\times r$ |
| $C(t)$ | matriz de saída | $m\times n$ |
| $D(t)$ | matriz de transmissão direta | $m\times r$ |

### Representação em diagrama de blocos

```
u(t) ──►[B]──►(+)──►[∫dt]──x(t)──►[C]──►(+)──► y(t)
              ▲                              ▲
              │                              │
            [A]◄────x(t)                   [D]◄──u(t)
```

O sinal $u(t)$ passa por $B$, soma-se à realimentação de $x(t)$ via $A$, integra-se para obter $x(t)$, que passa por $C$ para compor $y(t)$ — com $D$ representando o "caminho direto" de $u$ para $y$, sem passar pelo integrador.

*(Fonte da figura original: OGATA, K. Engenharia de Controle Moderno, 4ª ed., Pearson & Prentice Hall, 2005.)*

---

## 4. Sistemas lineares invariantes no tempo

Se as funções $f$ e $g$ **não envolvem o tempo $t$ explicitamente**, o sistema é **invariante no tempo**. As matrizes tornam-se constantes:

$$\begin{bmatrix}\dot{x}_1(t)\\\vdots\\\dot{x}_n(t)\end{bmatrix} = \begin{bmatrix}a_{11} & \cdots & a_{1n}\\ \vdots & \ddots & \vdots \\ a_{n1} & \cdots & a_{nn}\end{bmatrix}\begin{bmatrix}x_1(t)\\\vdots\\x_n(t)\end{bmatrix} + \begin{bmatrix}b_{11} & \cdots & b_{1r}\\ \vdots & & \vdots \\ b_{n1} & \cdots & b_{nr}\end{bmatrix}\begin{bmatrix}u_1(t)\\\vdots\\u_r(t)\end{bmatrix}$$

$$y(t) = \begin{bmatrix}c_1 & \cdots & c_n\end{bmatrix}\begin{bmatrix}x_1(t)\\\vdots\\x_n(t)\end{bmatrix} + \begin{bmatrix}d_{11}&\cdots\\ \vdots & \end{bmatrix}\begin{bmatrix}u_1(t)\\\vdots\end{bmatrix}$$

ou, na forma vetorial-matricial:

$$\boxed{\dot{x}(t) = Ax(t) + Bu(t)}$$
$$\boxed{y(t) = Cx(t) + Du(t)}$$

nas quais $A$ é a matriz de estado, $B$ a matriz de entrada, $C$ a matriz de saída, e $D$ a matriz de transmissão direta — todas **constantes**. Essa é a forma usada na maior parte do restante da disciplina.

---

## 5. Exemplo âncora: 2ª ordem na forma padrão

Conectando diretamente com a Aula 2, a equação diferencial linear de 2ª ordem na forma padrão:

$$\ddot{x}(t) + 2\xi\omega_n\dot{x}(t) + \omega_n^2x(t) = \omega_n^2u(t) \qquad (3)$$

na qual $\omega_n$ é a frequência natural não amortecida e $\xi$ é o fator de amortecimento, pode ser representada em variáveis de estado.

### Escolha das variáveis de estado

$$x_1(t) = x(t), \qquad x_2(t) = \dot{x}(t) = \dot{x}_1(t)$$

> Posição e velocidade — exatamente as duas condições iniciais necessárias para resolver a EDO de 2ª ordem original ($x_0$ e $dx_0/dt$). O número de variáveis de estado (2) coincide com a ordem da EDO (2ª ordem).

### Equações de estado

$$\dot{x}_2(t) = \ddot{x}(t) = -\omega_n^2x(t) - 2\xi\omega_n\dot{x}(t) + \omega_n^2u(t) = -\omega_n^2x_1(t) - 2\xi\omega_nx_2(t) + \omega_n^2u(t)$$

### Forma matricial

$$\begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\end{bmatrix} = \begin{bmatrix}0 & 1\\-\omega_n^2 & -2\xi\omega_n\end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix} + \begin{bmatrix}0\\\omega_n^2\end{bmatrix}u(t), \qquad y(t) = \begin{bmatrix}1&0\end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix}$$

$$A = \begin{bmatrix}0&1\\-\omega_n^2&-2\xi\omega_n\end{bmatrix}, \quad B=\begin{bmatrix}0\\\omega_n^2\end{bmatrix}, \quad C=\begin{bmatrix}1&0\end{bmatrix}, \quad D=0$$

---

## 6. Autovalores de A — generalização da equação característica

Os **autovalores** da matriz $A$ fazem exatamente o mesmo papel que as raízes $\alpha_1,\alpha_2$ da equação característica faziam nas Aulas 1 e 2 — agora generalizado para sistemas com múltiplas variáveis de estado.

Definidos por:

$$\det(\alpha I - A) = 0$$

na qual $I$ é a matriz identidade de ordem $n$. Para o exemplo âncora ($n=2$):

$$\det\left(\begin{bmatrix}\alpha&0\\0&\alpha\end{bmatrix}-\begin{bmatrix}0&1\\-\omega_n^2&-2\xi\omega_n\end{bmatrix}\right)=0 \Rightarrow \det\begin{pmatrix}\alpha&-1\\\omega_n^2&\alpha+2\xi\omega_n\end{pmatrix}=0 \Rightarrow \alpha^2+2\xi\omega_n\alpha+\omega_n^2=0$$

Que é **exatamente a mesma equação característica** já deduzida diretamente da EDO na Aula 2:

$$\alpha = \frac{-2\xi\omega_n\pm\sqrt{4\xi^2\omega_n^2-4\omega_n^2}}{2} = -\xi\omega_n\pm\omega_n\sqrt{\xi^2-1} \Rightarrow \boxed{\alpha = -\xi\omega_n\pm j\omega_n\sqrt{1-\xi^2}}$$

> **Conclusão central:** os autovalores da matriz $A$ generalizam as raízes da equação característica. Toda a teoria de estabilidade construída nas Aulas 1 e 2 (parte real negativa ⇒ assintoticamente estável) se aplica diretamente aos autovalores de $A$, agora para sistemas de ordem $n$ arbitrária — sem depender de resolver EDOs de ordem alta "na mão".

---

## 7. Exemplo 1 — Sistema massa-mola-amortecedor

**Enunciado:** sistema mecânico massa-mola-amortecedor, linear e invariante no tempo (Figura 3), com entrada $u(t)$ = força externa aplicada na massa, e saída $y(t)$ = deslocamento $w(t)$ da massa a partir do equilíbrio. Massa $m=3\,\text{kg}$. Determinar $k$ (constante elástica) e $b$ (fator de amortecimento do amortecedor) de modo que $M_p=14{,}7\%$ e $t_s=0{,}5\,\text{s}$ para entrada degrau unitário.

*(Fonte da figura original: OGATA, K. Engenharia de Controle Moderno, 4ª ed., Pearson & Prentice Hall, 2005.)*

### 7.1 Modelagem física (2ª lei de Newton)

$$\sum_{i=1}^{3}\vec{F}_i = m\vec{a} \Rightarrow -kw(t) - b\dot{w}(t) + ku(t) = m\ddot{w}(t)$$

$$\Rightarrow m\ddot{w}(t)+b\dot{w}(t)+kw(t) = ku(t) \Rightarrow \ddot{w}(t)+\frac{b}{m}\dot{w}(t)+\frac{k}{m}w(t)=\frac{k}{m}u(t)$$

Comparando com a forma padrão $\ddot{w}(t)+2\xi\omega_n\dot{w}(t)+\omega_n^2w(t)=\omega_n^2u(t)$:

$$\omega_n^2 = \frac{k}{m} \Rightarrow k=m\omega_n^2, \qquad 2\xi\omega_n = \frac{b}{m} \Rightarrow b=2m\xi\omega_n$$

> Sistema de 2ª ordem → **2 integradores** → **2 variáveis de estado**.

### 7.2 Representação em espaço de estados

$$x_1(t)=w(t), \qquad x_2(t)=\dot{w}(t)=\dot{x}_1(t)$$

$$\dot{x}_2(t) = \ddot{w}(t) = -\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)+\frac{k}{m}u(t) = -\frac{k}{m}x_1(t)-\frac{b}{m}x_2(t)+\frac{k}{m}u(t)$$

Equação de saída: $y(t)=w(t)=x_1(t)$.

$$\begin{bmatrix}\dot{x}_1(t)\\\dot{x}_2(t)\end{bmatrix} = \begin{bmatrix}0&1\\-k/m&-b/m\end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix} + \begin{bmatrix}0\\k/m\end{bmatrix}u(t), \qquad y(t)=\begin{bmatrix}1&0\end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t)\end{bmatrix}$$

$$A=\begin{bmatrix}0&1\\-k/m&-b/m\end{bmatrix}, \quad B=\begin{bmatrix}0\\k/m\end{bmatrix}, \quad C=\begin{bmatrix}1&0\end{bmatrix}, \quad D=0$$

### 7.3 Projeto: de especificações a parâmetros físicos

**Passo 1 — Isolar $\xi$ a partir de $M_p$.** Invertendo $M_p=e^{-\xi\pi/\sqrt{1-\xi^2}}$:

$$\ln(M_p) = -\frac{\xi\pi}{\sqrt{1-\xi^2}} \Rightarrow (\ln M_p)^2 = \frac{\xi^2\pi^2}{1-\xi^2} \Rightarrow (\ln M_p)^2(1-\xi^2)=\xi^2\pi^2$$

$$(\ln M_p)^2 = \xi^2\left[(\ln M_p)^2+\pi^2\right] \Rightarrow \xi^2 = \frac{(\ln M_p)^2}{(\ln M_p)^2+\pi^2}$$

$$\xi = \sqrt{\frac{(\ln(0{,}147))^2}{(\ln(0{,}147))^2+\pi^2}} = 0{,}521$$

**Passo 2 — Isolar $\omega_n$ a partir de $t_s$** (critério 2%):

$$t_s = \frac{4}{\xi\omega_n} \Rightarrow \omega_n = \frac{4}{t_s\xi} = \frac{4}{0{,}5\times0{,}521} = 15{,}4\,\text{rad/s}$$

**Passo 3 — Calcular $k$ e $b$:**

$$k = m\omega_n^2 = 3\times(15{,}4)^2 = 712\,\text{N/m}$$

$$b = 2m\xi\omega_n = 2\times3\times0{,}521\times15{,}4 = 48{,}1\,\text{Ns/m}$$

> **Observação metodológica:** este é o processo inverso do habitual — em vez de "dado o sistema, calcule $\xi$ e $\omega_n$", aqui as **especificações de desempenho vêm primeiro**, e delas derivam-se os **parâmetros físicos** do sistema ($k$, $b$). Isso é, literalmente, projetar/dimensionar um componente físico para atender requisitos de desempenho.

A Figura 5 apresenta a resposta de $x_2(t)$ (velocidade da massa) ao degrau unitário, exibindo o comportamento oscilatório amortecido esperado de um sistema subamortecido.

### 7.4 Verificação via autovalores

$$\det(\alpha I - A)=0 \Rightarrow \alpha^2+\frac{b}{m}\alpha+\frac{k}{m}=0$$

$$\alpha = \frac{-b\pm\sqrt{b^2-4mk}}{2m} = \frac{-48{,}1\pm\sqrt{48{,}1^2-4\times3\times712}}{2\times3} \Rightarrow \boxed{\alpha=-8{,}02\pm j13{,}2}$$

Parte real negativa → **sistema assintoticamente estável**, confirmando a consistência do projeto.

---

## 8. Exemplo 2 — Sistema mecânico com duas massas

**Enunciado:** sistema mecânico (Figura 7) com duas massas $m_1=3\,\text{kg}$, $m_2=1\,\text{kg}$, acopladas por mola $k_2=20\,\text{N/m}$ e amortecedor $b=10\,\text{Ns/m}$, cada massa também ligada à base por $k_1=10\,\text{N/m}$ e $k_3=30\,\text{N/m}$ respectivamente. Entrada $u(t)$ aplicada em $m_1$.

*(Fonte da figura original: OGATA, K. Engenharia de Controle Moderno, 4ª ed., Pearson & Prentice Hall, 2005.)*

### 8.1 Equações de Newton

**Massa $m_1$:**

$$\sum_{i=1}^{4}\vec{F}_i = m_1\vec{a} \Rightarrow -k_1w_1(t)-k_2(w_1(t)-w_2(t))-b(\dot{w}_1(t)-\dot{w}_2(t))+u(t)=m_1\ddot{w}_1(t)$$

$$m_1\ddot{w}_1(t) = -b\dot{w}_1(t)-(k_1+k_2)w_1(t)+b\dot{w}_2(t)+k_2w_2(t)+u(t)$$

$$\ddot{w}_1(t) = -\frac{(k_1+k_2)}{m_1}w_1(t)+\frac{k_2}{m_1}w_2(t)-\frac{b}{m_1}\dot{w}_1(t)+\frac{b}{m_1}\dot{w}_2(t)+\frac{1}{m_1}u(t)$$

**Massa $m_2$:**

$$\sum_{i=1}^{3}\vec{F}_i = m_2\vec{a} \Rightarrow -k_3w_2(t)-k_2(w_2(t)-w_1(t))-b(\dot{w}_2(t)-\dot{w}_1(t))=m_2\ddot{w}_2(t)$$

$$m_2\ddot{w}_2(t)+b\dot{w}_2(t)+(k_2+k_3)w_2(t) = b\dot{w}_1(t)+k_2w_1(t)$$

$$\ddot{w}_2(t) = \frac{k_2}{m_2}w_1(t)-\frac{(k_2+k_3)}{m_2}w_2(t)-\frac{b}{m_2}\dot{w}_2(t)+\frac{b}{m_2}\dot{w}_1(t)$$

### 8.2 Variáveis de estado

Com duas massas, cada uma contribuindo posição + velocidade: **4 integradores** → **4 variáveis de estado**:

$$x_1(t)=w_1(t), \quad x_2(t)=w_2(t), \quad x_3(t)=\dot{w}_1(t), \quad x_4(t)=\dot{w}_2(t)$$

### 8.3 Equações de estado

$$\dot{x}_1(t) = x_3(t)$$
$$\dot{x}_2(t) = x_4(t)$$
$$\dot{x}_3(t) = -\frac{(k_1+k_2)}{m_1}x_1(t)+\frac{k_2}{m_1}x_2(t)-\frac{b}{m_1}x_3(t)+\frac{b}{m_1}x_4(t)+\frac{1}{m_1}u(t)$$
$$\dot{x}_4(t) = \frac{k_2}{m_2}x_1(t)-\frac{(k_2+k_3)}{m_2}x_2(t)+\frac{b}{m_2}x_3(t)-\frac{b}{m_2}x_4(t)$$

Equação de saída (sistema MIMO: 1 entrada, 2 saídas): $y_1(t)=w_1(t)=x_1(t)$, $y_2(t)=w_2(t)=x_2(t)$.

> **Padrão geral:** as duas primeiras equações ($\dot{x}_1=x_3$, $\dot{x}_2=x_4$) são apenas as **definições** de velocidade (derivada da posição), sem informação física nova — toda a física de Newton está concentrada em $\dot{x}_3$ e $\dot{x}_4$. Em sistemas mecânicos com $n$ graus de liberdade, sempre metade das equações de estado é "trivial" (posição→velocidade) e a outra metade vem diretamente de Newton.

### 8.4 Resposta dinâmica (Figura 8)

Condições iniciais: $x_1(0)=0{,}4\,\text{m}$, $x_2(0)=0{,}2\,\text{m}$, $x_3(0)=0$, $x_4(0)=0$; entrada degrau unitário. As quatro variáveis de estado (posições $x_1,x_2$ e velocidades $x_3,x_4$) oscilam de forma amortecida, convergindo para um novo ponto de equilíbrio — comportamento típico de sistema subamortecido.

### 8.5 Plano de fase (Figura 9)

O **plano de fase** apresenta gráficos de velocidade *vs.* posição (ex.: $x_3(t)$ *vs.* $x_1(t)$), em vez de cada variável *vs.* tempo. As trajetórias espiraladas convergindo para um ponto central indicam que os pontos de equilíbrio são **focos estáveis**.

> **Conexão com a Aula 1:** essa é literalmente uma trajetória $x(t)$ no espaço de estados, espiralando e convergindo para $x_e$ — a mesma imagem conceitual da Figura 1 da Aula 1 ("Assintoticamente estável"), agora vista sem o eixo do tempo, gerada por um sistema físico real de 2 graus de liberdade.

---

## 9. Síntese geral

### 9.1 Por que os dois exemplos são complementares

1. **Exemplo 1** mostra o fluxo **especificação → parâmetros físicos**: dado um desempenho desejado ($M_p$, $t_s$), "projeta-se" o sistema (encontram-se $k$, $b$) — a essência do projeto de controle.
2. **Exemplo 2** mostra a **escalabilidade** do espaço de estados: sistemas mais complexos (mais massas, mais graus de liberdade) geram simplesmente **mais variáveis de estado**, mas seguem exatamente a mesma estrutura matricial $\dot{x}=Ax+Bu$ — sem mudança conceitual, apenas aumento de dimensão.

### 9.2 Conexão com as Aulas 1 e 2

- O **espaço de estado** formaliza o espaço onde vivem as regiões $S(\delta)$, $S(\xi)$ da análise de Lyapunov (Aula 1).
- Os **autovalores de $A$** generalizam as raízes da equação característica (Aula 2): parte real negativa continua sendo o critério de estabilidade assintótica, agora aplicável a sistemas de ordem $n$ qualquer, sem depender de resolver uma EDO de ordem alta diretamente.
- O **plano de fase** oferece uma visualização geométrica direta das trajetórias no espaço de estado — a mesma ideia da Figura 1 (Aula 1), agora aplicada a sistemas reais multidimensionais.
- Especificações de desempenho ($M_p$, $t_s$ — Aula 2) podem ser usadas tanto para **analisar** um sistema existente quanto para **projetar** (dimensionar) seus parâmetros físicos, como no Exemplo 1.

---

## Referências

- OGATA, K. *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 3*. Slides de aula, UFABC, 2021.

---

*Material elaborado como notas de estudo, a partir dos slides da disciplina ESTA020-17 (Modelagem e Controle) — UFABC.*
