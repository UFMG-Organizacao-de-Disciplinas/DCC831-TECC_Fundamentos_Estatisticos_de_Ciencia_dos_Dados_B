# Fundamentos Estatísticos para Ciência de Dados - Professor: Renato Martins Assunção

## Aula 1 - 13/03/2025

O Objetivo do curso é ensinar a base teórica e conceitual de como e por que são usados certos conceitos.

Distribuição Multivariada/Bivariada: Entrar no material do professor para estudar. Também nos vídeos do professor. Não sabendo, não vai valer a pena.

- Distribuição de pontos:
  - 40 pontos: listas de exercícios
  - 60 pontos: provas; umas 3 provas

---

## Regressão e Mínimos quadrados

### Lei de Ohm

- Lei de Ohm: V = R.I
  - A inclinação da reta de $I = V/R$ é a resistência ($1/R$)

#### Problema: estimar R

[Lembrar ele de corrigir o slide 10]

Na prática, os valores coletados não ficam diretamente associados à reta, então acaba-se gerando uma nova reta aproximada que é aproximadamente o esperado.

Ou seja: $I \approx (1/R) V$ ou $I = (1/R) V + \epsilon$

A reta então é: $I = \beta_0 + \beta_1 V_k + \epsilon$, onde o $\epsilon$ é o erro e o $\beta_0$ é a intercessão da reta gerada pelo erro. O $\beta_1$ é a inclinação da reta, ou seja, $1/R$.

### Problema de regressão

- Algoritmo que encontre os valores de $\beta_0$ e $\beta_1$ que minimizem o erro.b

### Casos mais realistas

[JV: ele listou vários casos]

[Lembrar ele de corrigir os eixos na descrição do slide 30]

### Resumo

...

[JV: Lembrar ele de corrigir o "beta" no slide 35]

### Tentando encontrar a reta

Resíduo: a diferença no eixo Y entre o valor real e o valor estimado.

### Uma boa reta minimiza  a soma dos $|r_i|$

[Slide 40 e 41, suponho que $f(\beta_0, \beta_1)$ deveria ter uma vírgula]

#### Não é uma boa ideia

Ele explicou que em dado momento teria que ver o mínimo valor da função de valor absoluto, mas ao fazer a derivada, o ponto mínimo não é derivável.

Então, outro critério seria...

### Outro critério: Minimizar o quadrado ${r_i}^2$

Como encontrar um ponto crítico de $f(\beta_0, \beta_1)$? DErive, iguale a zero e resolva:

$$
0 = \frac{\partial f}{\partial \beta_0} [\sum_{i=1}^{n} (y_i - (\beta_0 + \beta_1 x_i))^2]\\
0 = \sum_{i=1}^{n} 2(y_i - (\beta_0 + \beta_1 x_i))(-x_i)\\
$$

$$
0 = \frac{\partial f}{\partial \beta_1} [\sum_{i=1}^{n} (y_i - (\beta_0 + \beta_1 x_i))^2]
$$

### Mínimos Quadrados

Um monte de Equações.

## Predição de preços imobiliários

- Qual o valor de um imóvel?

### Localização

- Dividir a cidade em pequenas áreas.
- Ao invés de usar a localização, usar a renda média das pessoas naquela região.

### Outras caraceterísticas do imóvel

- Ano da cosntrução
- Àrea total
- Número de quartos
- etc.

Imagine 30 características para 1500 apartamentos.

### Visão matricial

- Matriz 1500X30

$$
Y = \begin {pmatrix}
y_1\\
y_2\\
\vdots\\
y_{1500}
\end{pmatrix}
$$

$$
X = \begin {pmatrix}
1 & x_{11} & x_{12} & \cdots & x_{1p}\\
1 & x_{21} & x_{22} & \cdots & x_{2p}\\
\vdots & \vdots & \vdots & \ddots & \vdots\\
1 & x_{n1} & x_{n2} & \cdots & x_{np}
\end{pmatrix}
$$

### Modelo inicial

valor pela área:

$Y = a + b*área$

Melhorando modelo inicial

$Y = a + b*área + c*idade$

Modelo mais complexo: $Y = a + b*área + c*idade + d*quartos + \dots$

- **Pergunta:** nesse modelo, consideramos que todas as variáveis influenciam linearmente, correto? Se alguma delas não influenciasse linearmente, de que forma deveríamos proceder?
  - **Resposta:** Isso seria a **Feature Engineering**. Se a relação não fosse linear, passamos a criar uma equação que representa o seu valor para cada uma das linhas da matriz e calcularíamos com isso, mas deixaria sim de ser linear.

### O problema de forma Matricial

$$
\begin{pmatrix}
  1 \\ 1 \\ \vdots \\ 1 \\ 1 \\
\end{pmatrix}
+ b_0 *
\begin{pmatrix}
  área_1 \\ área_2 \\ \vdots \\ área_{1499} \\ área_{1500} \\
\end{pmatrix}
+ b_1 *
\begin{pmatrix}
  idade_1 \\ idade_2 \\ \vdots \\ idade_{1499} \\ idade_{1500} \\
\end{pmatrix}
\dots
$$

### A solução do problema

- Veremos com mais detalhes mais tarde no curso como resolver este problema.
- Por enquanto entende-se que será um problema de equações lineares.

onde a matriz grandona tem 31 colunas (30 características + 1 (constantes para o b_0)) e 1500 linhas.

$$
Y =
\begin{pmatrix}
  Y_1 \\ Y_2 \\ \vdots \\ Y_{1500} \\
\end{pmatrix}
\approx
\begin{pmatrix}
  1 & área_1 & idade_1 & \dots & salão_1\\
  1 & área_2 & idade_2 & \dots & salão_2\\
  \vdots & \vdots & \vdots & \ddots & \dots \\
  1 & área_{1500} & idade_{1500} & \dots salão_{1500} \\
\end{pmatrix}
*
\begin{pmatrix}
  b_0 \\ b_1 \\ b_2 \\ \vdots \\ b_{30} \\
\end{pmatrix}
$$

Como X não é uma matriz quadrada, não é um sistema linear usual, logo, não tem solução em geral.

[JV: Regressão Linear, Slide 23: "soluç ao" -> "solução"]

Uma forma para ter uma matriz quadrada é multiplicar a transposta de X por X de um lado, e multiplicar por Y do outro. Dessa forma, teremos:

$(X^T * X) * b = X^T * Y \equiv ((31x1500) * (1500x31)) * (31x1) = (31x1500) * (1500x1)$

$(31x31 * 31x1) = 31x1$

## Modelos de Regressão

### Solução: Projeção ortogonal

Ele vai usar a norma de $Y - Xb$ para minimizar o erro.

- Queremos $b^{^} = arg min_b ||T - Xb||^2$

Pesquisar sobre espaço vetorial e sub-espaço vetorial.

## Aula 2

## Aula 3 - 20/03/2025: Não haverá aula. Ele enviará um material para estudarmos
