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

