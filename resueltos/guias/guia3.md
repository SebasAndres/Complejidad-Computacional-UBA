## Práctica 3

### <u>1. Determinar V o F y demostrar. </u>

- a. $P \subset NP$ y $P \subset coNP$

> Vale que $P \subset NP$ porque puedo definir $M_{NP}(\langle x, u\rangle) := M_P(x)$ (ultra abuso de notación!!!!).
> 
> $P \subset coNP = \{ L^c : L \in NP \}$ solo vale si $L \in P \iff L^c \in NP$. Luego esto vale porque $L \in P \iff L^c \in P \subset NP$
>
> $\therefore \text{ La afirmación es Verdadera } \square$

- b. Si P = NP, entonces coNP = NP

> Quiero ver que $coNP = \{ L^c : L \in NP \} = NP$ asumiendo $P=NP$. 
> 
> Esto equivale a querer ver que $L \in NP \iff L^c \in NP$. 
> $L \in NP$ implica que existe una máquina determinísta $M$ tal que existe un certificado de tamaño polinomial al tamaño de cualquier entrada que permite decidir el lenguaje computando $M(\langle x, u\rangle)$.
> 
> Para definir $L^c$, en este caso no puedo validar $x \notin L$ como negación de $M(\langle x, u\rangle) == 0$, pues depende del certificado dado. Entonces tengo dos alternativas:
> 
> - i. Probar para todos los certificados posibles (aunque no puedo hacerlo en tiempo polinomial $2^{p(|x|)}$)
> - ii. Usar que P=NP. Como P=NP entonces para todo $L \in NP$ existe una $M$ que decide a $L$ en tiempo polinomial solo pasandole como entrada $x$. Luego probamos que $P = coP = coNP = NP$...
> 
> Vale que $P = coP = \{ L^c : L \in P \}$ solo si para todo $L \in P \iff L^c \in P$. Esto es cierto pues si $L \in P$, entonces existe una máquina determinista $M$ que corre en tiempo polinomial que decide $L$. Luego $x \in L$ se computa en tiempo polinomial. Entonces $x \notin L$ (o en síntesis $L^c$) equivale a computar $M'(x) := M(x)==0$, entonces $\forall L \in P, L^c \in P$. 
> 
> Entonces puedo concluir $P = NP \rightarrow coNP = NP$ 
> $\therefore \text{ La afirmación es Verdadera } \square$

- c. Si P = NP, entonces todos los lenguajes pertenecen a P
> Esta pregunta equivale a decir que todos los lenguajes están en $P$ o en $NP$. 
> Esto es falso, pues el lenguaje $HALT$ no está ni en $P$ ni en $NP$.
> $\therefore \text{ La afirmación es Falsa } \square$

- d. Si $coNP = NP$, entonces $SAT ∈ coNP$
> Equivale a ver que $SAT \in NP$. Esto es cierto, ya que podemos evaluar cualquier formula $\psi$ en tiempo polinomial pasandole como certificado $u$ la valuación de la misma $v : \text{Prop}^k \rightarrow \{0,1\}^k$ que nos permite ver que $x \in SAT$ (si es que lo está). 
> $\therefore \text{ La afirmación es Verdadera } \square$

- e. Si $coNP ⊆ NP$, entonces $NP = coNP$.
> Vale $\{L^c, \forall L \in NP\} \subset NP$.
> En principio, por cardinalidad $|coNP| = |NP|$, 
> por premisa $(\forall L \in NP), L^c \in NP \rightarrow L \in NP$
> En particular, es trivial que $L \in NP$ porque lo uso para la construcción de $coNP$,
> Entonces es un $\iff$...
> $L^c \in NP \iff L \in NP$
>
> $\therefore \text{ La afirmación es Verdadera } \square$


### 2. Es cierto que si dos lenguajes $Π$ y $Γ$ pertenecen a $NP$ entonces $Π ≤_p Γ$, y también $Γ ≤_p Π$? Justificar

> Se que $L \in \text{NP-completo} \implies ((\forall L' \in NP) L' \leq_p L)$. 
> Luego $\Gamma, \Pi \in \text{NP-completo} \implies (\Gamma \leq_p \Pi \land \Pi \leq_p \Gamma)$.
> 
> Voy a demostrar que no todo lenguaje en NP es NP-completo con un contraejemplo.
> $L_1 = \empty, L_2 = \{ 1 \}$
> $L_2 \leq_p L_1 \implies x \in L_2 \iff f(x) \in L_1$
>
> En este caso $1 \in L_2$ pero $\forall f. f(1) \notin L_1$, luego no vale $L_2 \leq_p L_1 \square$.

### 3. Sean $Π$ y $Γ$ dos lenguajes tales que $Π ≤_p Γ$. ¿Qué se puede inferir?

$$Π ≤_p Γ \iff (x \in \Pi \implies f(x) \in \Gamma), f \text{ computable en tiempo polinomial para todo }x$$

a. Si $Π∈P$ entonces $Γ∈P$
> Falso.
> $\Pi \in P \implies \exists M \text{ computable en tiempo polinomial tal que } \forall M(x) = 1 \iff x \in \Pi$ 
> Luego existe la función que reduce polinomialmente $\Pi \leq_p \Gamma$, entonces solo se que si computo $\Gamma$ puedo computar $\Pi$ en un orden polinomialmente similar. Entonces no puedo afirmar esto.

b. Si $Γ∈P$ entonces $Π∈P$.
> Verdadero.
> $\Gamma \in P \implies \exists M \text{ computable en tiempo polinomial tal que } \forall M(x) = 1 \iff x \in \Gamma$. Luego puedo validar $x \in \Gamma$ computando $M(f(x))$, lo cual es polinomial por las asunciones previas.

c. Si $Γ ∈ NPC$ entonces $Π ∈ NPC$
> Falso.
> $\forall L, L \leq_p \Gamma \in NPC$ 

d. Si $\Pi ∈ NPC$ entonces $\Gamma ∈ NPC$
> Falso.
> $\Pi \in NPC \iff (\forall L \in NP) \, L \leq_p \Pi \land \Pi \in NP$ 
> **Si vale que $\Gamma \in NP$** entonces como $(\forall L \in NP) \, L \leq_p \Pi$, por transitividad todo $(\forall L \in NP) \, L \leq_p \Gamma$. Luego $\Gamma \in NPC$.
> **¿Vale $\Gamma \in NP$? No necesariamente, entonces es falso.**

e. Si $Γ∈NPC$ y $Π∈NP$ entonces $Π∈NPC$
> Falso. 
> Contraejemplo: $\Pi = \empty \in NP$ y $\Gamma \in NPC$.
> $\Pi \leq_p \Gamma$ pero no $\empty$ no es $NPHard$.

f. Si $Π∈NPC$ y $Γ∈NP$ entonces $Γ∈NPC$
> Verdadero. 
> {...} **Si vale que $\Gamma \in NP$** entonces como $(\forall L \in NP) \, L \leq_p \Pi$, por transitividad todo $(\forall L \in NP) \, L \leq_p \Gamma$. Luego $\Gamma \in NPC$.


g. $Π$ y $Γ$ no pueden pertenecer ambos a $NPC$
> Falso.

## 4. Decir si las siguientes afirmaciones son verdaderas o falsas

a. Si P=NP, entonces todo problema NP-completo es polinomial

- Si, porque $L \in NPC \iff L\in NP \land L \in NPHard$. Como $NP=P \rightarrow L \in NP \iff L \in P \square$

b. Si $P=NP$, entonces todo problema NP-hard es polinomial.

- No, porque $halt \in NPHard$ pero $halt \notin NP$ (y entonces $halt \notin P$). 

c. Si las clases NP-completo y coNP-completo son disjuntas entonces $P \neq NP$.

- Supongo que $P=NP$ quiero ver que $NPC \cap coNPC = \empty$.

> Si $P=NP$ entonces $NP=NPC$ pues $(\forall L \in NP) \, L \in NPC$ pues $(\forall W \in P) \, W \leq_p L$. 
> Luego, $coNPC = \{ W^c : W \in NPC \} = \{ W^c: W \in NP\} = coNP$. 
> Como asumimos $P = NP$, entonces $coP = coNP$.
> Llego a que $P=coP \land coP = coNP \implies P=NP=coNP$ .
> Entonces, $L \in NP \iff L \in coNP$
> O equivalentemente en este caso,
> $L \in NPC \iff L \in coNPC$
> $\therefore NPC \cap coNPC \neq \empty \, \square$ 


## 5. Suponiendo que $P = NP$, diseñar un algoritmo polinomial que dada una fórmula booleana φ encuentre una asignación que la satizfaga, si es que φ es satisfacible

#### Intento 1: Está mal, es exponencial
~~~python
def findValuation(phi: any):
    if not isSAT(phi): # computa en P
        return None

    # generar y evaluar cada valuacion posible de phi
    # hasta terminar o encontrar una que satisfaga phi
    i = 0
    for val in _generate_next_eval(phi.nvars, i):
        if phi(val) == 1: 
            return val 

    return None

def _generate_next_eval(nvars, iter):
    val = np.zeros(nvars)
    val += bin(iter)
    return val
~~~

#### Intento 2.
~~~python

def findValuation(phi):
    # Si la fórmula completa no es satisfacible, cortamos rápido
    if not isSAT(phi):
        return None
        
    valuation = {}
    
    # Iteramos solo n veces (una por cada variable)
    for var in phi.variables:
        # 1. Probamos asignarle True a la variable actual
        # phi_con_true es la fórmula phi pero reemplazando 'var' por True
        phi_con_true = phi.assign(var, True) 
        
        # 2. Consultamos si el resto de la fórmula sobrevive a esta asignación
        if isSAT(phi_con_true):
            valuation[var] = True
            phi = phi_con_true # Actualizamos la fórmula para la siguiente iteración
        else:
            # Si asignar True la hace insatisfacible, obligatoriamente debe ser False
            # (Sabemos que al menos un camino es válido porque isSAT(phi) original dio True)
            valuation[var] = False
            phi = phi.assign(var, False)
            
    return valuation
~~~


## 6. Suponiendo que P = NP, diseñar un algoritmo polinomial que dado un grafo G retorne una clique de tamaño máximo de G

~~~python
def findClique(G):
    # Fase 1
    # hasta N llamadas a hasClique : O(N*p(N))
    k_max = 0
    for k in range(len(G.nodes), 0, -1):
        if hasClique(G, k): # P = NP --> se computa en P
            k_max = k
            break
    return k_max

    # Fase 2
    # hasta N llamadas a hasClique : O(N*p(N))
    clique_graph = G.copy()
    for node in G.nodes:
        if len(clique_graph) == k_max:
            break
        temp_graph = clique_graph.copy()
        temp_graph.remove(node)
        if hasClique(temp_graph, k): # P
           clique_graph.remove(node) 
    return clique_graph
~~~

## 7. Sabiendo que CLIQUE es NP-completo, demostrar que SUBGRAPH ISOMORPHISM es NP- completo.

$SI = \text{SUBGRAPH ISOMORPHISM} = \{ \langle G, H \rangle: \text {Existe un subgrafo de G isomorfo a H} \} \\ 
= \{ \langle G, H \rangle: \exists f \text{ inyectiva}: \forall (u,v) \in E(H) \implies (f(u), f(v)) \in E(G)\}$

Tengo que demostrar que $SI \in NPC$, para esto basta con ver que $SI \in NP \land CLIQUE \leq_p SI$...

$SI \in NP$ pues puedo definir:

$$M(\langle G, H, f \rangle) := 1 * (\forall (u,v) \in E(H): (f(u), f(v)) \in E(G)) \land (\forall u, v \in V(H): u \neq v \implies f(u) \neq f(v))$$

la cual valida la condicion en tiempo polinomial para $f$ la traducción del nodo en $H$ al de $G$.

Ahora quiero ver que $CLIQUE \leq_p SI$...

Esto equivale a ver que $\exists f/ \forall \langle G,k \rangle \, \in CLIQUE \iff f( \langle G,k \rangle) \in SI$

$f: Graph \times Int \rightarrow Graph \times Graph$

**Prop:** Si $G$ tiene una cliqué de tamaño $k$, entonces $\langle G, \texttt{generarClique(k)} \rangle \in SI$, pues cualquier cliqué de tamaño $k$ es isomorfa a otra cliqué de igual tamaño.

Luego defino $f(G, k) := \langle G, \texttt{generarClique(k)} \rangle$.

Donde $\texttt{generarClique(k) := ([1..k], [(x,y) for x in [1..k] for y in [1..k]])}$. En su defecto puede ser $E$ una matriz de adyacencia de $k \times k$ de todos unos.

Esta función cuesta tiempo polinomial respecto a $\langle G,k \rangle$ pues es $O(k^2)$

Luego quedo demostrado que $SI \in NPC \, \square$.