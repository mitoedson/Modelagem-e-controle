# Análise de Estabilidade de Lyapunov

## Índice

1. [Primeiro método de Lyapunov](#1-primeiro-método-de-lyapunov)
2. [Exemplo — pêndulo simples sem atrito](#2-exemplo--pêndulo-simples-sem-atrito)
3. [Exemplo — pêndulo simples com atrito](#3-exemplo--pêndulo-simples-com-atrito)
4. [Segundo método de Lyapunov](#4-segundo-método-de-lyapunov)
5. [Síntese geral](#5-síntese-geral)


## 1. Primeiro método de Lyapunov

### 1.1 Ideia central

O primeiro método de Lyapunov também é conhecido como **método indireto** ou **método da linearização**. Ele permite investigar a estabilidade local de um sistema não linear através do seu modelo linearizado.

Os sistemas não lineares podem ser aproximados por truncamento da representação em série de Taylor em torno dos pontos de equilíbrio para que a sua estabilidade seja estudada através dos autovalores.

**Série de Taylor:**

$$f(x)=f(x_e)+\left.\frac{df(x)}{dx}\right|_{x=x_e}(x-x_e)+\ldots+\frac{1}{n!}\left.\frac{d^nf(x)}{dx^n}\right|_{x=x_e}(x-x_e)^n$$

**Exemplos:**

Para $f(x)=\text{sen}\,x$ e $x_e=0$, temos que $f(x)\approx\text{sen}\,0+\cos0(x-0)\Rightarrow f(x)\approx x$.

Para $f(x)=\cos x$ e $x_e=0$, temos que $f(x)\approx\cos0-\text{sen}\,0(x-0)\Rightarrow f(x)\approx1$.

Para $f(x)=\text{sen}\,x$ e $x_e=\pi$, temos que $f(x)\approx\text{sen}\,\pi+\cos\pi(x-\pi)\Rightarrow f(x)\approx-x+\pi$.

Para $f(x)=\text{sen}\,x$ e $x_e=\dfrac{\pi}{2}$, temos que $f(x)\approx\text{sen}\,\dfrac{\pi}{2}+\cos\dfrac{\pi}{2}\left(x-\dfrac{\pi}{2}\right)\Rightarrow f(x)\approx1$.

> A linearização por série de Taylor é sempre feita em torno de um ponto de equilíbrio específico $x_e$ — a aproximação só é localmente válida na vizinhança desse ponto.

### 1.2 Linearização de sistemas dinâmicos

Considere o sistema dinâmico descrito por $\dot{x}(t)=f(x,u)$, no qual $x_e$ é o ponto de equilíbrio correspondente a uma entrada constante $u(t)=u_e$ (degrau), ou seja, $\dot{x}(t)=f(x_e,u_e)=0$.

Para uma entrada perturbada $u(t)=u_e+v(t)$, o estado perturbado é do tipo $x(t)=x_e+\xi(t)$, de maneira que

$$\frac{dx(t)}{dt} = \frac{d(x_e+\xi(t))}{dt} = \underbrace{\frac{dx_e}{dt}}_{0}+\frac{d\xi(t)}{dt} = f(x,u) = f(x_e+\xi(t),u_e+v(t))$$

$$= \underbrace{f(x_e,u_e)}_{0}+\underbrace{\nabla_xf(x_e,u_e)}_{A=\left.\frac{\partial f(x,u)}{\partial x}\right|_{x=x_e,\,u=u_e}}\xi(t)+\underbrace{\nabla_uf(x_e,u_e)}_{B=\left.\frac{\partial f(x,u)}{\partial u}\right|_{x=x_e,\,u=u_e}}v(t)+\underbrace{o(||\xi(t),v(t)||^2)}_{\text{termos de ordem superior}}$$

O modelo linearizado é dado por

$$\boxed{\frac{d\xi(t)}{dt}=A\xi(t)+Bv(t)}$$

> Os termos de ordem superior $o(||\xi(t),v(t)||^2)$ são desprezados — a validade da aproximação depende de $\xi(t)$ e $v(t)$ permanecerem "pequenos", ou seja, o estado e a entrada perturbados devem se manter próximos do ponto de equilíbrio $(x_e,u_e)$.

### 1.3 Teorema do primeiro método de Lyapunov

> **Teorema 0.1 [Primeiro método de Lyapunov]**
>
> i) Se o modelo linearizado é assintoticamente estável, então o sistema original é assintoticamente estável em torno de $x_e$.
>
> ii) Se o modelo linearizado é instável, então o sistema original é instável em torno de $x_e$.

Se o modelo linearizado é estável, mas não é assintoticamente estável, ou seja, se algum autovalor de $A$ estiver sobre o eixo imaginário, **nada pode ser afirmado** sobre a estabilidade do sistema original.

> Este é o ponto central do método: ele é **conclusivo** apenas em dois casos (assintoticamente estável ou instável). Quando os autovalores de $A$ incluem algum sobre o eixo imaginário (parte real nula), o primeiro método de Lyapunov é **inconclusivo**, e outra ferramenta — como o segundo método de Lyapunov — é necessária.

---

## 2. Exemplo — pêndulo simples sem atrito

### 2.1 Modelagem

Considere um pêndulo simples sem atrito, composto por uma haste rígida de comprimento $l$ e massa desprezível. Na sua extremidade móvel, existe uma massa $m$ sujeita à aceleração da gravidade $g$. O ângulo de rotação $\theta(t)$ é formado entre a haste e o eixo vertical. Pela segunda lei de Newton para o sistema rotacional, temos que $\sum_{i=1}^n\vec{\tau}_i=J\vec{\alpha}$, na qual $\tau$ é o torque, $J=\sum_{j=1}^n m_ir_i^2$ é o momento de inércia e $\alpha$ é a aceleração angular. Os valores de $m$, $g$ e $l$ são estritamente positivos. Logo,

$$-mgl\,\text{sen}\,\theta(t)=ml^2\ddot{\theta}(t) \Rightarrow \ddot{\theta}(t)=-\frac{g}{l}\text{sen}\,\theta(t)$$

Definindo as variáveis de estado como $x_1(t)=\theta(t)$ e $x_2(t)=\dot{\theta}(t)$, temos que

$$\dot{x}_1(t) = x_2(t)$$
$$\dot{x}_2(t) = -\frac{g}{l}\text{sen}\,x_1(t)$$

Pelas condições de equilíbrio, temos que $\dot{x}_1(t)=\dot{x}_2(t)=0$ e, para $n=0,\pm1,\pm2,\ldots$. Portanto

$$0=x_2(t)$$
$$0=-\frac{g}{l}\text{sen}\,x_1(t) \Rightarrow \text{sen}\,x_1(t)=0 \Rightarrow x_1(t)=n\pi$$

Linearizando em $x_e=(n\pi,0)$, temos que

$$A=\left.\frac{\partial f(x,u)}{\partial x}\right|_{\theta(t)=n\pi,\,u=0} = \left[\begin{matrix}0 & 1\\-\frac{g}{l}\cos x_1(t) & 0\end{matrix}\right]_{x_1(t)=n\pi}$$

> Há **infinitos pontos de equilíbrio**, $x_e=(n\pi,0)$, todos fisicamente equivalentes dois a dois: $n$ par corresponde ao pêndulo na posição **para baixo** (equilíbrio esperado, estável) e $n$ ímpar à posição **invertida, para cima** (equilíbrio instável). Os dois casos representativos são analisados a seguir: $x_e=(0,0)$ e $x_e=(\pi,0)$.

### 2.2 Equilíbrio $x_e=(0,0)$ — pêndulo para baixo

Em torno de $x_e=(0,0)$, temos que $\cos0=1$. Assim,

$$A=\left[\begin{matrix}0 & 1\\-\dfrac{g}{l} & 0\end{matrix}\right]$$

e, portanto, os autovalores de $A$ são dados por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&1\\-\frac{g}{l}&0\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&1\\-\frac{g}{l}&0\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&-1\\\frac{g}{l}&\lambda\end{matrix}\right]\right)=0 \Rightarrow \lambda^2+\frac{g}{l}=0 \Rightarrow \boxed{\lambda=\pm j\sqrt{\frac{g}{l}}}$$

Os autovalores de $A$ são um par complexo conjugado **puramente imaginário** para quaisquer valores de $g$ e $l$ estritamente positivos e, portanto, **o primeiro método de Lyapunov não permite avaliar a estabilidade do sistema original em torno de $x_e=(0,0)$**.

> Resultado intuitivamente estranho à primeira vista: fisicamente, sabemos que o pêndulo sem atrito, deslocado da posição vertical inferior, oscila indefinidamente (nunca converge, nunca diverge) — é o caso "de fronteira" que o primeiro método de Lyapunov não consegue classificar.

### 2.3 Equilíbrio $x_e=(\pi,0)$ — pêndulo invertido

Em torno de $x_e=(\pi,0)$, temos que $\cos\pi=-1$. Assim,

$$A=\left[\begin{matrix}0 & 1\\\dfrac{g}{l} & 0\end{matrix}\right]$$

e, portanto, os autovalores de $A$ são dados por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&1\\\frac{g}{l}&0\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&1\\\frac{g}{l}&0\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&-1\\-\frac{g}{l}&\lambda\end{matrix}\right]\right)=0 \Rightarrow \lambda^2-\frac{g}{l}=0 \Rightarrow \boxed{\lambda=\pm\sqrt{\frac{g}{l}}}$$

Como existe um autovalor de $A$ no **semiplano direito** do plano complexo para quaisquer valores de $g$ e $l$ estritamente positivos, pelo primeiro método de Lyapunov, **conclui-se que o sistema original é instável em torno de $x_e=(\pi,0)$**.

> Coerente com a intuição física: o pêndulo invertido é um equilíbrio instável — qualquer perturbação, por menor que seja, faz o pêndulo cair.

---

## 3. Exemplo — pêndulo simples com atrito

### 3.1 Modelagem

Considere que haja atrito no pêndulo, com coeficiente de atrito $b$ estritamente positivo, de maneira que

$$-mgl\,\text{sen}\,\theta(t)-bl\dot{\theta}(t)=ml^2\ddot{\theta}(t) \Rightarrow \ddot{\theta}(t)=-\frac{g}{l}\text{sen}\,\theta(t)-\frac{b}{ml}\dot{\theta}(t)$$

Definindo as variáveis de estado como $x_1(t)=\theta(t)$ e $x_2(t)=\dot{\theta}(t)$, temos que

$$\dot{x}_1(t) = x_2(t)$$
$$\dot{x}_2(t) = -\frac{g}{l}\text{sen}\,x_1(t)-\frac{b}{ml}x_2(t)$$

Pelas condições de equilíbrio, temos que $\dot{x}_1(t)=\dot{x}_2(t)=0$ e, para $n=0,\pm1,\pm2,\ldots$, temos que

$$0=x_2(t)$$
$$0=-\frac{g}{l}\text{sen}\,x_1(t)-\frac{b}{ml}x_2(t) \Rightarrow \text{sen}\,x_1(t)=0 \Rightarrow x_1(t)=n\pi$$

Linearizando em $x_e=(n\pi,0)$, temos que

$$A=\left.\frac{\partial f(x,u)}{\partial x}\right|_{\theta(t)=n\pi,\,u=0} = \left[\begin{matrix}0 & 1\\-\frac{g}{l}\cos x_1(t) & -\frac{b}{ml}\end{matrix}\right]_{x_1(t)=n\pi}$$

### 3.2 Equilíbrio $x_e=(0,0)$ — pêndulo para baixo, com atrito

Em torno de $x_e=(0,0)$, temos que $\cos0=1$. Assim,

$$A=\left[\begin{matrix}0 & 1\\-\dfrac{g}{l} & -\dfrac{b}{ml}\end{matrix}\right]$$

e, portanto, a equação característica é dada por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&1\\-\frac{g}{l}&-\frac{b}{ml}\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&1\\-\frac{g}{l}&-\frac{b}{ml}\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&-1\\\frac{g}{l}&\lambda+\frac{b}{ml}\end{matrix}\right]\right)=0 \Rightarrow \lambda^2+\frac{b}{ml}\lambda+\frac{g}{l}=0 \Rightarrow \lambda=-\frac{b}{2ml}\pm\frac{\sqrt{b^2-4m^2gl}}{2ml}$$

**Caso $b^2-4m^2gl>0$:**

$$b^2-4m^2gl>0 \Rightarrow b^2>4m^2gl \Rightarrow b>\pm\sqrt{4m^2gl} \Rightarrow b>2m\sqrt{gl}$$

já que $b>0$. Logo, como $b>\sqrt{b^2-4m^2gl}$, para quaisquer valores de $m$, $g$ e $l$ positivos, os autovalores serão **reais e distintos**, de maneira que

$$\lambda=-\frac{b}{2ml}-\frac{\sqrt{b^2-4m^2gl}}{2ml}<0 \qquad \text{e} \qquad \lambda=-\frac{b}{2ml}+\frac{\sqrt{b^2-4m^2gl}}{2ml}<0$$

**Caso $b^2-4m^2gl<0$:**

Para este mesmo caso, se $b^2-4m^2gl<0$, temos que $b<2m\sqrt{gl}$ e os autovalores serão um par **complexo conjugado no semiplano esquerdo** do plano complexo, pois a parte real de $\lambda$ é $-b/2ml<0$ para quaisquer $b$, $m$ e $l$ positivos, ou seja,

$$\lambda=-\frac{b}{2ml}\pm j\frac{\sqrt{4m^2gl-b^2}}{2ml}$$

Os autovalores da matriz $A$ estão no **semiplano esquerdo** do plano complexo para quaisquer valores de $m$, $b$, $g$ e $l$ estritamente positivos e, portanto, o modelo linearizado é assintoticamente estável. Logo, pelo primeiro método de Lyapunov, **o sistema original é assintoticamente estável em torno de $x_e=(0,0)$**.

> **O atrito resolve a inconclusividade do caso sem atrito:** enquanto no pêndulo ideal (sem atrito) os autovalores ficavam exatamente sobre o eixo imaginário, a introdução de qualquer $b>0$ desloca ambos os autovalores para o semiplano esquerdo — independentemente de o regime ser super-amortecido (raízes reais) ou sub-amortecido (raízes complexas), a conclusão de estabilidade assintótica é a mesma.

### 3.3 Equilíbrio $x_e=(\pi,0)$ — pêndulo invertido, com atrito

Em torno de $x_e=(\pi,0)$, temos que $\cos\pi=-1$. Assim,

$$A=\left[\begin{matrix}0 & 1\\\dfrac{g}{l} & -\dfrac{b}{ml}\end{matrix}\right]$$

e, portanto, a equação característica é dada por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&1\\\frac{g}{l}&-\frac{b}{ml}\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&1\\\frac{g}{l}&-\frac{b}{ml}\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&-1\\-\frac{g}{l}&\lambda+\frac{b}{ml}\end{matrix}\right]\right)=0 \Rightarrow \lambda^2+\frac{b}{ml}\lambda-\frac{g}{l}=0 \Rightarrow \lambda=-\frac{b}{2ml}\pm\frac{\sqrt{b^2+4m^2gl}}{2ml}$$

Neste caso, para quaisquer $b$, $m$, $g$ e $l$ positivos, temos que $b^2+4m^2gl>0$. Logo, como $b<\sqrt{b^2+4m^2gl}$, os autovalores serão **reais e distintos**, de maneira que

$$\lambda=-\frac{b}{2ml}-\frac{\sqrt{b^2+4m^2gl}}{2ml}<0 \qquad \text{e} \qquad \lambda=-\frac{b}{2ml}+\frac{\sqrt{b^2+4m^2gl}}{2ml}>0$$

Como existe um autovalor de $A$ no **semiplano direito** do plano complexo para quaisquer valores de $b$, $m$, $g$ e $l$ estritamente positivos, pelo primeiro método de Lyapunov, **conclui-se que o sistema original é instável em torno de $x_e=(\pi,0)$**.

> **O atrito não estabiliza o equilíbrio invertido:** mesmo com dissipação de energia, o pêndulo invertido continua instável — resultado coerente com a física, já que o atrito dissipa energia (o que ajuda a convergir para o equilíbrio "para baixo"), mas não altera a natureza intrinsecamente instável do ponto de equilíbrio "para cima".

---

## 4. Segundo método de Lyapunov

### 4.1 Ideia central

O segundo método de Lyapunov também é conhecido como **método direto** e é baseado no conceito de **energia** no sistema.

### 4.2 Exemplo — pêndulo simples com atrito (energia)

Considere o pêndulo simples de haste rígida com atrito descrito anteriormente. As energias cinética e potencial gravitacional são dadas, respectivamente, por

$$E_c=\frac{1}{2}mv^2(t)=\frac{1}{2}m(l\dot{\theta}(t))^2=\frac{1}{2}ml^2\dot{\theta}^2(t) \qquad \text{e} \qquad E_p=mgh(t)=mgl(1-\cos\theta(t))$$

de maneira que a energia total do sistema é dada por

$$E_T(t)=E_c+E_p=\frac{1}{2}ml^2\dot{\theta}^2(t)+mgl-mgl\cos\theta(t)$$

e é **positiva** para quaisquer valores de $\theta(t)$ e $\dot{\theta}(t)$. A taxa de variação da energia no sistema é dada por

$$\dot{E}_T(t) = \frac{1}{2}ml^22\dot{\theta}(t)\ddot{\theta}(t)+mgl\dot{\theta}(t)\text{sen}\,\theta(t)$$

$$= ml^2\dot{\theta}(t)\underbrace{\left(-\frac{g}{l}\text{sen}\,\theta(t)-\frac{b}{ml}\dot{\theta}(t)\right)}_{\ddot{\theta}(t)}+mgl\dot{\theta}(t)\text{sen}\,\theta(t)$$

$$= -mgl\dot{\theta}(t)\text{sen}\,\theta(t)-bl\dot{\theta}^2(t)+mgl\dot{\theta}(t)\text{sen}\,\theta(t)$$

$$= -bl\dot{\theta}^2(t)<0$$

e é **negativa** para quaisquer valores de $\theta(t)$ e $\dot{\theta}(t)$ (não nulos). Assim, as trajetórias de estado convergem para o ponto de equilíbrio $x_e=(0,0)$ para quaisquer condições iniciais $x_0$.

> **A energia mecânica do pêndulo é uma candidata natural a função de Lyapunov:** ela é sempre positiva (exceto no equilíbrio) e sua taxa de variação é sempre negativa (pois o atrito dissipa energia continuamente) — exatamente os dois ingredientes que o Teorema 0.2 exige para garantir estabilidade assintótica, **sem que seja necessário resolver a equação diferencial não linear**.

### 4.3 Exemplo — sistema massa-mola-amortecedor (energia)

A dinâmica do sistema massa-mola-amortecedor, para entrada nula, é dada por

$$\ddot{w}(t)=-\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)$$

As energias cinética e potencial elástica são dadas, respectivamente, por

$$E_c(t)=\frac{1}{2}m\dot{w}^2(t) \qquad \text{e} \qquad E_p(t)=\frac{1}{2}kw^2(t)$$

de maneira que a energia total do sistema é dada por

$$E(t)=\frac{1}{2}m\dot{w}^2(t)+\frac{1}{2}kw^2(t)>0$$

e é **positiva** para quaisquer valores de $w(t)$ e $\dot{w}(t)$. A taxa de variação da energia no sistema é dada por

$$\dot{E}(t) = \frac{1}{2}m2\dot{w}(t)\ddot{w}(t)+\frac{1}{2}k2w(t)\dot{w}(t)$$

$$= m\dot{w}(t)\underbrace{\left(-\frac{k}{m}w(t)-\frac{b}{m}\dot{w}(t)\right)}_{\ddot{w}(t)}+kw(t)\dot{w}(t)$$

$$= -kw(t)\dot{w}(t)-b\dot{w}^2(t)+kw(t)\dot{w}(t)$$

$$= -b\dot{w}^2(t)<0$$

e é **negativa** para quaisquer valores de $w(t)$ e $\dot{w}(t)$ (não nulos). Assim, as trajetórias de estado convergem para o ponto de equilíbrio $x_e=(0,0)$ para quaisquer condições iniciais $x_0$.

> Mesma estrutura de raciocínio do pêndulo com atrito: a energia mecânica do sistema massa-mola-amortecedor serve diretamente como função de Lyapunov, e sua derivada negativa confirma a estabilidade assintótica **sem** exigir a solução explícita da equação diferencial — uma vantagem central do método direto, especialmente relevante para sistemas não lineares onde a solução analítica pode nem existir.

### 4.4 Teorema da estabilidade de Lyapunov

> **Teorema 0.2 (Teorema da estabilidade de Lyapunov)** Considere $x_e=0$ o ponto de equilíbrio de $\dot{x}=f(x)$ e $\mathcal{D}\subset\mathbb{R}^n$ um domínio contendo $x_e=0$. Considere também $V:\mathcal{D}\to\mathbb{R}$ uma função continuamente diferenciável, de maneira que
>
> $$V(0)=0 \qquad \text{e} \qquad V(x)>0 \;\;\text{em}\;\; \mathcal{D}-\{0\} \qquad (1)$$
>
> e também, que
>
> $$\dot{V}(x)\leq0 \;\;\text{em}\;\; \mathcal{D} \qquad (2)$$
>
> Então, $x_e=0$ é **estável**. Além disso, se
>
> $$\dot{V}(x)<0 \;\;\text{em}\;\; \mathcal{D}-\{0\} \qquad (3)$$
>
> então $x_e=0$ é **assintoticamente estável**.

Uma função continuamente diferenciável $V(x)$ que satisfaça (1) e (2) é chamada de **função de Lyapunov**. A superfície $V(x)=c$, para algum $c>0$, é chamada de **superfície de Lyapunov**.

> **Interpretação geométrica:** $V(x)$ funciona como uma medida generalizada de "energia" ou "distância" ao equilíbrio. As condições do teorema garantem que essa energia generalizada nunca aumenta ($\dot V(x)\leq0$) — ou, no caso da estabilidade assintótica, sempre diminui estritamente ($\dot V(x)<0$) — forçando o estado a permanecer preso em superfícies de Lyapunov cada vez menores, convergindo para $x_e=0$.

---

## 5. Síntese geral

### 5.1 Primeiro método (indireto/linearização) vs. segundo método (direto/energia)

| | Primeiro método | Segundo método |
|---|---|---|
| Base | Linearização (série de Taylor) + autovalores de $A$ | Função de Lyapunov $V(x)$ (tipicamente, energia) |
| Alcance | Estabilidade **local**, apenas nas vizinhanças de $x_e$ | Pode fornecer conclusões sobre uma região maior (dependendo de $\mathcal{D}$) |
| Quando é conclusivo | Sempre que nenhum autovalor de $A$ estiver sobre o eixo imaginário | Sempre que se encontrar uma função $V(x)$ válida — não há garantia geral de que exista uma "receita" para achá-la |
| Limitação principal | Inconclusivo quando há autovalor(es) com parte real nula (caso de fronteira) | Não há um método sistemático único para construir $V(x)$ em todos os casos |

### 5.2 O que os exemplos do pêndulo demonstram

1. **Sem atrito, em $x_e=(0,0)$:** autovalores puramente imaginários — o primeiro método é **inconclusivo**, embora fisicamente o pêndulo apenas oscile (nem convirja, nem divirja).
2. **Sem atrito, em $x_e=(\pi,0)$:** um autovalor real positivo — **instável**, coerente com a intuição física do pêndulo invertido.
3. **Com atrito, em $x_e=(0,0)$:** ambos os autovalores no semiplano esquerdo — **assintoticamente estável**, resolvendo a inconclusividade do caso sem atrito.
4. **Com atrito, em $x_e=(\pi,0)$:** ainda existe um autovalor no semiplano direito — **instável**; o atrito dissipa energia, mas não muda a natureza instável do equilíbrio invertido.
5. **O segundo método (energia)**, aplicado ao caso com atrito, confirma de forma direta e elegante a estabilidade assintótica em $x_e=(0,0)$, sem precisar resolver a equação diferencial não linear nem calcular autovalores.

### 5.3 Conexão com as aulas anteriores

- Os **autovalores da matriz de estado** (Aulas 1–4) continuam sendo o critério de estabilidade do modelo linearizado no primeiro método de Lyapunov — agora aplicados a sistemas **não lineares**, via linearização em torno de um ponto de equilíbrio.
- As **definições de estabilidade de Lyapunov** (estável, assintoticamente estável, instável), apresentadas na Aula 1, são formalizadas aqui em termos rigorosos através dos Teoremas 0.1 e 0.2.
- O conceito de **energia dissipada** pelo amortecedor, já explorado na Aula 5 (ressonância em sistemas amortecidos), reaparece aqui como a própria função de Lyapunov que certifica a estabilidade assintótica.

---

## Referências

- OGATA, K. *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- KHALIL, H. K. *Nonlinear Systems*. 3rd ed. Prentice Hall, 2002.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 6*. Slides de aula, UFABC, 2021.

