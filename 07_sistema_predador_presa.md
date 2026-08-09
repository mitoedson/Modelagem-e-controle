# Sistema Predador-Presa

## Índice

1. [Modelagem — equações de Lotka-Volterra](#1-modelagem--equações-de-lotka-volterra)
2. [Pontos de equilíbrio](#2-pontos-de-equilíbrio)
3. [Linearização e estabilidade no equilíbrio $(x_e,y_e)=(0,0)$](#3-linearização-e-estabilidade-no-equilíbrio-x_ey_e00)
4. [Linearização e estabilidade no equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$](#4-linearização-e-estabilidade-no-equilíbrio-x_ey_e-gammadeltaalphabeta)
5. [Trajetórias do sistema não linear](#5-trajetórias-do-sistema-não-linear)
6. [Trajetórias do sistema linearizado em torno de $(\gamma/\delta,\alpha/\beta)$](#6-trajetórias-do-sistema-linearizado-em-torno-de-gammadeltaalphabeta)
7. [Solução aproximada e interpretação física](#7-solução-aproximada-e-interpretação-física)
8. [Exemplo numérico — modelo de Lotka-Volterra puro](#8-exemplo-numérico--modelo-de-lotka-volterra-puro)
9. [Modelo com crescimento logístico da presa](#9-modelo-com-crescimento-logístico-da-presa)
10. [Modelo com agente nocivo (inseticida)](#10-modelo-com-agente-nocivo-inseticida)

---

## 1. Modelagem — equações de Lotka-Volterra

Considere a situação na qual uma espécie, o **predador**, alimenta-se de outra espécie, a **presa**, que por sua vez, vive de outra fonte de alimento.

Vamos indicar por $x(t)$ e $y(t)$, respectivamente, as populações de presas e predadores, em um instante de tempo $t$.

Ao se construir o modelo da interação entre as duas espécies, são consideradas as seguintes hipóteses:

**Hipótese 1.** Na ausência de predadores, a população de presas cresce a uma taxa proporcional à população presente, ou seja, quando $y(t)=0$,

$$\dot{x}(t)=\alpha x(t)$$

sendo que $\alpha>0$ é a taxa de crescimento da população de presas.

**Hipótese 2.** Na ausência de presas, a população de predadores diminui até desaparecer a uma taxa proporcional à população presente, ou seja, quando $x(t)=0$,

$$\dot{y}(t)=-\gamma y(t)$$

sendo que $\gamma>0$ é a taxa de mortalidade da população de predadores.

**Hipótese 3.** O número de encontros do predador com a presa é proporcional ao produto das respectivas populações. Cada encontro tende a promover o crescimento da população de predadores e inibir o crescimento da população de presas.

Assim, a taxa de crescimento da população de predadores é acrescida por uma parcela na forma

$$\delta x(t)y(t)$$

enquanto que a taxa de crescimento da população de presas é diminuída por uma parcela

$$-\beta x(t)y(t)$$

ou seja, $\beta>0$ e $\delta>0$ são medidas dos efeitos da interação entre as duas espécies.

Em consequência destas hipóteses, formula-se o seguinte sistema de equações diferenciais **não lineares** para descrever o modelo predador-presa:

$$\dot{x}(t) = \alpha x(t)-\beta x(t)y(t) \qquad (1)$$
$$\dot{y}(t) = -\gamma y(t)+\delta x(t)y(t) \qquad (2)$$

Estas equações são conhecidas como **equações de Lotka-Volterra**. Elas foram desenvolvidas pelo biofísico ucraniano *Alfred Lotka* e pelo matemático italiano *Vito Volterra*.

> O termo de acoplamento $x(t)y(t)$ é o que torna o sistema **não linear** — sem ele, as equações (1) e (2) seriam duas equações de primeira ordem desacopladas, cada uma descrevendo um crescimento (ou decaimento) exponencial simples.

---

## 2. Pontos de equilíbrio

As condições de equilíbrio do sistema são $\dot{x}(t)=0$ e $\dot{y}(t)=0$. Portanto,

$$\alpha x(t)-\beta x(t)y(t)=x(t)(\alpha-\beta y(t))=0$$

e

$$-\gamma y(t)+\delta x(t)y(t)=y(t)(-\gamma+\delta x(t))=0$$

Assim, $x(t)=0$ ou

$$\alpha-\beta y(t)=0 \Rightarrow y(t)=\frac{\alpha}{\beta}$$

e $y(t)=0$ ou

$$-\gamma+\delta x(t)=0 \Rightarrow x(t)=\frac{\gamma}{\delta}$$

Logo, existem **dois pontos de equilíbrio**: $(x_e,y_e)=(0,0)$ (extinção de ambas as espécies) e $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$. O vetor de estado é definido como $\boldsymbol{x}(t)=[x(t)\;y(t)]^T$.

> Os dois pontos de equilíbrio têm interpretações físicas bem distintas: $(0,0)$ é o equilíbrio "trivial" (nenhuma das duas espécies existe — e, na ausência de uma, a outra não teria como se sustentar de qualquer forma, no caso do predador), enquanto $(\gamma/\delta,\alpha/\beta)$ é o equilíbrio de **coexistência**, no qual as populações de presas e predadores se equilibram mutuamente.

---

## 3. Linearização e estabilidade no equilíbrio $(x_e,y_e)=(0,0)$

Linearizando o sistema descrito pelas equações (1) e (2) em torno do ponto de equilíbrio $(x_e,y_e)=(0,0)$, obtém-se duas equações diferenciais lineares de primeira ordem

$$\dot{x}(t) = \alpha x(t)$$
$$\dot{y}(t) = -\gamma y(t)$$

pois a matriz de estado é dada por

$$A=\left.\frac{\partial f(t,\boldsymbol{x})}{\partial\boldsymbol{x}}\right|_{x_e=0,\,y_e=0} = \left[\begin{matrix}\alpha-\beta y(t) & -\beta x(t)\\\delta y(t) & -\gamma+\delta x(t)\end{matrix}\right]_{x_e=0,\,y_e=0} = \left[\begin{matrix}\alpha & 0\\0 & -\gamma\end{matrix}\right]$$

A equação característica associada é dada por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}\alpha&0\\0&-\gamma\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}\alpha&0\\0&-\gamma\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda-\alpha&0\\0&\lambda+\gamma\end{matrix}\right]\right)=0 \Rightarrow (\lambda-\alpha)(\lambda+\gamma)=0$$

tendo como raízes $\boxed{\lambda=\alpha>0}$ e $\boxed{\lambda=-\gamma<0}$.

Os autovalores de $A$ são **reais e distintos**, com um autovalor no semiplano direito do plano complexo. Portanto, pelo primeiro método de Lyapunov, **o sistema descrito pelas equações (1) e (2) é instável no ponto de equilíbrio $(x_e,y_e)=(0,0)$**.

> Resultado coerente com a intuição biológica: partindo de populações pequenas mas não nulas, a presa (na ausência de predadores suficientes) cresce exponencialmente segundo $\dot x=\alpha x$ — o sistema se afasta da extinção mútua em vez de convergir para ela. O equilíbrio de "extinção de ambas as espécies" é, portanto, instável.

---

## 4. Linearização e estabilidade no equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$

Linearizando o sistema descrito pelas equações (1) e (2) em torno do ponto de equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$, obtém-se duas equações diferenciais lineares de primeira ordem

$$\dot{x}(t) = -\frac{\beta\gamma}{\delta}y(t)$$
$$\dot{y}(t) = \frac{\alpha\delta}{\beta}x(t)$$

pois a matriz de estado é dada por

$$A=\left.\frac{\partial f(t,\boldsymbol{x})}{\partial\boldsymbol{x}}\right|_{x_e=\gamma/\delta,\,y_e=\alpha/\beta} = \left[\begin{matrix}\alpha-\beta y(t) & -\beta x(t)\\\delta y(t) & -\gamma+\delta x(t)\end{matrix}\right]_{x_e=\gamma/\delta,\,y_e=\alpha/\beta} = \left[\begin{matrix}0 & -\dfrac{\beta\gamma}{\delta}\\[4pt]\dfrac{\alpha\delta}{\beta} & 0\end{matrix}\right]$$

A equação característica associada é dada por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&-\frac{\beta\gamma}{\delta}\\\frac{\alpha\delta}{\beta}&0\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&-\frac{\beta\gamma}{\delta}\\\frac{\alpha\delta}{\beta}&0\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&\frac{\beta\gamma}{\delta}\\-\frac{\alpha\delta}{\beta}&\lambda\end{matrix}\right]\right)=0 \Rightarrow \lambda^2+\frac{\alpha\delta}{\beta}\frac{\beta\gamma}{\delta}=0 \Rightarrow \lambda^2+\alpha\gamma=0 \Rightarrow \lambda^2=-\alpha\gamma \Rightarrow \boxed{\lambda=\pm j\sqrt{\alpha\gamma}}$$

Os autovalores de $A$ são **complexos conjugados puramente imaginários** e, portanto, pelo primeiro método de Lyapunov, **nada pode ser concluído sobre a estabilidade do sistema descrito pelas equações (1) e (2) no ponto de equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$**.

> Exatamente o caso de fronteira já visto na Aula 6 (pêndulo sem atrito): autovalores sobre o eixo imaginário tornam o primeiro método de Lyapunov inconclusivo. Isso motiva a análise direta das trajetórias do sistema, feita nas próximas seções.

---

## 5. Trajetórias do sistema não linear

Entretanto, é possível determinar a equação das trajetórias do sistema descrito pelas equações (1) e (2). Desta forma, dividindo (2) por (1), temos

$$\frac{\dot{y}(t)}{\dot{x}(t)} = \frac{\frac{dy(t)}{dt}}{\frac{dx(t)}{dt}} = \frac{dy(t)}{dt}\frac{dt}{dx(t)} = \frac{dy(t)}{dx(t)} = \frac{-\gamma y(t)+\delta x(t)y(t)}{\alpha x(t)-\beta x(t)y(t)} = \frac{y(t)(-\gamma+\delta x(t))}{x(t)(\alpha-\beta y(t))}$$

que equivale a

$$\frac{\alpha-\beta y(t)}{y(t)}dy(t) = \frac{-\gamma+\delta x(t)}{x(t)}dx(t) \Rightarrow \left(\alpha\frac{1}{y(t)}-\beta\right)dy(t) = \left(-\gamma\frac{1}{x(t)}+\delta\right)dx(t)$$

e, integrando ambos os lados, temos

$$\alpha\int_{y(0)}^{y(t)}\frac{1}{y}dy-\beta\int_{y(0)}^{y(t)}dy = -\gamma\int_{x(0)}^{x(t)}\frac{1}{x}dx+\delta\int_{x(0)}^{x(t)}dx$$

Para $x(0)=0$ e $y(0)=0$, obtém-se

$$\alpha\ln|y(t)|-\beta y(t) = -\gamma\ln|x(t)|+\delta x(t)+C$$

na qual $C$ é uma constante de integração e, como $x(t)\geq0$ e $y(t)\geq0$ para todo $t$, temos que

$$\boxed{\alpha\ln y(t)+\gamma\ln x(t)-\beta y(t)-\delta x(t)=C} \qquad (3)$$

O gráfico da equação (3), para um dado valor de $C$, é uma **curva fechada** ou **ciclo limite**, que circunda o ponto de equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$.

Este ponto de equilíbrio também é um **centro** do sistema não linear formado pelas equações (1) e (2), de maneira que as populações de predadores e presas apresentam **variações cíclicas**.

> A curva fechada é a "assinatura" visual do sistema predador-presa: em vez de convergir a um ponto fixo ou divergir, as populações de presas e predadores oscilam indefinidamente ao longo de uma trajetória fechada no plano $(x,y)$ — um comportamento que nem o critério de estabilidade assintótica nem o de instabilidade descreve adequadamente; daí a inconclusividade do primeiro método de Lyapunov na Seção 4.

---

## 6. Trajetórias do sistema linearizado em torno de $(\gamma/\delta,\alpha/\beta)$

Assim, para o ponto de equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$ e fazendo

$$x(t) = \frac{\gamma}{\delta}+z(t) \qquad (4)$$
$$y(t) = \frac{\alpha}{\beta}+w(t) \qquad (5)$$

obtém-se,

$$z(t) = x(t)-\frac{\gamma}{\delta} \qquad (6)$$
$$w(t) = y(t)-\frac{\alpha}{\beta} \qquad (7)$$

de maneira que $\dot{z}(t)=\dot{x}(t)$ e $\dot{w}(t)=\dot{y}(t)$.

Assim, substituindo (4) e (5) em (1) e (2), obtém-se

$$\dot{z}(t) = \alpha x(t)-\beta x(t)y(t)$$
$$= \alpha\left(\frac{\gamma}{\delta}+z(t)\right)-\beta\left(\frac{\gamma}{\delta}+z(t)\right)\left(\frac{\alpha}{\beta}+w(t)\right)$$
$$= \frac{\alpha\gamma}{\delta}+\alpha z(t)+\left(-\frac{\beta\gamma}{\delta}-\beta z(t)\right)\left(\frac{\alpha}{\beta}+w(t)\right)$$
$$= \frac{\alpha\gamma}{\delta}+\alpha z(t)-\frac{\alpha\gamma}{\delta}-\frac{\beta\gamma}{\delta}w(t)-\alpha z(t)-\beta z(t)w(t)$$
$$= -\frac{\beta\gamma}{\delta}w(t)-\beta z(t)w(t) \qquad (8)$$

e

$$\dot{w}(t) = -\gamma y(t)+\delta x(t)y(t)$$
$$= -\gamma\left(\frac{\alpha}{\beta}+w(t)\right)+\delta\left(\frac{\gamma}{\delta}+z(t)\right)\left(\frac{\alpha}{\beta}+w(t)\right)$$
$$= -\frac{\alpha\gamma}{\beta}-\gamma w(t)+(\gamma+\delta z(t))\left(\frac{\alpha}{\beta}+w(t)\right)$$
$$= -\frac{\alpha\gamma}{\beta}-\gamma w(t)+\frac{\alpha\gamma}{\beta}+\gamma w(t)+\frac{\alpha\delta}{\beta}z(t)+\delta z(t)w(t)$$
$$= \frac{\alpha\delta}{\beta}z(t)+\delta z(t)w(t) \qquad (9)$$

O vetor de estado agora pode ser definido como $\boldsymbol{x}(t)=[z(t)\;w(t)]^T$. Linearizando o sistema descrito pelas equações (8) e (9) em torno de $(z_e,w_e)=(0,0)$, obtém-se duas equações lineares de primeira ordem

$$\dot{z}(t) = -\frac{\beta\gamma}{\delta}w(t) \qquad (10)$$
$$\dot{w}(t) = \frac{\alpha\delta}{\beta}z(t) \qquad (11)$$

pois a matriz de estado é dada por

$$A=\left.\frac{\partial f(t,\boldsymbol{x})}{\partial\boldsymbol{x}}\right|_{z_e=0,\,w_e=0} = \left[\begin{matrix}-\beta w(t) & -\frac{\beta\gamma}{\delta}-\beta z(t)\\\frac{\alpha\delta}{\beta}+\delta w(t) & \delta z(t)\end{matrix}\right]_{z_e=0,\,w_e=0} = \left[\begin{matrix}0 & -\dfrac{\beta\gamma}{\delta}\\[4pt]\dfrac{\alpha\delta}{\beta} & 0\end{matrix}\right]$$

A equação característica associada é dada por

$$\det(\lambda I-A)=0 \Rightarrow \det\left(\lambda\left[\begin{matrix}1&0\\0&1\end{matrix}\right]-\left[\begin{matrix}0&-\frac{\beta\gamma}{\delta}\\\frac{\alpha\delta}{\beta}&0\end{matrix}\right]\right)=0 \Rightarrow \det\left(\left[\begin{matrix}\lambda&0\\0&\lambda\end{matrix}\right]-\left[\begin{matrix}0&-\frac{\beta\gamma}{\delta}\\\frac{\alpha\delta}{\beta}&0\end{matrix}\right]\right)=0$$

$$\Rightarrow \det\left(\left[\begin{matrix}\lambda&\frac{\beta\gamma}{\delta}\\-\frac{\alpha\delta}{\beta}&\lambda\end{matrix}\right]\right)=0 \Rightarrow \lambda^2+\frac{\alpha\delta}{\beta}\frac{\beta\gamma}{\delta}=0 \Rightarrow \lambda^2+\alpha\gamma=0 \Rightarrow \lambda^2=-\alpha\gamma \Rightarrow \boxed{\lambda=\pm j\sqrt{\alpha\gamma}}$$

Os autovalores de $A$ são complexos conjugados puramente imaginários e, portanto, pelo primeiro método de Lyapunov, **nada pode ser concluído sobre a estabilidade do sistema descrito pelas equações (1) e (2) no ponto de equilíbrio $(z_e,w_e)=(0,0)$**.

> Como esperado, a translação de coordenadas $(x,y)\to(z,w)$ apenas move o ponto de equilíbrio para a origem — a matriz $A$ e seus autovalores são **exatamente os mesmos** obtidos na Seção 4. A mudança de variáveis é útil, no entanto, para simplificar a próxima etapa: a determinação explícita das trajetórias elípticas do sistema linearizado.

### 6.1 Trajetórias elípticas do sistema linearizado

É possível mostrar que as trajetórias de estado do sistema linearizado formado por (10) e (11) correspondem a **elipses** com centro em $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$.

Desta forma, dividindo (11) por (10), temos

$$\frac{\dot{w}(t)}{\dot{z}(t)} = \frac{\frac{dw(t)}{dt}}{\frac{dz(t)}{dt}} = \frac{dw(t)}{dt}\frac{dt}{dz(t)} = \frac{dw(t)}{dz(t)} = \frac{\frac{\alpha\delta}{\beta}z(t)}{-\frac{\beta\gamma}{\delta}w(t)}$$

que equivale a

$$-\frac{\beta\gamma}{\delta}w(t)dw(t) = \frac{\alpha\delta}{\beta}z(t)dz(t)$$

e, integrando ambos os lados, temos

$$-\frac{\beta\gamma}{\delta}\int_{w(0)}^{w(t)}w\,dw = \frac{\alpha\delta}{\beta}\int_{z(0)}^{z(t)}z\,dz$$

Para $z(0)=0$ e $w(0)=0$, obtém-se

$$\boxed{\frac{\alpha\delta}{2\beta}z^2(t)+\frac{\beta\gamma}{2\delta}w^2(t)=K}$$

que corresponde à equação de uma **elipse**, na qual $K\geq0$ é uma constante de integração.

> A elipse é a versão "exata" (para o sistema linearizado) da curva fechada aproximada obtida na Seção 5 para o sistema não linear original — ambas circundam o ponto de equilíbrio de coexistência, confirmando visualmente que se trata de um **centro**.

---

## 7. Solução aproximada e interpretação física

As variações cíclicas das populações de predadores e presas podem ser analisadas mais detalhadamente quando os desvios em relação ao ponto de equilíbrio $(x^*,y^*)=(\gamma/\delta,\alpha/\beta)$ forem pequenos e o sistema linear formado por (4) e (5) puder ser utilizado.

A solução para o sistema pode ser escrita na forma

$$z(t) = \frac{\gamma}{\delta}k\cos(\sqrt{\alpha\gamma}\,t+\phi) \qquad (12)$$
$$w(t) = \frac{\sqrt{\alpha\gamma}}{\beta}k\,\text{sen}(\sqrt{\alpha\gamma}\,t+\phi) \qquad (13)$$

Isto pode ser verificado através da substituição das equações (12) e (13) em (11) e (10), respectivamente, obtendo-se

$$\dot{z}(t) = -\frac{\beta\gamma}{\delta}w(t) = -\frac{\beta\gamma}{\delta}\frac{\sqrt{\alpha\gamma}}{\beta}k\,\text{sen}(\sqrt{\alpha\gamma}\,t+\phi) = -\frac{\gamma\sqrt{\alpha\gamma}}{\delta}k\,\text{sen}(\sqrt{\alpha\gamma}\,t+\phi)$$

$$\dot{w}(t) = \frac{\alpha\delta}{\beta}z(t) = \frac{\alpha\delta}{\beta}\frac{\gamma}{\delta}k\cos(\sqrt{\alpha\gamma}\,t+\phi) = \frac{\alpha\gamma}{\beta}k\cos(\sqrt{\alpha\gamma}\,t+\phi)$$

que correspondem exatamente às derivadas de (12) e (13).

### 7.1 Solução em termos de $x(t)$ e $y(t)$

Assim, substituindo (12) e (13) em (4) e (5), obtém-se

$$x(t) = \frac{\gamma}{\delta}+z(t) = \frac{\gamma}{\delta}+\frac{\gamma}{\delta}k\cos(\sqrt{\alpha\gamma}\,t+\phi) \qquad (14)$$
$$y(t) = \frac{\alpha}{\beta}+w(t) = \frac{\alpha}{\beta}+\frac{\sqrt{\alpha\gamma}}{\beta}k\,\text{sen}(\sqrt{\alpha\gamma}\,t+\phi) \qquad (15)$$

e as constantes $k$ e $\phi$ podem ser determinadas através das condições iniciais das equações (12) e (13):

$$z(0)=\frac{\gamma}{\delta}k\cos\phi \Rightarrow \cos\phi=\frac{z(0)\delta}{\gamma k}$$

$$w(0)=\frac{\sqrt{\alpha\gamma}}{\beta}k\,\text{sen}\,\phi \Rightarrow \text{sen}\,\phi=\frac{w(0)\beta}{\sqrt{\alpha\gamma}\,k}$$

de maneira que, aplicando a identidade $(\text{sen}\,\phi)^2+(\cos\phi)^2=1$, obtém-se

$$\frac{w^2(0)\beta^2}{\alpha\gamma k^2}+\frac{z^2(0)\delta^2}{\gamma^2k^2}=1 \Rightarrow \frac{1}{k^2}\left(\frac{w^2(0)\beta^2}{\alpha\gamma}+\frac{z^2(0)\delta^2}{\gamma^2}\right)=1 \Rightarrow \boxed{k=\sqrt{\frac{w^2(0)\beta^2}{\alpha\gamma}+\frac{z^2(0)\delta^2}{\gamma^2}}}$$

Pela definição de tangente, temos que

$$\tan\phi=\frac{\text{sen}\,\phi}{\cos\phi}=\frac{\frac{w(0)\beta}{\sqrt{\alpha\gamma}k}}{\frac{z(0)\delta}{\gamma k}}=\frac{w(0)\beta\gamma}{z(0)\sqrt{\alpha\gamma}\,\delta} \Rightarrow \boxed{\phi=\text{tg}^{-1}\left(\frac{w(0)\beta\gamma}{z(0)\sqrt{\alpha\gamma}\,\delta}\right)}$$

Os valores de $z(0)$ e $w(0)$ são determinados a partir de (6) e (7).

### 7.2 Interpretação — período, amplitude e médias

As equações (14) e (15) são boas aproximações para as trajetórias quase elípticas que ficam próximas do ponto de equilíbrio $(x_e,y_e)=(\gamma/\delta,\alpha/\beta)$.

Conclui-se que:

**Período.** As populações de presas e predadores oscilam com período

$$T=\frac{2\pi}{\sqrt{\alpha\gamma}}$$

pois, da equação (15), temos que

$$\text{sen}(\omega t+\phi)=\text{sen}\left(\frac{2\pi}{T}t+\phi\right)=\text{sen}(\sqrt{\alpha\gamma}\,t+\phi)$$

independendo das condições iniciais e estando defasadas de $\pi/2$ (as funções sen e cos são defasadas em $\pi/2$).

**Amplitude.** As amplitudes das oscilações para as populações de presas e predadores são, respectivamente,

$$\tilde{x}=\frac{\gamma}{\delta}k \qquad \text{e} \qquad \tilde{y}=\frac{\sqrt{\alpha\gamma}}{\beta}k$$

dependendo das condições iniciais e dos parâmetros.

**Médias.** As populações médias de presas e predadores sobre um ciclo completo são

$$\bar{x}=\frac{\gamma}{\delta} \qquad \text{e} \qquad \bar{y}=\frac{\alpha}{\beta}$$

respectivamente, coincidindo com as populações no equilíbrio.

> **Observação biológica notável:** independentemente da amplitude das oscilações (que depende das condições iniciais), a população **média** de cada espécie ao longo de um ciclo completo é sempre igual ao valor de equilíbrio $(\gamma/\delta,\alpha/\beta)$ — um resultado conhecido como "princípio de Volterra", historicamente usado para explicar por que a pesca reduzida durante a Primeira Guerra Mundial levou a um aumento relativo na proporção de peixes predadores no Adriático.

---

## 8. Exemplo numérico — modelo de Lotka-Volterra puro

Considere o sistema predador-presa descrito pelas equações (1) e (2), no qual $\alpha=1{,}000$, $\beta=0{,}025$, $\gamma=1{,}200$ e $\delta=0{,}015$. As condições iniciais são $x(0)=100$ e $y(0)=20$. O ponto de equilíbrio ocorre em $(x_e,y_e)=(80,40)$.

> **Figura 1** — população de presas (contínuo) e de predadores (tracejado) em função do tempo: apresenta comportamento **periódico**, com um período $T=5{,}74$ anos, exatamente como previsto pela fórmula $T=2\pi/\sqrt{\alpha\gamma}$ da Seção 7.

**Figura 2** — plano de fase para este sistema, para várias condições iniciais: as trajetórias no plano de fase são **curvas fechadas** que circundam o ponto de equilíbrio $(80,40)$, percorridas no sentido **anti-horário** — exatamente o comportamento de "centro" previsto teoricamente na Seção 5 (equação (3)) e na Seção 6 (aproximação elíptica).

> Note que, quanto mais afastada a condição inicial do ponto de equilíbrio, mais a trajetória se afasta da forma elíptica "ideal" (válida apenas para pequenos desvios) e assume um formato mais alongado/assimétrico — consistente com a curva de nível exata da equação (3), que só se aproxima de uma elipse perto do centro.

---

## 9. Modelo com crescimento logístico da presa

### 9.1 Motivação e modificação do modelo

Uma crítica às equações de Lotka-Volterra é que, na ausência de predadores, a população de presas **cresce ilimitadamente**.

Pode-se corrigir este fato, sem perda de generalidade na análise feita anteriormente, introduzindo um efeito de **inibição natural** que uma população muito grande teria sobre a sua taxa de crescimento.

A equação (1) pode ser modificada de modo que, na ausência do predador, ou seja $y(t)=0$, ela seja reduzida a uma equação **logística** em $x(t)$, de maneira que

$$\dot{x}(t) = \alpha x(t)-\epsilon x^2(t)-\beta x(t)y(t)$$
$$\dot{y}(t) = -\gamma y(t)+\delta x(t)y(t)$$

na qual $\alpha,\beta,\gamma,\delta$ e $\epsilon$ são constantes estritamente positivas e $\alpha/\epsilon\gg\gamma/\beta$.

A constante $\epsilon$ é a **taxa de crescimento intrínseco** da população de presas, dada por $\epsilon=\alpha/k$, na qual $k$ é a **capacidade de suporte ambiental** da população de presas.

> Sem predadores ($y=0$), a equação se reduz a $\dot x=\alpha x-\epsilon x^2$ — a clássica equação logística, cuja solução satura em $x=\alpha/\epsilon=k$ em vez de crescer exponencialmente. É essa saturação que corrige a crítica original ao modelo de Lotka-Volterra puro.

### 9.2 Novo ponto de equilíbrio

As condições de equilíbrio do sistema são $\dot{x}(t)=0$ e $\dot{y}(t)=0$. Portanto,

$$\alpha x(t)-\epsilon x^2(t)-\beta x(t)y(t)=x(t)(\alpha-\epsilon x(t)-\beta y(t))=0$$

e

$$-\gamma y(t)+\delta x(t)y(t)=y(t)(-\gamma+\delta x(t))=0$$

Assim, $y(t)=0$ ou

$$-\gamma+\delta x(t)=0 \Rightarrow x(t)=\frac{\gamma}{\delta}$$

e $x(t)=0$ ou

$$\alpha-\epsilon x(t)-\beta y(t)=0 \Rightarrow y(t)=\frac{\alpha}{\beta}-\frac{\epsilon}{\beta}x(t) \Rightarrow y(t)=\frac{\alpha}{\beta}-\frac{\epsilon\gamma}{\beta\delta}$$

Logo, o ponto de equilíbrio

$$(x_e,y_e)=\left(\frac{\gamma}{\delta},\frac{\alpha}{\beta}\right)$$

se desloca para

$$\boxed{(x_e,y_e)=\left(\frac{\gamma}{\delta},\frac{\alpha}{\beta}-\frac{\epsilon\gamma}{\beta\delta}\right)}$$

que é **assintoticamente estável**.

> **Diferença qualitativa fundamental em relação ao modelo puro:** enquanto no modelo de Lotka-Volterra original o ponto de equilíbrio de coexistência era um **centro** (trajetórias em ciclos fechados, sem convergência), a introdução do termo logístico o transforma em um ponto **assintoticamente estável** — as trajetórias agora convergem para o equilíbrio, tipicamente em espiral. Além disso, note que a coordenada $x_e=\gamma/\delta$ (população de presas no equilíbrio) **não muda**; apenas $y_e$ (população de predadores) diminui, de $\alpha/\beta$ para $\alpha/\beta-\epsilon\gamma/(\beta\delta)$.

### 9.3 Comportamento no tempo e no plano de fase

A Figura 3 apresenta a variação das populações em função do tempo com as mesmas condições iniciais para $k=400$ e $\epsilon=0{,}0025$. O ponto de equilíbrio se deslocou de $(x_e,y_e)=(80,40)$ para $(x_e,y_e)=(80,32)$.

> **Figura 3** — populações de presas (contínuo) e predadores (tracejado) em função do tempo: as oscilações agora são **amortecidas**, convergindo suavemente para o novo ponto de equilíbrio $(80,32)$ — contraste direto com o comportamento estritamente periódico da Figura 1.

A Figura 4 mostra o plano de fase.

> **Figura 4** — plano de fase do sistema predador-presa com crescimento logístico: a trajetória é uma **espiral convergente** que se enrola em torno do novo ponto de equilíbrio $(80,32)$ — a assinatura visual clássica de um **foco estável** (autovalores complexos conjugados com parte real negativa), em contraste com as curvas fechadas (centro) da Figura 2.

---

## 10. Modelo com agente nocivo (inseticida)

### 10.1 Motivação e modificação do modelo

Suponha que se empregue um inseticida com o objetivo de reduzir a população de insetos e que este inseticida também seja tóxico para os predadores, matando-os a taxas proporcionais às respectivas populações.

Esta situação pode ser modelada matematicamente através da seguinte modificação nas equações (1) e (2), de maneira que

$$\dot{x}(t) = \alpha x(t)-\beta x(t)y(t)-\xi x(t)$$
$$\dot{y}(t) = -\gamma y(t)+\delta x(t)y(t)-\pi y(t)$$

na qual $\xi>0$ e $\pi>0$ representam a ação de um agente nocivo para ambas as espécies.

As condições de equilíbrio do sistema são $\dot{x}(t)=0$ e $\dot{y}(t)=0$. Assim,

$$\alpha x(t)-\beta x(t)y(t)-\xi x(t)=x(t)(\alpha-\beta y(t)-\xi)=0$$

e

$$-\gamma y(t)+\delta x(t)y(t)-\pi y(t)=y(t)(-\gamma+\delta x(t)-\pi)=0$$

### 10.2 Novo ponto de equilíbrio

Assim, $x(t)=0$ ou

$$\alpha-\beta y(t)-\xi=0 \Rightarrow y(t)=\frac{\alpha-\xi}{\beta}$$

e $y(t)=0$ ou

$$-\gamma+\delta x(t)-\pi=0 \Rightarrow x(t)=\frac{\gamma+\pi}{\delta}$$

Logo, o ponto de equilíbrio

$$(x_e,y_e)=\left(\frac{\gamma}{\delta},\frac{\alpha}{\beta}\right)$$

se desloca para

$$\boxed{(x_e,y_e)=\left(\frac{\gamma+\pi}{\delta},\frac{\alpha-\xi}{\beta}\right)}$$

que é **assintoticamente estável**.

> **O paradoxo do inseticida:** note que o inseticida tem um efeito nocivo maior sobre a população de insetos (presas) do que sobre o seu predador natural, sendo, portanto, **seletivo**, ou seja $\xi>\pi$. Ainda assim, o ponto de equilíbrio da população de **insetos aumenta** (de $\gamma/\delta$ para $(\gamma+\pi)/\delta$) e o ponto de equilíbrio da população de **predadores diminui** (de $\alpha/\beta$ para $(\alpha-\xi)/\beta$)! Esse é um resultado contraintuitivo conhecido na ecologia como **princípio de Volterra**: eliminar indiscriminadamente presas e predadores tende a favorecer, em termos relativos, a população de presas — pois reduz a pressão de predação mais do que reduz a própria população de presas.

### 10.3 Comportamento no tempo e no plano de fase

A Figura 5 apresenta a variação das populações em função do tempo com as mesmas condições iniciais para $\xi=0{,}3$ e $\pi=0{,}1$. O ponto de equilíbrio se deslocou de $(x_e,y_e)=(80,40)$ para $(x_e,y_e)=(87,19)$.

> **Figura 5** — populações de presas (contínuo) e predadores (tracejado) em função do tempo com agente nocivo: assim como no modelo logístico, as oscilações são **amortecidas**, mas agora convergindo para um equilíbrio com **mais** presas (87, contra 80 originalmente) e **menos** predadores (19, contra 40 originalmente) — confirmação numérica direta do princípio de Volterra discutido acima.

A Figura 6 mostra o plano de fase.

> **Figura 6** — plano de fase do sistema predador-presa com agente nocivo: novamente uma **espiral convergente**, agora em torno do ponto de equilíbrio deslocado $(87,19)$ — o mesmo padrão qualitativo de foco estável observado no modelo logístico (Figura 4), embora obtido por um mecanismo físico completamente diferente (mortalidade induzida por agente externo, em vez de limitação de recursos).

---

## Referências

- ODUM, E. *Fundamentals of Ecology*. 3rd ed. Saunders, 1971.
- BOYCE, W. E.; DIPRIMA, R. C. *Elementary Differential Equations and Boundary Value Problems*. 8th ed. John Wiley & Sons Inc., 2005.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 7*. Slides de aula, UFABC, 2021.

