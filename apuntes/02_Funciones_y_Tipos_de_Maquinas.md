# Clase 2 — Funciones computables, tiempo de cómputo y variantes de máquinas

## Funciones computables

Sea $f: \Gamma^* \to \Gamma^*$ y $M = (\Gamma', Q, \delta)$. Decimos que $M$ **computa** a $f$ si para todo $x \in \Gamma^*$ existe un cómputo $C_0, \dots, C_\ell$ de $M$ a partir de $x$ tal que en $C_\ell$ la cinta de salida tiene escrito $f(x)$ seguido de blancos. Notamos $M(x) = f(x)$.

- $f$ es **computable** si existe una máquina que la computa.
- Para una $f$ computable, existen **infinitas** máquinas que la computan.

**Observación**: podemos representar a las máquinas como autómatas. Los nodos son los estados y las transiciones se representan como flechas etiquetadas con la regla (ej: $1,\square \to L,1,R,0$).

![](../img/transiciones_mt_automatas.png)

### Funciones parciales
Una función parcial puede indefinirse en algunos puntos:
- $f(x)\uparrow$: $f$ se indefine en $x$.
- $f(x)\downarrow$: $f$ se define en $x$.
- $\mathrm{Dom}(f) = \{ x : f(x)\downarrow \}$.

Notación: $f : \subseteq \Gamma^* \to \Gamma^*$.

En general, como las máquinas pueden colgarse, van a computar funciones parciales.

#### Parcialmente computable
Sea $f : \subseteq \Gamma^* \to \Gamma^*$ y $M = (\Gamma', Q, \delta)$. $M$ computa a $f$ si para todo $x \in \Gamma^*$:
- Si $f(x)\downarrow$: existe un cómputo $C_0, \dots, C_\ell$ tal que en $C_\ell$ la salida es $f(x)$ seguido de blancos. Decimos $M(x)\downarrow$.
- Si $f(x)\uparrow$: existe una secuencia infinita $C_0, C_1, \dots$ de configuraciones que no es cómputo (M se cuelga).

$f$ es **parcial computable** si existe una máquina que la computa.

### Parciales vs. totales
Una función total mapea **toda** entrada; una parcial es un mapeo posiblemente incompleto.

## Tiempo de cómputo

**Tamaño de la entrada**: $|x| = |[x]|$ para $x \in \Gamma^*$.

Sea $T: \mathbb{N} \to \mathbb{N}$ y $M$ una máquina:
- $M$ **corre en tiempo $T(n)$** si para todo $x \in \Gamma^*$ existe un cómputo de $M$ a partir de $x$ de longitud $\leq T(|x|)$. En particular, $M$ no se cuelga.
- $M$ computa $f$ en tiempo $T(n)$ si corre en tiempo $T(n)$ y computa a $f$.

### Notación $O$
Sea $f,g: \mathbb{N} \to \mathbb{N}$. $f = O(g)$ si existe $c$ tal que para todo $n$ suficientemente grande $f(n) \leq c\cdot g(n)$.

- $M$ corre en tiempo $O(T(n))$ si existe $c$ tal que $\forall x \in \Gamma^*$ (salvo finitos) hay un cómputo de longitud $\leq c \cdot T(|x|)$.
- $M$ corre en **tiempo polinomial** si existe un polinomio $p$ tal que $M$ corre en tiempo $O(p)$.

**Observación**: un lenguaje $L$ es decidible en tiempo $T(n)$, $O(T(n))$ o polinomial si $\chi_L$ es computable con esas cotas.

### Definiciones clave basadas en el límite $L = \lim_{n \to \infty} \frac{f(n)}{g(n)}$

|Notación	| Condición sobre el límite L	|Interpretación intuitiva |
|------|---|---|
|$f=o(g)$|$L=0$ |	f crece estrictamente más lento que g.|
|$f=O(g)$|$L<∞$ (incluye el 0)|	f no crece más rápido que g.|
|$f=Θ(g)$|$0<L<∞$|	f y g crecen al mismo ritmo.|
|$f=Ω(g)$|$L>0$| (incluye ∞)	f crece al menos tan rápido como g.|
|$f=ω(g)$|$L=∞$|	f crece estrictamente más rápido que g.|

### Definiciones formales
$$f(n) = O(g(n)) \iff \exists c > 0, \exists n_0 \in \mathbb{N} : \forall n \geq n_0, 0 \leq f(n) \leq c \cdot g(n)$$
$$f(n) = \Omega(g(n)) \iff \exists c > 0, \exists n_0 \in \mathbb{N} : \forall n \geq n_0, 0 \leq c \cdot g(n) \leq f(n)$$
$$f(n) = \Theta(g(n)) \iff \exists c_1, c_2 > 0, \exists n_0 \in \mathbb{N} : \forall n \geq n_0, c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)$$
$$f(n) = o(g(n)) \iff \forall c > 0, \exists n_0 \in \mathbb{N} : \forall n \geq n_0, 0 \leq f(n) < c \cdot g(n)$$
$$f(n) = \omega(g(n)) \iff \forall c > 0, \exists n_0 \in \mathbb{N} : \forall n \geq n_0, 0 \leq c \cdot g(n) < f(n)$$

**Observación:** $f=o(g) \iff g=\omega (f)$

### Múltiples parámetros
Para codificar entradas con varias componentes se puede:
- Concatenar usando símbolos distinguidos: $\triangleright \sigma \square \tau \square \square \square$.
- Usar codificaciones autodelimitantes sobre $\{0,1\}^*$ (convención elegida en la materia).

### Funciones construibles en tiempo
$T: \mathbb{N} \to \mathbb{N}$ es **construible en tiempo** si:
- $T(n) \geq n$.
- La función $1^n \mapsto [T(n)]$ es computable en tiempo $O(T(n))$.

## Codificación de máquinas $\langle M \rangle$
Numeramos los estados de $Q$ desde $0$ hasta $|Q|-1$ y representamos cada estado $n$ con $[n]$. Reservamos $0$ para $q_0$ y $1$ para $q_f$.

Cada símbolo de $\Sigma \cup \{L,R,S\}$ se codifica con 3 bits:
- $[0]=000$
- $[1]=001$
- $[\square]=010$
- $[\triangleright]=011$
- $[L]=100$
- $[R]=101$
- $[S]=110$

Codificación de $\delta$:

![](../img/codificacion_transiciones.png)

### Máquinas ↔ palabras binarias
- Toda palabra $x \in \{0,1\}^*$ representa alguna máquina.
- Identificamos máquinas con palabras: "la máquina $x$" o "la $x$-ésima máquina" es la única $M$ tal que $\langle M \rangle = x$.
- Toda máquina representa una función parcial.
- Toda función parcial computable tiene infinitas máquinas que la computan.
- Toda función parcial computable se codifica con infinitas palabras.

### Numerabilidad
- Hay **numerables** máquinas.
- Hay **numerables** funciones computables $\{0,1\}^* \to \{0,1\}$.
- Hay **no numerables** funciones $\{0,1\}^* \to \{0,1\}$.
- Por lo tanto existen funciones **no computables** (conteo/diagonalización).

## Variantes de máquinas

### Sobre alfabetos no estándar
**Proposición**: Si $f$ es computable en tiempo $T(n)$ por $M=(\Gamma, Q, \delta)$ entonces $f$ es computable en tiempo $O(\log |\Gamma| \cdot T(n))$ por $M'=(\{0,1,\triangleright,\square\}, Q', \delta')$.

*Idea*: codificar cada símbolo de $\Gamma$ en binario usando $\lceil \log |\Gamma| \rceil$ celdas.

### Máquinas de cinta única
Tienen una sola cinta con cabeza de lectura y escritura. Función de transición:
$$\delta: Q \times \Sigma \to \Sigma \times \{L,R,S\} \times Q$$
(con restricciones para no pasar del inicio de la cinta).

**Proposición**: Si $f$ es computable en tiempo $T(n)$ por una máquina estándar de $k \geq 3$ cintas, entonces es computable en tiempo $O(T(n)^2)$ por una máquina de cinta única.

*Idea*: M' codifica en su única cinta todas las cintas de M (con marcadores de posición de cabeza subrayados) y en cada simulación de un paso de M, M' barre la cinta de izquierda a derecha leyendo los símbolos bajo las cabezas, aplica $\delta$ y luego barre de derecha a izquierda actualizando. Cada paso de M cuesta $O(T(n))$ pasos a M' (la región usada tiene a lo sumo $k\cdot T(n)$ celdas).

### Máquinas oblivious
Una máquina $M$ es **oblivious** si para cada entrada $x$ y cada $i \in \mathbb{N}$:
- La posición de las cabezas de las cintas de entrada y trabajo en el $i$-ésimo paso solo depende de $i$ y de $|x|$, **no** del contenido de $x$.
- Las funciones que computan esas posiciones a partir de $i,|x|$ son computables en tiempo polinomial.

**Proposición**: Si $f$ es computable en tiempo $T(n)$ por una máquina estándar, entonces hay una máquina oblivious que computa $f$ en tiempo $O(T(n)^2)$.

*Idea*: la máquina $M'$ construida en la simulación de cinta única es oblivious porque barre de punta a punta en cada paso.

### Máquinas con cintas bi-infinitas
Cintas infinitas en ambas direcciones.

**Proposición**: Si $f$ es computable por una máquina con cintas bi-infinitas en tiempo $T(n)$, entonces es computable por una máquina estándar en tiempo $O(T(n))$.

*Idea*: "plegar" la cinta bi-infinita en una cinta unilateral cuyo alfabeto tiene pares de símbolos $(a,b) \in \{0,1,\square\}^2$; el primer símbolo corresponde a la porción positiva de la cinta y el segundo a la negativa.
