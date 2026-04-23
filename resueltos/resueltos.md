# Resueltos CC.

## Practica 2

### 1. Demostrar $L \in P$ para cada $L$

> Para esto debo construir algoritmos que decidan cada $L$ ($x\in L \lor x \notin L$) en tiempo polinomial.

a) $\text{COPRIME} = \{ <a,b>: (a:b) == 1 \} \in P$

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

En mcd hay como mucho n divisiones y todas toman O(n^2) -> luego mcd es O(n^3) y isCOPRIME tambien, entonces isCOPRIME \in P

b) $\text{POWER} = \{ <a,e,b>: a^e = b \}$

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

a tiene n bits (a ~ 2^n), entonces hay O(n) multiplicaciones y cada una toma O(n^2) analogamente a las divisiones


c) $\text{TREE} = \{<G>: G \text{ es un grafo conexo sin ciclos} \}$

**dem:** 
Un grafo es conexo sin ciclos si no vuelvo a visitar un nodo 2 
veces en un recorrido haciendo dfs/bfs desde algun nodo.

Para esto voy a hacer BFS desde cada nodo $(O(n^2))$.
Luego, TREE se computa en $O(n^2)$.

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
Esto es O(n*costo_comparar)


### 2) Probar que la clase P está cerrada por unión, intersección y complemento.

**dem:**

Supongo $L, L' \in P$, quiero ver que:

1. $L \cup L' \in P$,

> Trivialmente es validar $x \in L \lor x \in L'$, como ambos están en $P$, corre todo en tiempo polinomial.

2. $L \cap L' \in P$,

> Analogamente: `isLL'(x) = isL(X) && isL'(X)`

3. $L^c \in P$.

> Basta con `isL^c(x) = 1 - isL(x)`

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

b. $\text{CLIQUE} = \{ <G>: \text{ G es un grafo con subgrafo completo de tamaño mayor o igual a k} \}$

**dem:**
Debería haber un $V' \subset V_G, |V'|\geq k$ tal que todos sus nodos están conectados entre si.

Planteo que el certificado sea ese $u := V'$.

```c
#define k 100
typedef Node = int;

uint8_t verifykCLIQUE(G: Graph, u: [Node]){	

	if _length(u) < k: return 0;

	Node prev_node = u[0]; 
	foreach (Node inode in u){
		if (! _contains_node(G, node)): return 0;		

		foreach (Node jnode in u) {
			if (inode == jnode): continue;
			if (G.edges[inode][jnode] == 0): return 0;
		}
	}

	return 1;	
}
```
Esto corre en $O(n^2)$ luego $\text{k-CLIQUE} \in NP$.

c. $\text{CLIQUE} = \{ <G, k>: \text{ G es un grafo con subgrafo completo de tamaño mayor o igual a k} \}$

**dem:**
El algoritmo es análogo al anterior, mismo certificado pero ahora el input tiene a $<G,k>$ y no solo a $G$.
```c
typedef Node = int;

uint8_t verifykCLIQUE(G: Graph, k: int, u: [Node]){     

        if _length(u) < k: return 0;

        Node prev_node = u[0]; 
        foreach (Node inode in u){
                if (! _contains_node(G, node)): return 0;               

                foreach (Node jnode in u) {
                        if (inode == jnode): continue;
                        if (G.edges[inode][jnode] == 0): return 0;
                }
        }

        return 1;       
}
```

d. $\text{k-COLORING} = \{⟨G⟩ : \text{G es un grafo que se puede particionar en k conjuntos indepenientes} \}$

**dem:**
Deben haber k grupos sin aristas entre si.

$u = \text{ S lista de grupos de nodos}$

```python

def _check_group_is_in_graph(group: [Node], G: Graph):
	for node 


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

Luego $O(n^2) \therefore L \in NP$ 

e. $\text{ISOMORPHISM} = \{⟨G,H⟩: \text{G y H son dos grafos isomorfos}\}$

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

g. $¬\text{SAT} = \{⟨φ⟩: ¬φ \text{ es satisfacible}\}$
