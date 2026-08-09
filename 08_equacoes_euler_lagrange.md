# Modelagem Matemática de Sistemas Mecânicos através das Equações de Euler-Lagrange

## Índice

1. [Motivação e restrições holonômicas](#1-motivação-e-restrições-holonômicas)
2. [O lagrangiano e as equações de Euler-Lagrange](#2-o-lagrangiano-e-as-equações-de-euler-lagrange)
3. [Equivalência com a segunda lei de Newton](#3-equivalência-com-a-segunda-lei-de-newton)
4. [Exemplo — pêndulo simples com atrito](#4-exemplo--pêndulo-simples-com-atrito)
5. [Síntese geral](#5-síntese-geral)

---

## 1. Motivação e restrições holonômicas

Quando o movimento de um sistema mecânico estiver de alguma maneira restrito, surgem as **forças de restrição**, também denominadas de forças de vínculo ou forças internas. A determinação destas forças pode não ser simples. Sob este aspecto, a formulação lagrangiana é uma alternativa vantajosa, pois ela **não requer** a determinação das forças de restrição para a obtenção das equações do movimento.

As equações de Euler-Lagrange descrevem o movimento de um sistema mecânico sujeito à restrições **holonômicas**, isto é, aquelas que apresentam equações de restrição ligando suas coordenadas generalizadas.

Considere um sistema de $k$ partículas sujeito a $m$ restrições holonômicas. A quantidade de graus de liberdade $n$ é igual à diferença entre a quantidade de graus de liberdade que o sistema teria se não houvessem restrições $p$ menos o número de restrições holonômicas $r$, ou seja,

$$n=p-r$$

A Figura 1 apresenta um pêndulo simples com coordenadas $x$ e $y$ orientadas, respectivamente, nas direções $\hat{i}$ e $\hat{j}$. Ele é composto por uma haste rígida de massa desprezível e comprimento $l$. Em sua extremidade está fixada uma massa pontual $m$, sujeita à aceleração gravitacional $g$ e coeficiente de atrito $b$. Existe uma equação de restrição para o sistema, pelo fato de que $l$ é uma constante, dada por $x^2+y^2=l^2$, ou seja, $r=1$. Se não existisse essa restrição, a massa teria dois graus de liberdade, ou seja, $p=2$. A quantidade de graus de liberdade é $n=p-r=1$ e a coordenada generalizada é $q_1=\theta(t)$.

> **Figura 1 — Pêndulo simples:** mostra a haste de comprimento $l$ formando ângulo $\theta(t)$ com o eixo vertical (eixo $y$), a massa $m$ na extremidade sujeita ao vetor gravidade $\vec g$, o vetor posição $\vec R$ da origem até a massa, e a decomposição do peso $mg$ nas componentes tangencial ($mg\,\text{sen}\,\theta(t)$) e radial ($mg\cos\theta(t)$) em relação à haste. A altura $h$ da massa, medida a partir do ponto mais baixo da trajetória (referência), é usada posteriormente para o cálculo da energia potencial.

> A grande vantagem prática ilustrada aqui: em vez de trabalhar com as duas coordenadas cartesianas $x$ e $y$ sujeitas à restrição $x^2+y^2=l^2$ — o que exigiria lidar explicitamente com a tração na haste (força de restrição) —, a formulação lagrangiana permite descrever o sistema com uma única **coordenada generalizada** $\theta(t)$, que já incorpora a restrição automaticamente.

---

## 2. O lagrangiano e as equações de Euler-Lagrange

Após a escolha de um conjunto de coordenadas generalizadas independentes $q_1,q_2,\ldots,q_n$, para $i=1,\ldots,k$, no qual $n$ é a quantidade de graus de liberdade do sistema mecânico, define-se o **lagrangiano** do sistema mecânico como

$$L=T-V \qquad (1)$$

no qual $T$ é a energia cinética e $V$ é a energia potencial do sistema. O lagrangiano resulta em um sistema de equações diferenciais de ordem $n$.

As **equações de Euler-Lagrange** são expressas como

$$\frac{d}{dt}\left(\frac{\partial L}{\partial\dot{q}_i}\right)-\frac{\partial L}{\partial q_i}=\tau_i \qquad (2)$$

na qual $\tau_i$ é a força generalizada **não conservativa** (torque ou força) na direção da coordenada generalizada independente $q_i$. Uma força não conservativa é aquela que não pode ser obtida por derivação da energia potencial. As forças não conservativas contribuem no lado direito das equações de Euler-Lagrange (2).

O **atrito** é uma força não conservativa, assim como as forças externas aplicadas ao sistema. A força elástica de uma mola é uma força conservativa, pois pode ser obtida derivando-se a energia potencial elástica. A força peso também é uma força conservativa, pois pode ser obtida derivando-se a energia potencial gravitacional.

> **Resumo prático:** forças conservativas (peso, mola) já estão "embutidas" no lagrangiano $L=T-V$, através de $V$. Forças não conservativas (atrito, forças externas de controle) não podem ser derivadas de um potencial e, por isso, entram explicitamente do lado direito da equação (2), como $\tau_i$.

---

## 3. Equivalência com a segunda lei de Newton

As equações de Euler-Lagrange (2) podem ser obtidas a partir da segunda lei de Newton. Considere $x(t)$ como a coordenada generalizada que representa a posição vertical de uma massa $m$ sujeita à aceleração gravitacional $g=-\ddot{x}(t)$.

A força peso $F$ pode ser representada por

$$F=-mg=m\ddot{x}(t)=\frac{d}{dt}(m\dot{x}(t))=\frac{d}{dt}\left(\frac{d}{d\dot{x}(t)}\left(\frac{1}{2}m\dot{x}^2(t)\right)\right)=\frac{d}{dt}\left(\frac{dT}{d\dot{x}(t)}\right) \qquad (3)$$

na qual $T$ é a energia cinética definida como

$$T=\frac{1}{2}m\dot{x}^2(t) \qquad (4)$$

A força peso também pode ser representada por

$$F=-mg=-\frac{d}{dx(t)}\underbrace{(mgx(t))}_{V}=-\frac{dV}{dx(t)} \qquad (5)$$

na qual a energia potencial gravitacional é definida como

$$V=mgx(t) \qquad (6)$$

Substituindo as equações (4) e (6) na equação do lagrangiano (1), temos que

$$L=T-V=\frac{1}{2}m\dot{x}^2(t)-mgx(t) \qquad (7)$$

Da equação (7), temos que

$$\frac{\partial L}{\partial\dot{x}(t)}=m\dot{x}(t)=\frac{dT}{d\dot{x}(t)} \qquad (8)$$

e

$$\frac{\partial L}{\partial x(t)}=-mg=-\frac{dV}{dx(t)}=F \qquad (9)$$

A derivada no tempo da equação (8) resulta na equação (3), pois

$$\frac{d}{dt}\left(\frac{\partial L}{\partial\dot{x}(t)}\right)=m\ddot{x}(t)=\frac{d}{dt}\left(\frac{dT}{d\dot{x}(t)}\right)=F \qquad (10)$$

As equações (9) e (10) representam a força $F$ e, portanto, são equivalentes, de maneira que

$$\frac{d}{dt}\left(\frac{\partial L}{\partial\dot{x}(t)}\right)=\frac{\partial L}{\partial x(t)} \Rightarrow \frac{d}{dt}\left(\frac{\partial L}{\partial\dot{x}(t)}\right)-\frac{\partial L}{\partial x(t)}=0$$

que é a equação de Euler-Lagrange (2) para a coordenada generalizada $x(t)$ na **ausência** de forças não conservativas.

> Esta dedução conecta diretamente o formalismo lagrangiano à mecânica newtoniana já familiar das aulas anteriores: as equações de Euler-Lagrange não são um método "alternativo e desconectado", mas sim uma reformulação matematicamente equivalente da segunda lei de Newton, expressa em termos de energia em vez de forças diretamente.

---

## 4. Exemplo — pêndulo simples com atrito

### 4.1 Modelo obtido via segunda lei de Newton (revisão)

Considere novamente o pêndulo simples ilustrado na Figura 1, composto por uma haste rígida de comprimento $l$ e massa desprezível. Na sua extremidade móvel, existe uma massa $m$ sujeita à aceleração gravitacional $g$ e coeficiente de atrito $b$. O ângulo de rotação $\theta(t)$ é formado entre a haste e o eixo vertical. Pela segunda lei de Newton para o sistema rotacional, temos que $\sum_{i=1}^n\vec{\tau}_i=J\vec{\alpha}$, na qual $\tau$ é o torque, $J=\sum_{j=1}^nm_ir_i^2$ é o momento de inércia e $\alpha$ é a aceleração angular. Os valores de $m$, $g$, $l$ e $b$ são estritamente positivos. Logo,

$$-mgl\,\text{sen}\,\theta(t)-bl\dot{\theta}(t)=ml^2\ddot{\theta}(t) \Rightarrow \ddot{\theta}(t)=-\frac{g}{l}\text{sen}\,\theta(t)-\frac{b}{ml}\dot{\theta}(t) \qquad (11)$$

Este modelo também pode ser obtido através das equações de Euler-Lagrange.

### 4.2 Energia cinética via formulação lagrangiana

O vetor $\vec{R}$ é definido como

$$\vec{R}=l\,\text{sen}\,\theta(t)\,\hat{i}-l\cos\theta(t)\,\hat{j}$$

de maneira que a derivada no tempo é dada por

$$\dot{\vec{R}}=l\dot{\theta}(t)\cos\theta(t)\,\hat{i}+l\dot{\theta}(t)\,\text{sen}\,\theta(t)\,\hat{j}$$

Assim

$$|\dot{\vec{R}}|^2 = [l\dot{\theta}(t)\cos\theta(t)]^2+[l\dot{\theta}(t)\,\text{sen}\,\theta(t)]^2$$
$$= l^2\dot{\theta}^2(t)[\cos\theta(t)]^2+l^2\dot{\theta}^2(t)[\text{sen}\,\theta(t)]^2$$
$$= l^2\dot{\theta}^2(t)\underbrace{\{[\cos\theta(t)]^2+[\text{sen}\,\theta(t)]^2\}}_{=1}$$
$$= l^2\dot{\theta}^2(t)$$

A energia cinética é dada por

$$T=\frac{1}{2}m|\dot{\vec{R}}|^2=\frac{1}{2}ml^2\dot{\theta}^2(t)$$

### 4.3 Energia potencial e lagrangiano

Da Figura 1, temos que $h(t)=l-l\cos\theta(t)$ e, portanto, a energia potencial gravitacional é dada por

$$V=mgh=mg(l-l\cos\theta(t))=mgl-mgl\cos\theta(t)$$

O lagrangiano é dado por

$$L=T-V=\frac{1}{2}ml^2\dot{\theta}^2(t)-mgl+mgl\cos\theta(t)$$

### 4.4 Aplicação das equações de Euler-Lagrange

Temos que

$$\frac{\partial L}{\partial\theta(t)}=-mgl\,\text{sen}\,\theta(t)$$

e

$$\frac{\partial L}{\partial\dot{\theta}(t)}=ml^2\dot{\theta}(t) \Rightarrow \frac{d}{dt}\left(\frac{\partial L}{\partial\dot{\theta}(t)}\right)=ml^2\ddot{\theta}(t)$$

Portanto, da equação de Euler-Lagrange (2) e considerando o torque não conservativo relativo ao atrito, temos que

$$\frac{d}{dt}\left(\frac{\partial L}{\partial\dot{\theta}(t)}\right)-\frac{\partial L}{\partial\theta(t)}=-bl\dot{\theta}(t) \Rightarrow ml^2\ddot{\theta}(t)+mgl\,\text{sen}\,\theta(t)=-bl\dot{\theta}(t)$$

$$\Rightarrow \boxed{\ddot{\theta}(t)=-\frac{g}{l}\text{sen}\,\theta(t)-\frac{b}{ml}\dot{\theta}(t)}$$

que se iguala à equação (11).

> **Confirmação do método:** a equação obtida via formalismo lagrangiano é **idêntica** à equação (11), obtida diretamente pela segunda lei de Newton para sistemas rotacionais — validando o formalismo, mas destacando sua principal vantagem: em nenhum momento foi necessário calcular explicitamente a tração na haste (força de restrição), que seria necessária em uma análise vetorial completa das forças. O torque de atrito $-bl\dot{\theta}(t)$, por ser não conservativo, entrou diretamente como $\tau_i$ do lado direito da equação (2) — não há como derivá-lo de um potencial $V$.

---

## 5. Síntese geral

### 5.1 O procedimento geral do método lagrangiano

1. **Identificar as restrições holonômicas** do sistema e determinar o número de graus de liberdade $n=p-r$.
2. **Escolher coordenadas generalizadas** $q_1,\ldots,q_n$ independentes que descrevam completamente a configuração do sistema, incorporando automaticamente as restrições.
3. **Calcular a energia cinética $T$** e a **energia potencial $V$** em termos das coordenadas generalizadas e suas derivadas.
4. **Formar o lagrangiano** $L=T-V$.
5. **Identificar as forças não conservativas** $\tau_i$ (atrito, forças externas de controle) atuantes em cada coordenada generalizada.
6. **Aplicar a equação de Euler-Lagrange** $\dfrac{d}{dt}\left(\dfrac{\partial L}{\partial\dot q_i}\right)-\dfrac{\partial L}{\partial q_i}=\tau_i$ para cada $i=1,\ldots,n$, obtendo o sistema de equações diferenciais do movimento.

### 5.2 Vantagens sobre a abordagem newtoniana direta

- **Não é necessário calcular forças de restrição** (trações, normais, reações de vínculo) — o formalismo trabalha diretamente com energias escalares.
- **Coordenadas generalizadas** podem ser escolhidas livremente (ângulos, deslocamentos, combinações), desde que independentes e compatíveis com as restrições, tornando o método naturalmente adaptável a sistemas complexos com múltiplos graus de liberdade.
- **Sistematização:** o mesmo procedimento (Seção 5.1) se aplica a qualquer sistema mecânico holonômico, da massa em queda livre (Seção 3) ao pêndulo com atrito (Seção 4), passando por sistemas muito mais complexos, como robôs manipuladores com múltiplos elos.

### 5.3 Conexão com as aulas anteriores

- O **modelo do pêndulo simples com atrito**, já analisado na Aula 6 (estabilidade de Lyapunov) a partir da segunda lei de Newton, é obtido aqui de forma independente pelo formalismo de Euler-Lagrange — os dois caminhos levam à **mesma equação diferencial** (equação 11), reforçando a consistência entre as abordagens.
- A distinção entre **forças conservativas e não conservativas**, central nesta aula, é a mesma distinção usada implicitamente nas Aulas 5 e 6, ao tratar separadamente os termos de rigidez/gravidade (conservativos) e amortecimento/atrito (não conservativos, dissipativos).
- O formalismo lagrangiano apresentado aqui é a base natural para a modelagem de sistemas mecânicos mais complexos (múltiplos graus de liberdade, sistemas robóticos), que tipicamente seguem nas próximas etapas do curso.

---

## Referências

- SPONG, M. S.; VIDYASAGAR, M. *Robot Dynamics and Control*. Wiley, 1989.
- RAO, S. *Vibrações Mecânicas*. 4ª edição. Pearson, 2012.
- LORDELO, A. D. S. *ESTA020-17: Modelagem e Controle — Aula 8*. Slides de aula, UFABC, 2021.

