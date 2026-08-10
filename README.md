# Modelagem e Controle

Material elaborado a partir dos slides de aula, da disciplina **ESTA020-17: Modelagem e Controle**, da Universidade Federal do ABC (UFABC), ministrada pelo Prof. Dr. Alfredo Del Sole Lordelo, com dedução completa das equações, exemplos numéricos resolvidos passo a passo, e conexões explícitas entre os tópicos.

**Objetivo:** aprofundar os conhecimentos de modelagem matemática de sistemas dinâmicos e introduzir conceitos elementares no projeto de controladores no domínio do tempo.

**Ementa:** modelagem matemática de sistemas dinâmicos através de equações diferenciais e no espaço de estados. Análise de estabilidade de sistemas dinâmicos. Princípios de controle de malha aberta e de malha fechada; projeto de controladores elementares no domínio do tempo.


## Estrutura do curso

A disciplina se desenvolve em seis grandes blocos, que se conectam de forma sequencial:

```
┌─────────────────┐   ┌───────────────────┐   ┌──────────────────┐   ┌───────────────────┐   ┌───────────────────┐   ┌───────────────────┐
│ 1. Estabilidade │   │ 2. Comportamento  │   │ 3. Espaço de     │   │ 4. Projeto de     │   │ 5. Ressonância e  │   │ 6. Modelagem via  │
│ segundo Lyapunov│──►│ dinâmico (EDOs de │──►│ estados          │──►│ controladores     │──►│ estabilidade não  │──►│ Euler-Lagrange    │
│ (definições)    │   │ 1ª e 2ª ordem)    │   │ (generalização)  │   │ (PD)              │   │ linear (Lyapunov  │   │ (sistemas         │
│                 │   │                   │   │                  │   │                   │   │ 1º/2º método)     │   │ mecânicos)        │
└─────────────────┘   └───────────────────┘   └──────────────────┘   └───────────────────┘   └───────────────────┘   └───────────────────┘
```

1. **Define-se** o que significa um sistema ser estável (Aula 1).
2. **Aplica-se** essa definição a casos concretos e solúveis — EDOs lineares de 1ª e 2ª ordem, homogêneas e não homogêneas — extraindo especificações de desempenho ($M_p$, $t_s$, $t_r$, $t_p$) (Aulas 1–2).
3. **Generaliza-se** a representação para sistemas de ordem arbitrária, via espaço de estados e autovalores (Aula 3).
4. **Usa-se** tudo isso para projetar controladores que atendam especificações de desempenho desejadas (Aula 4).
5. **Estuda-se** o comportamento em regime de excitação senoidal (ressonância) e formaliza-se a análise de estabilidade para sistemas não lineares, via os métodos direto e indireto de Lyapunov (Aulas 5–6), aplicando-os a um sistema não linear paradigmático — o predador-presa (Aula 7).
6. **Introduz-se** uma formulação alternativa e mais poderosa para obter as equações do movimento de sistemas mecânicos — as equações de Euler-Lagrange —, dispensando o cálculo explícito das forças de restrição (Aula 8).


## Índice dos materiais

| Arquivo | Aula | Conteúdo |
|---|---|---|
| [`01_estabilidade_lyapunov_edo_homogeneas.md`](01_estabilidade_lyapunov_edo_homogeneas.md) | Aula 1 | Estabilidade segundo Lyapunov ($S(\delta)$, $S(\xi)$, estável/assintoticamente estável/instável); EDOs lineares homogêneas de 1ª e 2ª ordem (raízes reais distintas, duplas, complexas conjugadas) |
| [`02_resposta_transitoria_regime_estacionario.md`](02_resposta_transitoria_regime_estacionario.md) | Aula 2 | EDOs lineares não homogêneas de 1ª e 2ª ordem; forma padrão ($\xi$, $\omega_n$); especificações da resposta transitória ($t_d$, $t_r$, $t_p$, $M_p$, $t_s$); resposta ao impulso |
| [`03_modelagem_espaco_de_estados.md`](03_modelagem_espaco_de_estados.md) | Aula 3 | Conceitos de estado, variáveis de estado, espaço de estado; forma matricial $\dot{x}=Ax+Bu$; autovalores como generalização da equação característica; exemplos com sistemas mecânicos de 1 e 2 graus de liberdade |
| [`04_controle_proporcional_derivativo.md`](04_controle_proporcional_derivativo.md) | Aula 4 | Controle proporcional (P) e proporcional-derivativo (PD); erro de regime permanente; projeto de ganhos $k_p$, $k_d$ a partir de especificações de desempenho |
| [`05_ressonancia.md`](05_ressonancia.md) | Aula 5 | Ressonância em sistemas de 2ª ordem não amortecidos e amortecidos; caso limite $\gamma=\omega_n$ via regra de l'Hôpital; frequência de ressonância $\gamma_{ress}=\omega_n\sqrt{1-2\xi^2}$; exemplo massa-mola-amortecedor com resposta em frequência |
| [`06_analise_estabilidade_lyapunov.md`](06_analise_estabilidade_lyapunov.md) | Aula 6 | Primeiro método de Lyapunov (linearização); segundo método de Lyapunov (função de energia); exemplos do pêndulo simples com e sem atrito, nos equilíbrios estável e invertido; teorema da estabilidade de Lyapunov |
| [`07_sistema_predador_presa.md`](07_sistema_predador_presa.md) | Aula 7 | Equações de Lotka-Volterra; pontos de equilíbrio e sua estabilidade; trajetórias em ciclo fechado (centro); extensões com crescimento logístico da presa e com agente nocivo (inseticida) — princípio de Volterra |
| [`08_equacoes_euler_lagrange.md`](08_equacoes_euler_lagrange.md) | Aula 8 | Restrições holonômicas e coordenadas generalizadas; lagrangiano $L=T-V$; equações de Euler-Lagrange; equivalência com a segunda lei de Newton; exemplo completo do pêndulo simples com atrito |


## Conceitos-chave que atravessam todo o curso

- **Ponto de equilíbrio** $x_e$: obtido resolvendo $f(t,x_e)=0$ — é sempre o primeiro passo de qualquer análise, linear ou não linear.
- **Estabilidade assintótica ⟺ parte real negativa**: seja das raízes da equação característica (Aulas 1–2), seja dos autovalores da matriz $A$ (Aula 3), seja dos autovalores do modelo **linearizado** em torno de um ponto de equilíbrio (Aulas 6–7) — o mesmo critério se generaliza ao longo de todo o curso.
- **Forma padrão de 2ª ordem** ($\xi$, $\omega_n$): a "linguagem comum" usada para especificar desempenho (overshoot, tempo de acomodação, frequência de ressonância) e, mais adiante, para projetar controladores.
- **Trajetória no espaço de estados / plano de fase**: a mesma imagem geométrica (Figura 1 da Aula 1) reaparece em planos de fase de sistemas reais (Aula 3), nas respostas de sistemas controlados (Aula 4) e nos ciclos e espirais do sistema predador-presa (Aula 7).
- **Energia como ferramenta de análise**: usada para caracterizar amplitude de oscilação na ressonância (Aula 5), como função de Lyapunov para certificar estabilidade sem resolver a EDO (Aula 6), e como base do lagrangiano $L=T-V$ para obter as próprias equações do movimento (Aula 8).
- **Casos de fronteira (autovalores no eixo imaginário)**: aparecem recorrentemente — no pêndulo sem atrito (Aula 6) e no equilíbrio de coexistência do sistema predador-presa (Aula 7) — como o limite de validade do primeiro método de Lyapunov, motivando ferramentas complementares (segundo método, análise direta de trajetórias).


## Referências bibliográficas

- OGATA, K. *Engenharia de Controle Moderno*. 4ª ed. Pearson & Prentice Hall, 2005.
- BOYCE, W. E.; DIPRIMA, R. C. *Equações Diferenciais Elementares e Problemas de Valores de Contorno*. 8ª ed. LTC, 2006.
- ZILL, D. G. *Equações Diferenciais*. 3ª ed., vol. 1. Pearson Makron Books, 2006.
- ZILL, D. G. *Equações Diferenciais com Aplicações em Modelagem*. Thomson, 2003.
- KHALIL, H. K. *Nonlinear Systems*. 3rd ed. Prentice Hall, 2002.
- ODUM, E. *Fundamentals of Ecology*. 3rd ed. Saunders, 1971.
- SPONG, M. S.; VIDYASAGAR, M. *Robot Dynamics and Control*. Wiley, 1989.
- RAO, S. *Vibrações Mecânicas*. 4ª edição. Pearson, 2012.

