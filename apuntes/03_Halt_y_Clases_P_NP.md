# Clase 3 — Halt, máquina universal y las clases P y NP

## 1. El problema de la detención (*halting problem*)

Definimos $halt: \{0,1\}^* \to \{0,1\}$ como
$$halt(x) = \begin{cases} 1 & \text{si la máquina } x \text{ con entrada } x \text{ termina} \\ 0 & \text{si no}\end{cases}$$

### Teorema (Turing, 1936)
$halt$ **no es computable**.

**Demostración (por absurdo)**. Supongamos que $halt$ es computable. Definimos una máquina $M$ tal que $M(x)$ termina sii $halt(x)=0$. Sea $y = \langle M \rangle$. Entonces
$$M(y) \text{ termina} \iff \text{la máquina } y \text{ con entrada } y \text{ no termina} \iff M(y) \text{ no termina}.$$
Absurdo.

## 2. La máquina universal $U$

Sea $M_i$ la máquina tal que $\langle M \rangle = i$. Definimos la función parcial
$$u: \subseteq \{0,1\}^* \to \{0,1\}^*, \qquad u(\langle i,x\rangle) = M_i(x).$$

En particular $u(\langle i,x \rangle) \downarrow$ sii $M_i(x)\downarrow$.

### Teorema (máquina universal)
Existe una máquina $U$ que computa $u$. Más aún, si $M_i$ con entrada $x$ termina en $t$ pasos, entonces $U$ con entrada $\langle i,x \rangle$ termina en $c \cdot t \cdot \log t$ pasos, donde $c$ depende solo de $i$.

**Idea (caso simple, $M$ con una única cinta de trabajo)**: $U$ tiene 3 cintas de trabajo.
- Cinta #1: almacena $x$.
- Cinta #2: simula la cinta de trabajo de $M$.
- Cinta #3: almacena el estado de $M$.

$U$ lee $\langle \langle M \rangle, x \rangle$, copia $x$ en #1, escribe $[q_0]$ en #3 y, mientras el estado no sea $[q_f]$, consulta $\delta$ en la cinta de entrada y actualiza #2 y #3. Buscar $\delta$ por cada paso simulado cuesta una constante $c$ que depende de $M$ pero no de $x$.

En el caso general (varias cintas de trabajo) se puede reducir a una única cinta con sobrecosto $O(t^2)$, pero eso excede la cota $O(t \log t)$; la prueba del caso general es más técnica.

### Máquina universal con tiempo acotado
Definimos la función **total** $\tilde{u}: \{0,1\}^* \to \{0,1\}^*$:
$$\tilde{u}(\langle i,t,x\rangle) = \begin{cases} 1\,M_i(x) & \text{si } M_i(x) \text{ termina en } \leq t \text{ pasos}\\ 0 & \text{si no}\end{cases}$$

### Teorema
Existe una máquina $\tilde{U}$ que computa $\tilde{u}$ en tiempo $c\cdot t \cdot \log t$, con $c$ dependiendo solo de $i$. $\tilde{U}$ tiene una cinta de trabajo adicional para llevar un contador de pasos $\leq t$.

## 3. Clases de complejidad y $\mathbf{DTime}(T(n))$

Sea $L \subseteq \{0,1\}^*$ un lenguaje y $\Sigma$ el alfabeto estándar.

### Definiciones
- **Decisión**: $M=(Q,\Sigma,\delta)$ **decide** $L$ [en tiempo $T(n)$] si $M$ computa $\chi_L$ [en tiempo $T(n)$].
  - $M$ **acepta** $x$ si $M(x)=1$; **rechaza** $x$ si $M(x)=0$.
- **Notación** $\mathcal{L}(M)$: lenguaje decidido por $M$.
- **Clase de complejidad**: conjunto de lenguajes decidibles por máquinas con ciertos recursos acotados. Por ahora, el recurso es el tiempo.

### Clase $\mathbf{DTime}(T(n))$
$\mathbf{DTime}(T(n))$ es la clase de lenguajes $L$ para los cuales existe una máquina **determinística** $M$ que decide $L$ en tiempo $O(T(n))$. La "D" indica *determinística*.

## 4. La clase P

### Definición
$$\mathbf{P} = \bigcup_{c > 0} \mathbf{DTime}(n^c)$$

Son los problemas que se resuelven en tiempo polinomial respecto al tamaño de la entrada. **P es considerada la clase de problemas "factibles"**.

### Ejemplo: conectividad de grafos
Un grafo $G=(V,E)$ es **conexo** si todo par de nodos está unido por un camino.
$$\mathsf{CON} = \{\langle G \rangle : G \text{ es conexo}\}$$

Representamos $G$ por su matriz de adyacencia con $V=\{0,\dots,k-1\}$. Una máquina $M$ hace DFS desde un nodo $u$ marcando nodos visitados. Si quedó un nodo sin visitar, escribe 0; si no, escribe 1. Si $n = |\langle G \rangle|$, $M$ corre en tiempo $O(n^2)$, luego $\mathsf{CON} \in \mathbf{P}$.

## 5. Simplificación: máquinas sin cinta de salida
Para calcular funciones valuadas en $\{0,1\}$ no hace falta una cinta de salida. Alternativas:
- Dejar el 0/1 en la celda de trabajo donde termina la cabeza al entrar a $q_f$.
- Reemplazar $q_f$ por dos estados $q_{\text{sí}}$ (devuelve 1) y $q_{\text{no}}$ (devuelve 0); la configuración final queda en uno u otro.

**Proposición**: Si $L$ es decidible en tiempo $T(n)$ por una máquina estándar de 3 cintas, entonces es decidible en tiempo $O(T(n))$ por una máquina sin cinta de salida.

## 6. La clase NP

### Definición (por verificador)
$\mathbf{NP}$ es la clase de lenguajes $L$ tales que existe un polinomio $p: \mathbb{N} \to \mathbb{N}$ y una máquina determinística $M$ con:
- $M$ corre en tiempo polinomial.
- Para todo $x$:
$$x \in L \iff \exists u \in \{0,1\}^{p(|x|)} \text{ tal que } M(\langle x,u \rangle) = 1.$$

$M$ es el **verificador** y $u$ un **certificado** para $x$.

**Notar** que la segunda condición es equivalente a $x \in L \iff \exists u \in \{0,1\}^{p(|x|)} M(xu)=1$, porque $M$ puede primero contar $m$, las celdas hasta el primer blanco, y luego buscar el primer $n$ tal que $m = n + p(n)$, recuperando así $x$ y $u$.

### Teorema
$\mathbf{P} \subseteq \mathbf{NP}$.

**Demostración**. Sea $L \in \mathbf{P}$ decidida por $M$ en tiempo polinomial. Tomamos $p(n)=0$ y definimos $M'(\langle x,\epsilon\rangle) = M(x)$. Luego
$$x \in L \iff M(x)=1 \iff M'(\langle x,\epsilon\rangle)=1 \iff \exists u \in \{0,1\}^0\ M'(\langle x,u\rangle)=1.$$

### Ejemplo: conjunto independiente
Un conjunto $X$ de nodos de $G=(V,E)$ es **independiente** si no existen $u,v \in X$ con $(u,v) \in E$.
$$\mathsf{INDSET} = \{\langle G,k\rangle : G \text{ tiene un conjunto independiente de } \geq k \text{ vértices}\}.$$

- Suponemos $V = \{[0], [1], \dots, [|V|-1]\}$.
- Certificado $u$: lista de $k$ nodos distintos que forman un conjunto independiente.
- Tamaño de $u$: $O(k \lceil \log |V| \rceil)$. Si $n = |\langle \langle G \rangle, [k] \rangle|$, como $k \leq |V|$, tenemos $|u| = O(n \log n)$; eligiendo un polinomio cuadrático $p$, $|u|=p(n)$ (completando con ceros).
- El verificador $M$ recibe $x$; si no tiene la forma $\langle \langle G,k\rangle, u\rangle$ con $|u|=p(n)$, rechaza; si no, verifica en tiempo polinomial que $u$ codifique un conjunto independiente de $k$ nodos.

Entonces $\mathsf{INDSET} \in \mathbf{NP}$.
