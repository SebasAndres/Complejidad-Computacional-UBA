# Clase 4 — Máquinas no-determinísticas, reducibilidad polinomial y lógica proposicional

## 1. Máquinas no-determinísticas (NTM)

### Máquinas determinísticas

Las vistas hasta ahora son **determinísticas**: cada configuración evoluciona de una única forma. Un cómputo de $M=(\Sigma,Q,\delta)$ a partir de $x$ es
$$C_0 \xrightarrow{\delta} C_1 \xrightarrow{\delta} C_2 \xrightarrow{\delta} \cdots \xrightarrow{\delta} C_\ell$$
con $C_\ell$ final.

### Definición de NTMV

Una máquina no-determinística es una tripla $(\Sigma, Q, \delta)$ con dos diferencias respecto a las determinísticas:

1. La función de transición es
$$\delta: Q \times \Sigma^{k-1} \to \big(\{L,R,S\}\times \Sigma^{k-2} \times \{L,R,S\}^{k-2} \times (\Sigma \cup \{S\}) \times Q\big)^2$$
es decir, $\delta$ especifica **una o dos** posibles evoluciones por paso.
2. $Q$ tiene tres estados distinguidos: $q_0$, $q_{\text{sí}}$ y $q_{\text{no}}$.

### Cómputo y aceptación

Una **configuración final** de una NTM $N$ es aquella cuyo estado es $q_{\text{sí}}$ o $q_{\text{no}}$. Un cómputo de $N$ a partir de $x$ es $C_0, \dots, C_\ell$ tal que:

1. $C_0$ es inicial.
2. $C_{i+1}$ es la evolución de $C_i$ por alguna de las dos tuplas de $\delta$.
3. $C_\ell$ está en estado $q_{\text{sí}}$ o $q_{\text{no}}$.

Un **cómputo aceptador** es uno en el que $C_\ell$ está en $q_{\text{sí}}$.

### Lenguaje aceptado

$N$ **acepta** $x$ si existe un cómputo aceptador; si no, lo **rechaza**.
$$N \text{ decide } L \iff \forall x\ (x \in L \iff N \text{ acepta } x).$$

**Observaciones**:

- Las NTM no computan funciones; solo aceptan lenguajes.
- La cinta de salida es irrelevante.
- Notación: $N(x)=1$ si acepta, $N(x)=0$ si rechaza. $\mathcal{L}(N)$ es el lenguaje decidido.

### Tiempo no-determinístico

$N$ corre en tiempo $T(n)$ si para todo $x$, **todo** cómputo de $N$ a partir de $x$ tiene longitud $\leq T(|x|)$. Es decir, la rama más larga del árbol de cómputo tiene esa cota.

### Clase $\mathbf{NDTime}(T(n))$

$\mathbf{NDTime}(T(n))$: lenguajes $L$ tales que existe una NTM $N$ que decide $L$ en tiempo $O(T(n))$.

### Cómputos codificados con palabras binarias

Si $\delta(q,s)=(a,b)$, definimos $\delta_0(q,s)=a$ y $\delta_1(q,s)=b$. Cada cómputo de longitud $T(|x|)$ se codifica con una cadena $u \in \{0,1\}^{T(|x|)}$ donde $u(i)=0$ si se usó $\delta_0$ y $u(i)=1$ si se usó $\delta_1$ en el paso $i$.

### Simulación determinística

Si $N$ corre en tiempo $T(n)$, podemos decidir si $N$ acepta o rechaza $x$ con una máquina determinística en tiempo $O(2^{T(n)^2})$: probamos los $2^{T(n)}$ cómputos posibles, cada uno cuesta $O(T(n) \cdot 2^{T(n)})$.

### Definición alternativa de NP

#### Teorema

$$\mathbf{NP} = \bigcup_{c \in \mathbb{N}} \mathbf{NDTime}(n^c).$$

Es decir, la definición por verificador y la definición por NTM son equivalentes.

**Prueba** ($\supseteq$): Dada NTM $N$ que decide $L$ en tiempo polinomial $p$, tomamos como certificado $u$ la codificación del cómputo aceptador. Un verificador $M(\langle x,u\rangle)$ simula $N$ siguiendo $u$ y acepta sii ese cómputo es aceptador.

**Prueba** ($\subseteq$): Dada $M$ verificadora, construimos NTM $N$ que, con entrada $x$, "inventa" $u \in \{0,1\}^{p(|x|)}$ no-determinísticamente (escribiendo 0 o 1 en su cinta de trabajo usando las dos ramas de $\delta$) y luego simula $M(\langle x,u\rangle)$.

### NTM ↔ palabras binarias

Como para MT determinísticas: toda palabra en $\{0,1\}^*$ representa alguna NTM; hay numerables NTM.

### NTM universal

**Teorema**: Existe una NTM $\mathcal{NU}$ tal que $\mathcal{NU}(\langle i,x\rangle)$ acepta sii $N_i$ acepta $x$; si $N_i$ corre en tiempo $T(n)$, $\mathcal{NU}(\langle i,x\rangle)$ lo decide en $c \cdot T(|x|)$ pasos, con $c$ dependiendo solo de $i$.

## 2. Reducibilidad polinomial

### Definición (Karp)

$L \subseteq \{0,1\}^*$ es **Karp reducible polinomialmente** a $L' \subseteq \{0,1\}^*$, notado $L \leq_p L'$, si existe $f: \{0,1\}^* \to \{0,1\}^*$ computable en tiempo polinomial tal que
$$x \in L \iff f(x) \in L'.$$

$f$ se llama **reducción polinomial**; decimos $L \leq_p L'$ **vía** $f$.

### NP-hard y NP-completo

- $L$ es **NP-hard** si $L' \leq_p L$ para todo $L' \in \mathbf{NP}$.
- $L$ es **NP-completo** si $L \in \mathbf{NP}$ y $L$ es NP-hard.

**Ejercicio**: Si $L \leq_p L'$ y $L' \in \mathbf{P}$, entonces $L \in \mathbf{P}$.

### Teorema: $\leq_p$ es transitiva

Si $L \leq_p L'$ vía $f$ y $L' \leq_p L''$ vía $g$, entonces $L \leq_p L''$ vía $g \circ f$.

**Prueba**. Sean $M_f$ y $M_g$ las máquinas que computan $f$ y $g$ en tiempos $O(n^c)$ y $O(n^d)$. Definimos $M$ que simula $M_f(x)$ (obteniendo $y=f(x)$ con $|y|=O(|x|^c)$) y luego $M_g(y)$. $M$ corre en $O(n^{cd})$.

### Teorema

Si $\mathbf{NP}\text{-hard} \cap \mathbf{P} \neq \emptyset$, entonces $\mathbf{P} = \mathbf{NP}$.

### Corolario

Si $L \in \mathbf{NP}\text{-completo}$, entonces $L \in \mathbf{P}$ sii $\mathbf{P} = \mathbf{NP}$.

### Ejemplo: TMSAT es NP-completo

Llamemos $M_y$ a la máquina determinística con $\langle M \rangle = y$.
$$\mathsf{TMSAT} = \{\langle y, x, 1^n, 1^t\rangle : \exists u \in \{0,1\}^n\ M_y(xu)=1 \text{ en } \leq t \text{ pasos}\}.$$

**Proposición**: $\mathsf{TMSAT} \in \mathbf{NP}\text{-completo}$.

**Prueba**: $\mathsf{TMSAT} \in \mathbf{NP}$ es claro (el certificado es $u$). Para ver que es NP-hard, tomamos $L \in \mathbf{NP}$ con verificador $M$ que corre en tiempo $q(n)$ y certificado de tamaño $\leq p(|x|)$. Definimos
$$f(x) = \langle \langle M \rangle, x, 1^{p(|x|)}, 1^{q(|x|+p(|x|))}\rangle.$$
$f$ es computable en tiempo polinomial y
$$f(x) \in \mathsf{TMSAT} \iff \exists u \in \{0,1\}^{p(|x|)}\ M(xu)=1 \text{ en } \leq q(|xu|) \text{ pasos} \iff x \in L.$$

## 3. Lógica proposicional

### Fórmulas booleanas

Se forman con la gramática
$$\varphi ::= p \mid \neg \varphi \mid (\varphi \wedge \varphi) \mid (\varphi \vee \varphi), \qquad p \in \mathsf{PROP}.$$
El **tamaño** de $\varphi$ es la cantidad de símbolos.

Una **valuación** es $v: \mathsf{PROP} \to \{0,1\}$. Definimos $v \models \varphi$ por inducción:

- $v \models p$ si $v(p)=1$.
- $v \models \neg\varphi$ si no $v \models \varphi$.
- $v \models \varphi \wedge \psi$ si $v \models \varphi$ y $v \models \psi$.
- $v \models \varphi \vee \psi$ si $v \models \varphi$ o $v \models \psi$.

Decimos que $\varphi$ es:

- **verdadera** para $v$ (o que $v$ la satisface) si $v \models \varphi$.
- **falsa** para $v$ si $v \not\models \varphi$.
- **satisfacible** si existe $v$ tal que $v \models \varphi$.
- **tautología** si $v \models \varphi$ para toda $v$.

### Valuaciones parciales

Notación $\varphi(p_1, \dots, p_n)$ indica que las variables de $\varphi$ están entre $p_1, \dots, p_n$.

**Proposición**: Si $v, v'$ coinciden en $\{p_1, \dots, p_n\}$, entonces $v \models \varphi(p_1,\dots,p_n) \iff v' \models \varphi(p_1,\dots,p_n)$. Por ende podemos pensar $v \in \{0,1\}^n$.

### Forma normal conjuntiva (CNF)

Una fórmula está en **CNF** si es
$$(a_{11} \vee \cdots \vee a_{1n_1}) \wedge \cdots \wedge (a_{m1} \vee \cdots \vee a_{mn_m})$$
donde cada $a_{ij}$ es un **literal** (forma $p$ o $\neg p$).

En **3CNF** cada cláusula tiene a lo sumo 3 literales.

Representamos $\varphi \in \mathsf{CNF}$ con $\langle \varphi \rangle \in \{0,1\}^*$.

### Problemas SAT y 3SAT

$$\mathsf{SAT} = \{\langle \varphi \rangle : \varphi \in \mathsf{CNF} \text{ es satisfacible}\}$$
$$\mathsf{3SAT} = \{\langle \varphi \rangle : \varphi \in \mathsf{3CNF} \text{ es satisfacible}\}$$

### Teorema

$\mathsf{SAT}, \mathsf{3SAT} \in \mathbf{NP}$.

**Prueba** (para SAT). El verificador $M(\langle x,u\rangle)$ hace:

- Si $x$ no representa una fórmula, rechaza.
- Si $x = \langle \varphi \rangle$ con $\varphi$ de $m$ variables y $|u| < m$, rechaza.
- Si no, acepta sii $u \upharpoonright m \models \varphi$.

El certificado es la valuación satisfactora. $M$ corre en tiempo polinomial.

### Representación de funciones booleanas en CNF

**Proposición**: Para toda $F: \{0,1\}^\ell \to \{0,1\}$ existe una fórmula $\varphi_F(p_1, \dots, p_\ell)$ en CNF tal que
$$v \models \varphi_F \iff F(v) = 1, \quad \forall v \in \{0,1\}^\ell.$$
Más aún, $\varphi_F$ se computa en tiempo polinomial desde $\langle F \rangle$ y tiene tamaño $O(\ell \cdot 2^\ell)$.

**Construcción**:
$$\varphi = \bigwedge_{v: F(v)=0} \left( \bigvee_{i: v(i)=1} \neg p_i \;\vee\; \bigvee_{i: v(i)=0} p_i \right).$$

Cada cláusula "falsifica" una valuación que no satisface $F$. Tamaño por cláusula: $O(\ell)$; hay a lo sumo $2^\ell$ cláusulas.

**Corolario**: Para toda $F: \{0,1\}^\ell \to \{0,1\}^k$ existe $\varphi_F(p_1, \dots, p_{\ell+k})$ en CNF tal que $uv \models \varphi_F \iff F(u) = v$, computable en tiempo polinomial desde $\langle F \rangle$ y de tamaño $O((\ell+k) 2^{\ell+k})$. Se obtiene aplicando el resultado anterior a $G(uv) = 1 \iff F(u)=v$.
