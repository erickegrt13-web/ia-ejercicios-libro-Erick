# Ejercicio 8.1: XOR con una red neuronal

**Enunciado.** Dar los pesos y la estructura de una red con una capa oculta de activación ReLU y salida sigmoide que represente $x_1 \oplus x_2$ (o exclusivo), con verdadero $= 1$ y falso $= 0$.

## Respuesta

Dos neuronas ocultas ReLU y una de salida sigmoide:

```math
h_1 = \mathrm{ReLU}(x_1 - x_2), \qquad h_2 = \mathrm{ReLU}(x_2 - x_1), \qquad y = \sigma(10\,h_1 + 10\,h_2 - 5)
```

En forma matricial, con $h = \mathrm{ReLU}(Wx + b)$ y $y = \sigma(v^\top h + c)$:

```math
W = \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}, \quad
b = \begin{pmatrix} 0 \\ 0 \end{pmatrix}, \quad
v = \begin{pmatrix} 10 \\ 10 \end{pmatrix}, \quad
c = -5
```

## Verificación

| $x_1$ | $x_2$ | $h_1$ | $h_2$ | $z$ | $y = \sigma(z)$ | $x_1 \oplus x_2$ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 0 | 0 | 0 | 0 | −5 | 0.007 | 0 |
| 0 | 1 | 0 | 1 | 5 | 0.993 | 1 |
| 1 | 0 | 1 | 0 | 5 | 0.993 | 1 |
| 1 | 1 | 0 | 0 | −5 | 0.007 | 0 |

## Desarrollo

1. $x_1 \oplus x_2 = (x_1 \land \lnot x_2) \lor (\lnot x_1 \land x_2)$.
2. Si $a, b \in \lbrace 0,1 \rbrace$, entonces $\mathrm{ReLU}(a - b) = a \land \lnot b$, porque $a - b$ solo vale $1$ cuando $a = 1$ y $b = 0$.
3. $h_1$ y $h_2$ nunca valen $1$ a la vez, así que el "o" de los dos es su suma.
4. Para la salida pedimos $z \le -5$ cuando $h_1 + h_2 = 0$ y $z \ge 5$ cuando vale $1$ (criterio del Ejercicio 7.9 del libro). Eso da $c = -5$ y $w = 10$.

## Referencias

- Poole, D. L., y Mackworth, A. K. (2023). *Artificial Intelligence: Foundations of Computational Agents*, 3a. ed., Ejemplo 8.1 y Ejercicios 7.9 y 8.1.
