# Clase 1

18-03

## Preeliminar
- $\Gamma$: alfabeto
- $\Gamma^*$: conjunto de todas las palabras formadas sobre $\Gamma$
- $\epsilon$: es la palabra vacía ($\epsilon \in \Gamma^*$)
- $\sigma \in \Gamma^*,|\sigma| \text{ es la longitud de } \sigma \text{ (cantidad de letras)}$
- $\Gamma^k \text{ son todas las palabras/tuplas de longitud k del alfabeto } \Gamma$
- Concatenación: $\sigma \tau \text{ para } \sigma, \tau \in \Gamma^*$
- Indexación: $\sigma \in \Gamma^*, i \in \{ 0, ..., |\sigma| -1 \} \implies \sigma(i) \text{ es la (i+1)-ésima letra de }\sigma$

## Representaciones de objetos en binario
- Fijamos $\Gamma = \{ 0, 1\}$
- Buscamos representar objetos (numeros, grafos, etc) en binario
- Trabajar con métodos de transformación.

**Notación**: 
- $[n]$ es la representación de $n$ en binario.
- $|n| = ⌈ log n ⌉ $ es el tamaño de $[n]$. 

Ejemplo:
- $[0] = 0, [1] = 1, [2]=10$ 
- $|0| = 1, |1| = 1, |2| = 2$

### Representaciones autodelimitantes

Vale para $\Gamma$ finitos. En este caso asumimos $\Gamma = \{ 0, 1\}$

#### **Definición: Codificación autodelimitante de cadenas:**

Para $\sigma = b_1b_2..b_n, (b_i \in \Gamma)$, definimos $\langle \sigma \rangle = b_1b_1 b_2b_2 ... b_nb_n10$. $\langle \sigma \rangle$ es autodelimitante y el 10 marca el final.

Ejemplos:
- $\langle 101 \rangle = 11 00 11 10$
- $\langle \epsilon \rangle = 10$

#### Representaciones de listas, tuplas, conjuntos
Codificamos la lista $L=\sigma_1,...,\sigma_n (\sigma_i \in \Gamma^*)$ como:
$$\langle L \rangle = \langle \sigma_1 \rangle \langle \sigma_2 \rangle ... \langle \sigma_n \rangle 01$$

Ejemplos:
- $\langle \empty \rangle = 01$
- $\langle 11, 100, 0001 \rangle = \langle 11 \rangle \langle 100 \rangle \langle 0001 \rangle= 111110 11000010 0000001110 01$

#### Representaciones de otros objetos
La misma notación $\langle X \rangle$ se usará para otros objetos matemáticos $X$ a veces sin especificar su representación formal. Ej: Grafos, Digrafos, Matrices, etc.

#### Representaciones de tuplas de objetos
Sup. siempre cada objeto $O$ tiene una codificación razonable $\langle O \rangle$ en binario.

*Libertades de notación:*
- $\langle \langle O_1 \rangle, ... \langle O_n \rangle \rangle = \langle O_1, ...,  O_n\rangle$ 
- $|\langle O \rangle| = |O|$

## Problemas de decisión

Los problemas de decision se formalizan como funciones booleanas $f: \{ 0, 1\}^* \rightarrow \{ 0, 1\}$.

Toda funcion booleana representa un lenguaje $\mathbb{L}(f) = \{ x: f(x) = 1 \} \subset \{ 0, 1\}^*$ y viceversa: todo lenguaje puede representarse por 

$\mathbb{x}_\mathbb{L}(x) = \begin{cases} 1 & x \in \mathbb{L} \\ 0 & cc\end{cases}$

## Máquinas de Turing

### 3 cintas
Una MT de 3 cintas tiene:
- 1 cinta de entrada
- 1 cintas de trabajo
- 1 cinta de salida

Se define como una tripla $(\Sigma, Q, \delta)$ con:
- $Q$ el conjunto finito de estados
> - $q_0 \in Q$ estado inicial
> - $q_f \in Q$ estado final

- $\Sigma$ el alfabeto:
> - $▷ \in \Sigma$: comienzo de la cinta
> - $□ \in \Sigma$: blanco
> El alfabeto estandar es $\Sigma = \{ 0, 1, ▷, □ \}$

- $\delta : Q \times \Sigma \times \Sigma \rightarrow \{ L, R, S \} \times \Sigma \times \{ L, R, S \} \times (\Sigma \cup \{ S \}) \times Q$ la funcion de transición
> - $L$ left
> - $R$ right
> - $S$ stay

#### Restricciones sobre $\delta$
- $\delta(*, ▷, *)$ no puede ser de la forma $(L,*,*,*,*)$
- $\delta(*, *, ▷)$ no puede ser de la forma $(*,*,L,*,*)$
- $\delta(q_f, a, b)$ solo puede ser de la forma $(S,b,S,S,q_f)$

### $k$ cintas
Una MT de $k$ cintas tiene:
- 1 cinta de entrada
- k-2 cintas de trabajo
- 1 cinta de salida

Su funcion de transición es 
$$\delta : Q \times \Sigma^{k-1} \rightarrow \{L,R,S\} \times \Sigma^{k-2} \times \{L,R,S\}^{k-2} \times (\Sigma \cup \{S\})  \times Q$$

## Configuraciones y computos

**Configuración**: Es la fotografia de la maquina en un determinado momento (i.e: configuraciones instantáneas). La función $\delta$ hace transicionar/evolucionar el computo en un paso a partir de una configuración dada $C$. Hay configuraciones iniciales y finales

**Notación**: Fijamos un alfabeto $\Gamma$ y definimos $\Gamma ' = \Gamma \cup \{▷, □\}$. Las máquinas trabajan con $\Gamma'$. Las entradas y salidas son palabras sobre $\Gamma$.

**Cómputo**: Es una secuencia $C_0,..., C_l$ de configuraciones. $l$ es la longitud del computo. $M$ con entrada $x$ termine si existe un computo de $M$ a partir de $x$.