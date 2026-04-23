# Clase 5 — Mini-configuraciones, Cook-Levin, problemas NP-completos, coNP, ExpTime y NExpTime

## 1. Mini-configuraciones

Para simplificar, consideremos una máquina determinística $M = (\Sigma, Q, \delta)$:
- **sin** cinta de salida,
- con una cinta de entrada y
- con una sola cinta de trabajo (que funciona también como salida).

Todo se generaliza a cualquier cantidad de cintas de trabajo.

### Mini-configuración
Supongamos un cómputo $C_0, \dots, C_\ell$ de $M$ con entrada $y$. La **mini-configuración** en el paso $i$ es la tupla
$$z_i = (a_i, b_i, c_i) \in \Sigma \times \Sigma \times Q$$
donde:
- $a_i$: símbolo leído por la cabeza de entrada en $C_i$.
- $b_i$: símbolo leído en la cinta de trabajo en $C_i$.
- $c_i$: estado de $C_i$.

### Máquina oblivious
Si además $M$ es oblivious, podemos definir (en tiempo polinomial):
- $e(i,n)$: posición de la cabeza de entrada en el paso $i$ con entrada de tamaño $n$.
- $t(i,n)$: posición de la cabeza de trabajo en el paso $i$.
- $\mathsf{prev}(i,n) = \max\{j < i : t(j,n) = t(i,n)\} \cup \{1\}$: el último paso previo en que la cabeza de trabajo estaba en la misma celda que en el paso $i$ (o $1$ si no existe).

### Transición entre mini-configuraciones
$z_0 = (x(0), \square, q_0)$ y, para $i > 0$, $z_i$ depende de:
- $z_{i-1}$ (estado y símbolos en paso $i-1$),
- $\delta$ de $M$,
- el contenido de la cinta de entrada en la posición $e(i,|x|)$,
- el contenido de la cinta de trabajo en la posición $\mathsf{prev}(i,|x|)$, que está en $z_{\mathsf{prev}(i,|x|)}$.

### Codificación binaria de mini-configuraciones
Cada $z \in \Sigma \times \Sigma \times Q$ se codifica con $\langle z \rangle \in \{0,1\}^k$ donde $k = 4 + \lceil \log |Q|\rceil$ (depende solo de $M$):
- Los 4 símbolos de $\Sigma = \{0,1,\triangleright,\square\}$ con $00, 11, 01, 10$.
- Los estados de $Q$ con $\lceil \log |Q|\rceil$ bits ($0\dots0$ es $q_0$, $0\dots1$ es $q_f$).

### La función $F$ de evolución en un paso
$$F: \{0,1\}^k \times \{0,1\}^k \times \{0,1\}^2 \to \{0,1\}^k$$
$$F(\langle z_{i-1} \rangle,\ \langle z_{\mathsf{prev}(i,|y|)} \rangle,\ \langle x(e(i,|y|))\rangle) = \langle z_i \rangle$$
y $F(\cdot)=0^k$ en el resto (casos irrelevantes).

### $F$ representable en CNF
Por la construcción de la Clase 4, existe $\varphi_F(\bar p, \bar q, \bar r, \bar s)$ en CNF con variables libres
- $\bar p = p_1, \dots, p_k$ ($\langle z_{i-1} \rangle$),
- $\bar q = q_1, \dots, q_k$ ($\langle z_{\mathsf{prev}(i,|y|)}\rangle$),
- $\bar r = r_1, r_2$ ($\langle y(e(i,|y|))\rangle$),
- $\bar s = s_1, \dots, s_k$ ($\langle z_i \rangle$),

tal que para todo $\bar a, \bar b, \bar d \in \{0,1\}^k$ y $\bar c \in \{0,1\}^2$:
$$\bar a \bar b \bar c \bar d \models \varphi_F \iff \bar d = F(\bar a, \bar b, \bar c).$$

$\varphi_F$ se computa desde $\langle F \rangle$ en tiempo polinomial, con tamaño $\leq (3k+2) \cdot 2^{3k+2}$. **Con $M$ fija, $k$ es constante, por lo que $\varphi_F$ tiene tamaño constante.**

## 2. Teorema de Cook-Levin

### Teorema
$\mathsf{SAT} \in \mathbf{NP}\text{-hard}$.

**Demostración incorrecta (intento ingenuo)**. Dado $L \in \mathbf{NP}$ con verificador $M$ y certificado en $\{0,1\}^{p(|x|)}$, definir $F_x(u) = M(xu)$ y convertirlo a CNF. Problema: $\varphi_x$ tendría tamaño $O(p(|x|) \cdot 2^{p(|x|)})$ (exponencial).

### Demostración correcta
Fijemos $L \in \mathbf{NP}$. Existe una máquina determinística $M$ tal que:
- $M$ corre en tiempo polinomial $t(n)$,
- $M$ es oblivious, sin cinta de salida y con única cinta de trabajo,
- existe $p$ polinomio tal que $x \in L \iff \exists u \in \{0,1\}^{p(|x|)}\ M(xu)=1$.

Dado $x$, construimos $\varphi_x \in \mathsf{CNF}$ en tiempo polinomial tal que
$$x \in L \iff \varphi_x \in \mathsf{SAT}.$$

Afirmamos que $x \in L$ sii existe una codificación de la entrada $y \in \{0,1\}^{2n+4}$ (con $n = |x|+p(|x|)$) y una secuencia de mini-configuraciones $z_0, \dots, z_m \in \{0,1\}^k$ (con $m = t(n)$) tal que:
- $\psi_1 = $ "la entrada empieza con $x$ y con algún $u \in \{0,1\}^*$".
- $\psi_2 = $ "$z_0$ es la configuración inicial".
- $\psi_3 = $ "$z_j$ evoluciona a $z_{j+1}$ para $j=0, \dots, m-1$".
- $\psi_4 = $ "$z_m$ es una configuración final aceptadora".

Cada una se expresa en CNF en tiempo polinomial:

**$\psi_1$**: codifica que $y = \triangleright\, x\, u\, \square$:
- $y(0)y(1) = 01$ (marca $\triangleright$).
- $y(2j+2)y(2j+3)$ codifican $x(j)$ para $0 \leq j \leq |x|-1$.
- $y(2j)y(2j+1)$ tienen el mismo valor para $|x|+1 \leq j \leq n$ (u libre).
- $y(2n+2)y(2n+3) = 10$ (marca $\square$).

Tamaño: $|\psi_1| = O(n)$.

**$\psi_2$**: "$z_0 = (x(0), \square, q_0)$". Tamaño $O(1)$ (con $M$ fija).

**$\psi_3$**: para cada $0 < i \leq m$, la condición
$$\langle z_i \rangle = F(\langle z_{i-1} \rangle, \langle z_{\mathsf{prev}(i,n)}\rangle, \langle y(e(i,n))\rangle)$$
se expresa con $\psi_3^i$ en CNF usando $\varphi_F$. $\psi_3^i$ se computa en tiempo polinomial y tiene tamaño $O(k \cdot 2^{3k})$, con $k$ constante. Luego $\psi_3 = \bigwedge_{i=1}^{m} \psi_3^i$ se construye en tiempo polinomial y tiene tamaño polinomial.

**$\psi_4$**: "$z_m$ es de la forma $(*, 1, q_f)$". Tamaño $O(1)$.

Finalmente
$$\varphi_x = \psi_1 \wedge \psi_2 \wedge \psi_3 \wedge \psi_4, \qquad |\varphi_x| = O(|x| + t(|x| + p(|x|))).$$

$\varphi_x$ se construye en tiempo polinomial y $x \in L \iff \varphi_x \in \mathsf{SAT}$.

### Corolario
$\mathsf{SAT} \in \mathbf{NP}\text{-completo}$.

### 3SAT también es NP-completo
Ya sabemos $\mathsf{3SAT} \in \mathbf{NP}$. Para ver NP-hardness se prueba $\mathsf{SAT} \leq_p \mathsf{3SAT}$ (ejercicio).

**Corolario**: $\mathsf{SAT}, \mathsf{3SAT} \in \mathbf{NP}\text{-completo}$.

## 3. Otros problemas NP-completos

### INDSET
**Proposición**: $\mathsf{INDSET} \in \mathbf{NP}\text{-completo}$.

**Prueba** (NP-hard vía $\mathsf{3SAT} \leq_p \mathsf{INDSET}$). Dada $\varphi = \bigwedge_{i=1}^m (l_{i1} \vee l_{i2} \vee l_{i3})$ en 3CNF, definimos un grafo $G_\varphi$ con $3m$ vértices (uno por cada aparición de literal). Arista entre $z$ (correspondiente a $l_{ij}$) y $z'$ (correspondiente a $l_{i'j'}$) si:
- $i = i'$ (mismo triángulo de cláusula), o
- $l_{ij}$ es la negación de $l_{i'j'}$.

$G_\varphi$ se construye en tiempo polinomial. Se prueba que $\varphi$ es satisfacible sii $G_\varphi$ tiene un conjunto independiente de $\geq m$ vértices:
- $\Rightarrow$: Si $v \models \varphi$, para cada cláusula $i$ hay un $j$ con $v \models l_{ij}$. El conjunto $S$ de los vértices correspondientes es independiente (no hay aristas dentro del mismo triángulo ni entre literales contradictorios).
- $\Leftarrow$: Un conjunto independiente $S$ de $m$ vértices debe tener exactamente uno por triángulo. Para cada $z \in S$, si corresponde a $x_i$ definimos $v(x_i) = 1$; si corresponde a $\neg x_i$ definimos $v(x_i) = 0$. Bien definido por independencia. Luego $v \models \varphi$.

### CAMHAM (camino hamiltoniano)
Un **camino hamiltoniano** en un grafo dirigido $G$ visita todos los vértices exactamente una vez.
$$\mathsf{CAMHAM} = \{\langle G\rangle : G \text{ tiene un camino hamiltoniano}\}.$$

**Proposición**: $\mathsf{CAMHAM} \in \mathbf{NP}\text{-completo}$.

### TSP (travelling salesman problem)
Dadas $n$ ciudades con matriz de distancias $M$ ($n \times n$):
$$\mathsf{TSP} = \{\langle M, k\rangle : \exists \text{ ruta de distancia } \leq k \text{ que visita todas las ciudades y vuelve al origen}\}.$$

**Proposición**: $\mathsf{TSP} \in \mathbf{NP}\text{-completo}$.

### KNAPSACK (problema de la mochila)
Lista $M = [(v_1,p_1), \dots, (v_n,p_n)]$ de valores y pesos.
$$\mathsf{KNAPSACK} = \{\langle M, v, p\rangle : \exists \text{ subconjunto con valor total } \geq v \text{ y peso } \leq p\}.$$

**Proposición**: $\mathsf{KNAPSACK} \in \mathbf{NP}\text{-completo}$.

## 4. La clase coNP

### Problemas $\mathcal{C}$-hard y $\mathcal{C}$-completos
Para una clase $\mathcal{C}$:
- $L$ es $\mathcal{C}$-**hard** si $L' \leq_p L$ para todo $L' \in \mathcal{C}$.
- $L$ es $\mathcal{C}$-**completo** si $L \in \mathcal{C}$ y es $\mathcal{C}$-hard.

Son nociones relativas a $\leq_p$; para algunas clases se necesitarán reducciones más débiles.

### Complemento de un lenguaje y clase
- $\bar L = \{0,1\}^* \setminus L$.
- $\text{co}\mathcal{C} = \{L : \bar L \in \mathcal{C}\}$.

### Definición de coNP
$\mathbf{coNP} = \{L : \bar L \in \mathbf{NP}\}$.

Equivalentemente: $L \in \mathbf{coNP}$ sii existe un polinomio $p$ y una máquina determinística $M$ que corre en tiempo polinomial tal que
$$x \in L \iff \forall u \in \{0,1\}^{p(|x|)}\ M(\langle x,u\rangle) = 1.$$

### Relación con P y NP
**Ejercicios**:
- $\mathbf{P} \subseteq \mathbf{NP} \cap \mathbf{coNP}$.
- Si $\mathbf{P} = \mathbf{NP}$, entonces $\mathbf{NP} = \mathbf{coNP}$.

### Ejemplo: TAUT (tautología)
$$\mathsf{TAUT} = \{\langle \varphi\rangle : \varphi \in \mathsf{CNF} \text{ es tautología}\}.$$
$\varphi$ es tautología sii $\neg \varphi$ es insatisfacible: $\langle \varphi \rangle \in \mathsf{TAUT} \iff \langle \neg\varphi\rangle \notin \mathsf{SAT}$.

**Ejercicio**: $\mathsf{TAUT} \in \mathbf{coNP}\text{-completo}$.

## 5. ExpTime y NExpTime

$$\mathbf{ExpTime} = \bigcup_{c > 0} \mathbf{DTime}(2^{n^c}), \qquad \mathbf{NExpTime} = \bigcup_{c > 0} \mathbf{NDTime}(2^{n^c}).$$

**Jerarquía conocida**:
$$\mathbf{P} \subseteq \mathbf{NP} \subseteq \mathbf{ExpTime} \subseteq \mathbf{NExpTime}.$$

**Ejercicio**: $\mathbf{NP} \subseteq \mathbf{ExpTime}$.

### Teorema
Si $\mathbf{P} = \mathbf{NP}$, entonces $\mathbf{ExpTime} = \mathbf{NExpTime}$.

**Prueba (padding)**. Sea $L \in \mathbf{NDTime}(2^{n^c})$ decidido por una NTM $N$ en tiempo $c \cdot 2^{n^c}$. Consideremos
$$L_{\text{pad}} = \{\langle x, 1^{2^{|x|^c}}\rangle : x \in L\}.$$

- $L_{\text{pad}} \in \mathbf{NP}$: una NTM $N'$ con entrada $y$ verifica si $y = \langle z, 1^{2^{|z|^c}}\rangle$ y simula $N(z)$ por $c \cdot 2^{|z|^c}$ pasos. Como $|y|$ absorbe el $2^{|z|^c}$, esto es polinomial en $|y|$.
- Por hipótesis $L_{\text{pad}} \in \mathbf{NP} = \mathbf{P}$.
- Luego $L \in \mathbf{DTime}(2^{n^c})$: una máquina $M$ con entrada $x$ computa $y = \langle x, 1^{2^{|x|^c}}\rangle$ (en tiempo $O(2^{|x|^c})$) y decide si $y \in L_{\text{pad}}$ en tiempo polinomial en $|y|$. Total: $O(2^{|x|^{c+d}})$.

### P vs NP
- Pregunta abierta: ¿$\mathbf{P} = \mathbf{NP}$ o $\mathbf{P} \subsetneq \mathbf{NP}$?
- Pregunta intuitiva: ¿es esencialmente más fácil verificar una solución que generarla?
  - Por ejemplo, dado un sistema axiomático $S$:
    $$\{\langle \varphi, 1^n\rangle : \varphi \text{ tiene demostración en } S \text{ de longitud } \leq n\} \in \mathbf{NP}.$$
    Verificar que una secuencia de pasos es demostración está en $\mathbf{P}$.
- ¿Lo mejor que se puede hacer a veces es fuerza bruta?
