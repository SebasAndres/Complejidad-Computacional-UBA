# Clase 1 — Representaciones en binario e introducción a las Máquinas de Turing

## Preliminares sobre alfabetos y palabras
- $\Gamma$: alfabeto (conjunto finito de símbolos).
- $\Gamma^*$: conjunto de todas las palabras formadas sobre $\Gamma$.
- $\epsilon$: palabra vacía ($\epsilon \in \Gamma^*$).
- Para $\sigma \in \Gamma^*$, $|\sigma|$ es la longitud de $\sigma$ (cantidad de letras).
- $\Gamma^k$ es el conjunto de palabras/tuplas de longitud $k$ sobre $\Gamma$.
- **Concatenación**: $\sigma\tau$ para $\sigma, \tau \in \Gamma^*$.
- **Indexación**: si $\sigma \in \Gamma^*$ e $i \in \{0,\dots,|\sigma|-1\}$, entonces $\sigma(i)$ es la $(i+1)$-ésima letra de $\sigma$.

## Representaciones de objetos en binario
- Fijamos $\Gamma = \{0,1\}$.
- Buscamos representar objetos (números, grafos, tuplas, listas, máquinas, etc.) en binario y poder transformarlos.

**Notación**:
- $[n]$: representación de $n \in \mathbb{N}$ en binario.
- $|n| = \lceil \log n \rceil$: tamaño de $[n]$.

Ejemplos:
- $[0]=0$, $[1]=1$, $[2]=10$.
- $|0|=1$, $|1|=1$, $|2|=2$.

### Representaciones autodelimitantes
Sirven para $\Gamma$ finito. Tomamos $\Gamma = \{0,1\}$.

#### Codificación autodelimitante de cadenas
Para $\sigma = b_1 b_2 \dots b_n$ con $b_i \in \Gamma$, definimos
$$\langle \sigma \rangle = b_1 b_1\, b_2 b_2\, \cdots\, b_n b_n\, 10.$$
$\langle \sigma \rangle$ es autodelimitante; el sufijo `10` marca el final.

Ejemplos:
- $\langle 101 \rangle = 11\,00\,11\,10$.
- $\langle \epsilon \rangle = 10$.

#### Representación de listas/tuplas
Si $L = \sigma_1, \dots, \sigma_n$ con $\sigma_i \in \Gamma^*$:
$$\langle L \rangle = \langle \sigma_1 \rangle \langle \sigma_2 \rangle \cdots \langle \sigma_n \rangle\, 01.$$

Ejemplos:
- $\langle \emptyset \rangle = 01$.
- $\langle 11, 100, 0001 \rangle = 111110\,11000010\,0000001110\,01$.

#### Representación de otros objetos
La misma notación $\langle X \rangle$ se aplica a objetos matemáticos (grafos, dígrafos, matrices, etc.) usualmente sin especificar la representación formal.

#### Tuplas de objetos
Si cada objeto $O_i$ tiene una codificación razonable $\langle O_i \rangle$:
- $\langle \langle O_1 \rangle, \dots, \langle O_n \rangle \rangle = \langle O_1, \dots, O_n \rangle$.
- $|\langle O \rangle| = |O|$ (abuso de notación).

## Problemas de decisión
Se formalizan como funciones booleanas $f: \{0,1\}^* \to \{0,1\}$.

Toda $f$ determina un lenguaje $\mathbb{L}(f) = \{ x : f(x)=1 \} \subseteq \{0,1\}^*$ y, recíprocamente, todo lenguaje $\mathbb{L}$ se representa por su función característica
$$\chi_{\mathbb{L}}(x) = \begin{cases} 1 & x \in \mathbb{L}\\ 0 & \text{c.c.}\end{cases}$$

## Máquinas de Turing

### MT con 3 cintas
Tiene:
- 1 cinta de entrada (solo lectura).
- 1 cinta de trabajo.
- 1 cinta de salida.

Se define como una tripla $(\Sigma, Q, \delta)$ con:
- $Q$: conjunto finito de estados.
  - $q_0 \in Q$: estado inicial.
  - $q_f \in Q$: estado final.
- $\Sigma$: alfabeto, con símbolos distinguidos
  - $\triangleright \in \Sigma$: marca de comienzo de cinta.
  - $\square \in \Sigma$: símbolo blanco.
  - Alfabeto estándar: $\Sigma = \{0, 1, \triangleright, \square\}$.
- Función de transición
  $$\delta: Q \times \Sigma \times \Sigma \to \{L,R,S\} \times \Sigma \times \{L,R,S\} \times (\Sigma \cup \{S\}) \times Q$$
  donde $L=$ izquierda, $R=$ derecha, $S=$ quieto.

#### Restricciones sobre $\delta$
- $\delta(\ast, \triangleright, \ast)$ no puede ser de la forma $(L,\ast,\ast,\ast,\ast)$ (no pasar a la izquierda del inicio de la cinta de entrada).
- $\delta(\ast, \ast, \triangleright)$ no puede ser de la forma $(\ast,\ast,L,\ast,\ast)$ (ídem para cinta de trabajo).
- $\delta(q_f, a, b) = (S, b, S, S, q_f)$ (el estado final es absorbente y no modifica las cintas).

### MT con $k$ cintas
Tiene 1 cinta de entrada, $k-2$ de trabajo y 1 de salida. Su función de transición es
$$\delta: Q \times \Sigma^{k-1} \to \{L,R,S\} \times \Sigma^{k-2} \times \{L,R,S\}^{k-2} \times (\Sigma \cup \{S\}) \times Q.$$

## Configuraciones y cómputos

**Configuración**: fotografía instantánea de la máquina (contenido de las cintas, posiciones de las cabezas y estado actual). $\delta$ hace evolucionar la configuración $C$ en un paso. Hay configuraciones iniciales y finales.

**Notación**: fijado $\Gamma$, definimos $\Gamma' = \Gamma \cup \{\triangleright, \square\}$. Las máquinas trabajan con $\Gamma'$, mientras que entradas y salidas son palabras sobre $\Gamma$.

**Cómputo**: secuencia $C_0, \dots, C_\ell$ de configuraciones tal que $C_0$ es inicial y $C_\ell$ es final. $\ell$ es la **longitud** del cómputo. Decimos que $M$ con entrada $x$ **termina** si existe un cómputo de $M$ a partir de $x$.

Si no existe cómputo, la máquina se "cuelga" (secuencia infinita de configuraciones).
