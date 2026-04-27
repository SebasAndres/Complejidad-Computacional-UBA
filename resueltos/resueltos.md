# Resueltos CC.

## Practica 2

### 1. Demostrar $L \in P$ para cada $L$

> Para esto debo construir algoritmos que decidan cada $L$ ($x\in L \lor x \notin L$) en tiempo polinomial.

a) $\text{COPRIME} = \{ \langle a,b \rangle: (a:b) == 1 \} \in P$

**dem:**

Uso el algoritmo de Euclides.

```python
def inCOPRIME(x: Tuple[int, int]) -> bool:
    a, b = x
    return mcd(a,b) == 1

def mcd(a: int, b: int) -> int:
    if b == 0: return a
    return mcd(b, a % b)
```

En mcd hay como mucho $n$ divisiones y todas toman $O(n^2)$ -> luego mcd es $O(n^3)$ y isCOPRIME tambien, entonces $\text{COPRIME} \in P$ $\square$

b) $\text{POWER} = \{ \langle a,e,b \rangle: a^e = b \}$

**dem:**

Uso exponenciacion binaria:

```python
def pow(a: int, e: int) -> int:
    # Compl: O(n^3)
    if e == 2:
        return a * a
    if e % 2 == 0:
        return pow(pow(a, e/2), 2)
    return pow(a, e-1) * a
```

a tiene n bits ($a ~ 2^n$), entonces hay $O(n)$ multiplicaciones y cada una toma $O(n^2)$ analogamente a las divisiones $\square$


c) $\text{TREE} = \{\langle G \rangle: G \text{ es un grafo conexo sin ciclos} \}$

**dem:** 
Un grafo es conexo sin ciclos si no vuelvo a visitar un nodo 2 
veces en un recorrido haciendo dfs/bfs desde algun nodo.

Para esto voy a hacer BFS desde cada nodo $(O(n^2))$.
Luego, TREE se computa en $O(n^2)$. $\square$

```python
typedef Graph = [[Node], [Edge]]

def isTREE(g: Graph) -> bool:
	for node in g.nodes:
		counter_visits_per_node = bfs(g, from=node)
		
		# si no es conexo o es ciclico
		if any((x>1 or x==0) for x in counter_visits_per_node):
			return False
	return True
``` 

c) $L: |L| < \infty$

dem:
Cualquier lenguaje finito está en P porque puedo ir validando 1 a 1 por cada uno de sus elementos si x == L[i].
Esto es O(n*costo_comparar) $\square$


### 2) Probar que la clase P está cerrada por unión, intersección y complemento.

**dem:**

Supongo $L, L' \in P$, quiero ver que:

1. $L \cup L' \in P$,

> Trivialmente es validar $x \in L \lor x \in L'$, como ambos están en $P$, corre todo en tiempo polinomial.

2. $L \cap L' \in P$,

> Analogamente: `isLL'(x) = isL(X) && isL'(X)`

3. $L^c \in P$.

> Basta con `isL^c(x) = 1 - isL(x)` $\square$

### 3) Probar $L \in NP$

> Para ser un lenguaje en NP debe cumplir que existe un certificado $u$ tal que existe un algoritmo polinomial $V$ que al correr $V(x,u)$ verifica si $x\in L$. 

a. $\text{HAMPATH} = \{⟨G, s, t⟩ : G \text{ es un grafo con dos nodos s y t tales que hay un camino hamiltoniano de s a t} \}$:

**dem:**

Para probar $\text{HAMPATH} \in NP$ construyo un verificador polinomial.

- **Certificado** $u$: una lista de nodos $[v_0, v_1, \ldots, v_{n-1}]$ que representa el supuesto camino hamiltoniano.
- **Verificador** $V(\langle G,s,t \rangle, u)$: chequea que $u$ sea efectivamente un camino hamiltoniano de $s$ a $t$ en $G$.

```python
def verifyHAMPATH(G: Graph, s: Node, t: Node, u: List[Node]) -> bool:
    # El camino empieza en s y termina en t
    if u[0] != s or u[-1] != t:
        return False
    # Visita todos los nodos exactamente una vez
    if len(u) != len(G.nodes) or len(set(u)) != len(G.nodes):
        return False
    # Cada par consecutivo es una arista de G
    for i in range(len(u) - 1):
        if (u[i], u[i+1]) not in G.edges:
            return False
    return True
```

El certificado tiene tamaño $O(n)$ (lista de $n$ nodos), polinomial en el input. El verificador corre en $O(n)$, polinomial. Luego $\text{HAMPATH} \in NP$. $\square$

b. $\text{CLIQUE} = \{ \langle G \rangle: \text{ G es un grafo con subgrafo completo de tamaño mayor o igual a k} \}$

**dem:**
Debería haber un $V' \subset V_G, |V'|\geq k$ tal que todos sus nodos están conectados entre si.

Planteo que el certificado sea ese $u := V'$.

```c
#define k 100
typedef Node = int;

uint8_t verifykCLIQUE(G: Graph, u: [Node]){	

	if _length(u) < k: return 0;

	foreach (Node inode in u){
		if (! _contains_node(G, inode)): return 0;		

		foreach (Node jnode in u) {
			if (inode == jnode): continue;
			if (G.edges[inode][jnode] == 0): return 0;
		}
	}

	return 1;	
}
```
Esto corre en $O(n^2)$ luego $\text{k-CLIQUE} \in NP$. $\square$

c. $\text{CLIQUE} = \{ \langle G, k \rangle: \text{ G es un grafo con subgrafo completo de tamaño mayor o igual a k} \}$

**dem:**
El algoritmo es análogo al anterior, mismo certificado pero ahora el input tiene a $<G,k>$ y no solo a $G$.
```c
typedef Node = int;

uint8_t verifykCLIQUE(G: Graph, k: int, u: [Node]){     

        if _length(u) < k: return 0;
 
        foreach (Node inode in u){
                if (! _contains_node(G, inode)): return 0;               

                foreach (Node jnode in u) {
                        if (inode == jnode): continue;
                        if (G.edges[inode][jnode] == 0): return 0;
                }
        }

        return 1;       
}
```
$\square$

d. $\text{k-COLORING} = \{⟨G⟩ : \text{G es un grafo que se puede particionar en k conjuntos indepenientes} \}$

**dem:**
Deben haber k grupos sin aristas entre si.

$u = \text{ S lista de grupos de nodos}$

```python
def isKCOLORING(G: Graph, u: [[Node]]) -> bool:
	for i, group in enumerate(u):
		is_valid_group = _check_group_is_in_graph(group, G) \ 
			or _check_no_node_is_in_other_group(group, u[i:]) \
			or _check_no_node_has_connections_with_other_group(group, u[i:], G)

		if not is_valid_group:
			return 0
	return 1	

# _check_group_is_in_graph: O(n)
# _check_no_node_is_in_other_group: O(n)
# _check_no_node_has_connections_with_other_group: O(n)
``` 

Luego $O(n^2) \therefore L \in NP$ $\square$

e. $\text{ISOMORPHISM} = \{ \langle G,H \rangle: \text{G y H son dos grafos isomorfos}\}$

**dem:**

Dos grafos son isomorfos si son el mismo grafo con nodos etiquetados de forma distinta.

El certificado u es la biyección node -> node'. En este caso lo defino como la lista de {node: node', node in GraphA, node in GraphB}.

```python
def _check_edges_from_A_are_in_B(graphA, graphu, u) --> bool:	
    for nodeA, nodeB in u:
        for toA in len(graphA):
            if toA == nodeA: continue
            toB = u[toA]
            if graphB.edges[nodeB, toB] != graphA.edges[nodeA, toA]:
                return 0
    return 1

def isISOMORPHISM(graphA: Graph, graphB: Graph, u: Dict{}) -> bool:
    return _check_lengths_are_equal(graphA, graphB) \
        _check_edges_from_A_are_in_B(graphA, graphB) \
        _check_edges_from_A_are_in_B(graphB, graphA)
```
$\square$

g. $¬\text{SAT} = \{⟨φ⟩: ¬φ \text{ es satisfacible}\}$

**dem**

Una formula es satisfacible si existe una variacion que la hace verdadera.
El certificado es la valuacion de las variables de $\phi$, $u = (x_1, ..., x_n)$.

Evaluar una formula se puede realizar en tiempo lineal respecto al tamaño de la fórmula $|\phi|$.

```python 
def verifyNotSAT(Formula phi, Assignment u) -> bool:
	bool result = evaluate(phi, u)
	return not result
```
$\square$

### 4) Probar que los siguientes programas están en $\text{coNP}$ 

> $\text{coC} = \{ L: L^c \in C\} \rightarrow \text{coNP} = \{ L: L^c \in \text{NP} \}$
> Luego para demostrar $L \in \text{coNP}$ basta con ver que $L^c \in \text{NP}$.

a. $\text{PRIME} = \{ n: n \in \mathbb{N} \text{ es primo }\}$

**dem**:
Basta con ver que $\overline{\text{PRIME}} = \text{COMPOSITE} = \{n : n \text{ no es primo}\} \in \text{NP}$.

```python 
def verifyCOMPOSITE(n: int, cert: int) -> bool:
	# Validar que n no es primo
	
	if (1 < cert < n) and (n % cert == 0): 
		return true
	
	return false
```

Donde `n%cert` se computa en $O(k^2)$ para $max{n,cert} \sim 2^k$. $\square$

b. $\text{GIRTH} = \{ \langle G, k \rangle : G \text{ es un grafo tal que todos sus ciclos simples tienen } k \text{ o menos vértices} \}$ 

**dem**

$\overline{\text{GIRTH}} = \{ \langle G, k \rangle: G \text{ es un grafo que tiene algun ciclo simple con k o más vertices }\}$

El certificado es un camino de nodos que forma un ciclo simple de tamaño mayor o igual a 3.

```python
def verifyNOTGIRTH(G:Graph, k:int, cert:[Node]) -> bool:
	if len(cert) < k: return False
	if cert[0] != cert[-1]: return False	

	prev = cert[0]
	visited = {prev}

	for node in cert[1:-2]:
		if G.edges[prev,node] == 0:
			return False
			
		if node in visited:
			return False
		
		visited.add(node)
	
	if G.edges[cert[-2],cert[0]] == 0: 
		return False
	
	return True
```
$\square$

c) $\text{TAUTOLOGY} = \{ \langle φ \rangle: φ \text {es tautología} \}$

**dem**

$\overline{\text{TAUTOLOGY}}$ es encontrar una valuacion que muestre que $\phi$ no es tautología.

El certificado es una valuacion que no satisface la formula.

```python
def verifyNotTAUTOLOGY(phi: Formula, cert: Assignment) -> bool: 	
	return _eval(phi, cert)
```
$\square$

### 5) Considerar $\text{PATH}, \text{EVENPATH}$:

> $\text{PATH} = \{ \langle G,s,t,k \rangle : G \text{ es un digrafo con dos nodos s y t tales que hay un recorrido de longitud menor o igual a k de s a t} \}$
> 
> $\text{EVENPATH} = \{ \langle G,s,t,k \rangle: G \text{ es un digrafo con dos nodos s y t tales que hay un recorrido de longitud par y menor o igual a k de s a t} \}$
> 
> Dado un digrafo $G$, definimos $G'$ como el digrafo que tiene dos copias $(v,p)$ y $(v,i)$ de cada vértice $v∈V(G)$ donde $(v,x) →(w,y)$ es una arista de $G'$ si y solo si $v →w ∈E(G)$ y $x \neq y$.
>
> [a] Demostrar que $\langle G,s,t,k \rangle \in \text{EVENPATH} \iff \langle G',(s,p),(t,p),k \rangle \in \text{PATH}$ \
> [b] Mostrar que la reducción de EVENPATH a PATH implicada por el punto anterior es polinomial.

**[a]**

$\langle G, s, t, k \rangle \in \text{EVENPATH} \implies \langle G',(s,p),(t,p),k \rangle \in \text{PATH}$

$G'$ viaja con conexiones $(a,p) \rightarrow (b,i), (a,i) \rightarrow (b,p), \forall (a,b) \in E(G) (\iff (a,p) \rightarrow (b,i), (a,i) \rightarrow (b,p) \in E(G'\langle G',(s,p),(t,p),k \rangle \in \text{PATH}))$ 

Luego cada 2 aristas la segunda componente se repite. En particular, en $G$ el camino $s\rightarrow t$ tiene longitud par por $\langle G, s, t, k \rangle \in \text{EVENPATH}$, luego existe un camino $(s,p) \rightarrow (t,p)$ con la misma longitud, por lo tanto $\langle G',(s,p),(t,p),k \rangle \in \text{PATH}$

$\langle G',(s,p),(t,p),k \rangle \in \text{PATH} \implies \langle G, s, t, k \rangle \in \text{EVENPATH}$

$(s,p) \rightarrow^* (t,p) \in E(G') \iff s \rightarrow^* t \in E(G) \text{ para } \rightarrow^* \text{ de tamaño par}$

La premisa es que $\langle G',(s,p),(t,p),k \rangle \in \text{PATH}$ entonces el camino existe en $G'$ y tiene longitud $\leq k$. Como el camino existe entonces el camino original de $s$ a $t$ en $G$ tiene tamaño par ($2 | k$). Luego $\langle G, s, t, k \rangle \in \text{EVENPATH}$. $\square$

**[b]**

> $L \subseteq \{0,1\}^*$ es **Karp reducible polinomialmente** a $L' \subseteq \{0,1\}^*$, notado $L \leq_p L'$, si existe $f: \{0,1\}^* \to \{0,1\}^*$ computable en tiempo polinomial tal que $x \in L \iff f(x) \in L'$. $f$ se llama **reducción polinomial**; decimos $L \leq_p L'$ **vía** $f$.

La reducción polinomial la demuestro con la funcion $f: \langle G,s,t,k \rangle \rightarrow \langle G',(s,p),(t,p),k \rangle$. Para esto basta una $g: G \rightarrow G'$ que compute polinomialmente. Dado un $G$ es posible hacer esta transformación con esta función $g$ de forma polinomial segun la descripcion de la consigna. $\square$


### 6) Dados los lenguajes del enunciado ...

a) Demostrar que $\langle X \rangle \in \text{2-PARTITION} \iff \langle R,r1,...,r|X| \rangle \in \text{RECTANGLE PACKING}$

qvq $\langle X \rangle \in \text{2-PARTITION} \rightarrow \langle R,r1,...,r|X| \rangle \in \text{RECTANGLE PACKING}$

> Supongo $\langle X \rangle \in \text{2-P}$.
> $\langle X \rangle \in \text{2-PARTITION}$ implica que $X$ es un conconjunto finito de naturales tal que puede particionarse en dos $X_1$, $X_2$ disjuntos cuya suma es igual. \
> Sea $\sum_{x \in X_1} x = \sum_{x \in X_2} x = C \rightarrow \sum_{x \in X=X_1 \cup X_2} x = 2C$. \
> Defino a $R$ con base $\lfloor{\sum_{x \in X}x / 2} \rfloor$ y altura $2$, luego $\text{Área(R)}=\sum_{x \in X} x = 2C$. \
> Análogamente $r_i$ son rectangulos de altura $1$ y base $x_i$. \
> Ubicamos todos los rectángulos $r_i$ correspondientes a $x \in X_1$ uno al lado del otro en la "franja inferior" de $R$ (desde altura $y=0$ a $y=1$). Como su base total es $C$, cubren exactamente esa fila. \
> Luego como $\text{Area}(R) = \sum_{i=1}^{|X|}\text{Area}(r_i) =\sum_{i=1}^{|X|} r_i = \sum_{i=1}^{|X|} x_i = 2C$, entonces $\langle R, r_1, ..., r_{|X|}\rangle \in \text{RECTANGLE-PACKING}$ $\square$

qvq $\langle R,r1,...,r|X| \rangle \in \text{RECTANGLE PACKING} \rightarrow \langle X \rangle \in \text{2-PARTITION}$

> Supongo $\langle R, r_1, ..., r_{L}\rangle \in \text{RECTANGLE-PACKING}$. \
> Luego $\text{Area}(R) = \sum_i^{L} \text{Area}(r_i)$. \
> Defino $X: |X|=L \land x_i = \text{Area}(r_i) = r_i$. \
> Por construcción, la base de $R$ es $\lfloor \sum_{x \in X}x / 2 \rfloor$ y la altura $2$. \
> Quiero ver que existan dos subconjuntos de $x_i$ (o analogamente $r_i$) cuya suma $S$ sea igual y $\text{Area}(R) = 2S$. \
> En particular, la altura de $R$ es $2$ y cada $r_i$ tiene altura $1 \therefore$ hay dos rectangulos para cada fila cuya longitud debe ser igual $S$. \
> Defino $X_1 = \{r: r \in R_{inf} \}$ y $X_2 = \{r: r \in R_{sup} \}$. \
> $\sum_{x \in X_1} = \sum_{x \in X_2} = S$ por formar un rectangulo al solaparse uno sobre otro y $\sum_{x \in X_1} + \sum_{x \in X_2} = 2S = R$. $\square$

b) Demostrar $\langle X, t \rangle \in \text{3-PARTITION} \iff \langle R, r_1, ..., r_{|X|}\rangle \in \text{RECTANGLE PACKING}$

Sea $m = \frac{|X|}{3}$. Por definición: $R$ tiene base $m$ y altura $t + 3m$; cada $r_i$ tiene base $1$ y altura $m + x_i$.

**qvq** $\langle X, t \rangle \in \text{3-PARTITION} \rightarrow \langle R, r_1, ..., r_{|X|}\rangle \in \text{RECTANGLE PACKING}$

> Sup $\langle X, t \rangle \in \text{3-PARTITION}$. Entonces existen $m$ triplas $T_1, \ldots, T_m$ que particionan $X$, cada una con suma $t$. \
> \
> **Construcción del tiling:** para cada tripla $T_j = \{a_j, b_j, c_j\}$, apilamos verticalmente $r_{a_j}, r_{b_j}, r_{c_j}$ en la columna $j$ (posición horizontal $[j-1,\, j]$). \
> La altura total de cada pila es $(m+a_j)+(m+b_j)+(m+c_j) = 3m + t =$ altura de $R$. \
> Las $m$ columnas de ancho 1 cubren exactamente la base $m$ de $R$, sin superposición. \
> Luego $\langle R, r_1, ..., r_{|X|}\rangle \in \text{RECTANGLE PACKING}$. $\square$

**qvq** $\langle R, r_1, ..., r_{|X|}\rangle \in \text{RECTANGLE PACKING} \rightarrow \langle X, t \rangle \in \text{3-PARTITION}$

> Sup que existe un tiling válido de $R$ con los $r_i$. \
> \
> **Paso 1 — Sin rotaciones.** Como $x_i \geq 1$, la altura $m + x_i > m =$ base de $R$. Si $r_i$ fuese rotado, su base sería $m + x_i > m$, excediendo el ancho de $R$: no cabe. Luego ningún $r_i$ se rota. \
> \
> **Paso 2 — Alineación por columnas.** Como todas las dimensiones son naturales, WLOG las posiciones son enteras. Cada $r_i$ (base 1) ocupa exactamente una de las $m$ columnas $\{0, \ldots, m-1\}$. \
> \
> **Paso 3 — Cada columna tiene exactamente 3 rectángulos.** \
> Sea $S_j$ el conjunto de $r_i$ ubicados en la columna $j$ y $k_j = |S_j|$. Para que la columna quede completamente cubierta: \
> $\sum_{i \in S_j}(m + x_i) = t + 3m \;\implies\; \sum_{i \in S_j} x_i = t + (3 - k_j)\,m \quad (*)$ \
> *Nota: en este paso usamos $\max_{x \in X} x < \lfloor t/2 \rfloor$ como **hipótesis del input** $\langle X, t \rangle$ (es parte de la definición de 3-PARTITION), no como algo a demostrar. $X$ y $t$ son los mismos objetos fijos en ambas direcciones del bicondicional.* \
> Si $k_j < 3$: de $(*)$, $\sum_{i \in S_j} x_i \geq t + m > t$. Pero como $\max x < \lfloor t/2 \rfloor$ (hipótesis del input), $\sum_{i \in S_j} x_i < k_j \cdot \frac{t}{2} \leq 2 \cdot \frac{t}{2} = t$. Contradicción. \
> Si $k_j > 3$ para algún $j$: como $\sum_j k_j = |X| = 3m$ con $m$ columnas, algún $k_{j'} < 3$, lo cual es imposible por el caso anterior. Contradicción. \
> Luego $k_j = 3$ para todo $j$. \
> 
> **Paso 4 — Extracción de la 3-partición.** \
> De $(*)$ con $k_j = 3$: $\sum_{i \in S_j} x_i = t$. \
> Los conjuntos $\{ x_i : i \in S_j \}$ para $j = 1, \ldots, m$ particionan $X$ en $m$ triplas que suman $t$. \
> Luego $\langle X, t \rangle \in \text{3-PARTITION}$. $\square$

c) Mostrar que las reducciones implicadas por los puntos anteriores son polinomiales en función de los tamaños de las entradas

Una reducción de Karp $L \leq_p L'$ via $f$ requiere:
1. **Corrección:** $x \in L \iff f(x) \in L'$ — ya demostrado en 6a y 6b.
2. **Polinomialidad:** $f$ es computable en tiempo polinomial en $|x|$.

Solo resta mostrar el punto 2 para cada función. Sea $N$ el tamaño del input codificado en binario.

**Para $f_a: \langle X \rangle \mapsto \langle R, r_1, \ldots, r_{|X|} \rangle$**

> - Calcular $\lfloor \sum_{x \in X} x / 2 \rfloor$: sumar $n$ números cuya codificación total ocupa $N$ bits toma $O(N^2)$ operaciones de bit.
> - Escribir $R = \bigl(\lfloor \sum x_i / 2 \rfloor,\ 2\bigr)$: la suma es $\leq \sum x_i \leq 2^N$, cabe en $O(N)$ bits.
> - Escribir cada $r_i = (x_i,\ 1)$: copiar del input, $O(N)$ en total.
> - **Total:** $O(N^2)$, polinomial en $N$. $\square$

**Para $f_b: \langle X, t \rangle \mapsto \langle R, r_1, \ldots, r_{|X|} \rangle$**

> - Calcular $m = |X|/3$: trivial, $O(\log N)$.
> - Calcular $t + 3m$: una suma de números que caben en $O(N)$ bits, $O(N)$.
> - Escribir $R = (m,\ t + 3m)$: $O(N)$ bits.
> - Escribir cada $r_i = (1,\ m + x_i)$: una suma por elemento, $O(N)$ en total.
> - **Total:** $O(N)$, polinomial en $N$. $\square$

### 7. Explicar por qué la identidad no es una reducción polinomial de un lenguaje $Π$ a $Π^c$. Concluir que las nociones de NP y coNP son altamente sensibles a la “etiqueta” de la respuesta.

> Se dice que $L \leq_p L'$ si y solo si existe una $f$ computable en tiempo polinomial tal que $w \in L \iff f(w) \in L'$.

La identidad falla entre un lenguaje y su complemento para la identidad porque $w \in L \iff f(w)=w \in L^c$ es absurdo.

En $\text{coNP} = \{ L: L^c \in \text{NP}\}$, para probar que $L \in NP$ equivale ver $L^c \in \text{coNP}$.

Mostrar que $L \in \text{NP}$ es mediante un algoritmo $V$ con un certificado $u$ `V(u, *args)` para las instancias si. 
En cambio mostrar que $L^c \in \text{coNP}$ es mediante otro algoritmo + certificado para las instancias no (contraejemplo).

### 8. TODO

### 9. Sea $L \in \text{RECURSIVE}$. Probar que $L \leq_p \text{HALTING}$.

$L \in \text{RECURSIVE} \iff L \text{ es decidible}$.

Quiero hallar una $f$ computable polinomialmente tal que $x \in L \iff f(x) \in \text{HALTING}$

Es decir: $x \in L \implies f(x) \in \text{HALTING} \land x \notin L \implies f(x) \notin \text{HALTING}$.

Luego, defino f como:
```python
#_L_accepts(x) existe porque L in RECURSIVE.

def f(x):
	if _L_accepts(x): return 1
	while 1: continue
``` 

Esta definicion cumple lo pedido.


