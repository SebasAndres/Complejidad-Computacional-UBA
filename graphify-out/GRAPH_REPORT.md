# Graph Report - .  (2026-04-22)

## Corpus Check
- Corpus is ~17,778 words - fits in a single context window. You may not need a graph.

## Summary
- 147 nodes · 147 edges · 30 communities detected
- Extraction: 86% EXTRACTED · 14% INFERRED · 0% AMBIGUOUS · INFERRED: 20 edges (avg confidence: 0.83)
- Token cost: 28,300 input · 6,000 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Complexity Classes & Time Bounds|Complexity Classes & Time Bounds]]
- [[_COMMUNITY_NP-Completeness & Reductions|NP-Completeness & Reductions]]
- [[_COMMUNITY_TM Variants & Cook-Levin Proof|TM Variants & Cook-Levin Proof]]
- [[_COMMUNITY_TM Encoding & Binary Representation|TM Encoding & Binary Representation]]
- [[_COMMUNITY_TM Configuration & Computation|TM Configuration & Computation]]
- [[_COMMUNITY_Formal TM Definition|Formal TM Definition]]
- [[_COMMUNITY_P vs NP Core|P vs NP Core]]
- [[_COMMUNITY_NP via NDTime|NP via NDTime]]
- [[_COMMUNITY_Hierarchy Theorem & Diagonalization|Hierarchy Theorem & Diagonalization]]
- [[_COMMUNITY_Turing Machine Computable Functions|Turing Machine Computable Functions]]
- [[_COMMUNITY_Time Hierarchy Separation|Time Hierarchy Separation]]
- [[_COMMUNITY_Binary Representations|Binary Representations]]
- [[_COMMUNITY_Decision Problems & Languages|Decision Problems & Languages]]
- [[_COMMUNITY_Uncomputability|Uncomputability]]
- [[_COMMUNITY_Graph Optimization Problems|Graph Optimization Problems]]
- [[_COMMUNITY_Non-Deterministic Machines|Non-Deterministic Machines]]
- [[_COMMUNITY_Polynomial Reducibility|Polynomial Reducibility]]
- [[_COMMUNITY_PSPACE & Space Complexity|PSPACE & Space Complexity]]
- [[_COMMUNITY_Polynomial Hierarchy|Polynomial Hierarchy]]
- [[_COMMUNITY_Boolean Circuits|Boolean Circuits]]
- [[_COMMUNITY_Alphabet|Alphabet]]
- [[_COMMUNITY_Strings & Words|Strings & Words]]
- [[_COMMUNITY_Bi-Infinite Tape TM|Bi-Infinite Tape TM]]
- [[_COMMUNITY_Universal NTM|Universal NTM]]
- [[_COMMUNITY_Propositional Logic|Propositional Logic]]
- [[_COMMUNITY_Knapsack Problem|Knapsack Problem]]
- [[_COMMUNITY_Course Introduction|Course Introduction]]
- [[_COMMUNITY_Space Complexity (PSPACENLL)|Space Complexity (PSPACE/NL/L)]]
- [[_COMMUNITY_Polynomial Hierarchy (cap.7)|Polynomial Hierarchy (cap.7)]]
- [[_COMMUNITY_Boolean Circuits (cap.8)|Boolean Circuits (cap.8)]]

## God Nodes (most connected - your core abstractions)
1. `Clase P (tiempo polinomial determinístico)` - 9 edges
2. `Clase NP (definición por verificador)` - 9 edges
3. `Complejidad Computacional UBA [1c-2026]` - 7 edges
4. `Máquina de Turing (MT)` - 6 edges
5. `Problema SAT` - 6 edges
6. `Transition function δ: Q x Σ^(k-1) → {L,R,S} x Σ^(k-2) x {L,R,S}^(k-2) x (Σ∪{S}) x Q` - 6 edges
7. `Máquinas no-determinísticas` - 5 edges
8. `NP = unión de NDTime(n^c) — definición alternativa` - 5 edges
9. `Transition Function δ(q, 1, □) = (L, 1, R, 0, s)` - 5 edges
10. `Encoding of configuration tuple v = (E, t1, ..., tk-2, T1, ..., Tk-2, Z, q)` - 5 edges

## Surprising Connections (you probably didn't know these)
- `Problema CON (conectividad de grafos)` --semantically_similar_to--> `TREE ∈ P (BFS en grafos)`  [INFERRED] [semantically similar]
  apuntes/03_Halt_y_Clases_P_NP.md → resueltos/practica2.md
- `Práctica 2: Lenguajes en NP (HAMPATH, CLIQUE, COLORING, ISOMORPHISM)` --references--> `NP = unión de NDTime(n^c) — definición alternativa`  [INFERRED]
  practicas/practica_2_p_y_np.pdf → teoricas/clase4.pdf
- `Apunte CC: Tiempo polinomial, P, NP (cap.3)` --conceptually_related_to--> `NP = unión de NDTime(n^c) — definición alternativa`  [INFERRED]
  apunte CC.pdf → teoricas/clase4.pdf
- `Máquina no-determinística (NTM)` --semantically_similar_to--> `Máquina de Turing (MT)`  [INFERRED] [semantically similar]
  apuntes/04_NTM_NP_Logica_Proposicional.md → apuntes/01_Representaciones_Binario_e_Intro_MT.md
- `COPRIME ∈ P (algoritmo de Euclides)` --references--> `Clase P (tiempo polinomial determinístico)`  [EXTRACTED]
  resueltos/practica2.md → apuntes/03_Halt_y_Clases_P_NP.md

## Hyperedges (group relationships)
- **Two equivalent characterizations of NP: certificate/verifier and NTM** — apunte03_clase_np, apunte04_ntm, apunte04_equivalencia_np [EXTRACTED 0.95]
- **Cook-Levin proof pipeline: oblivious MT + mini-configurations + CNF encoding → SAT NP-hard** — apunte02_mt_oblivious, apunte05_mini_configuracion, apunte05_cook_levin [EXTRACTED 0.97]
- **Core NP-complete problems related by polynomial reductions: SAT, 3SAT, INDSET** — apunte05_sat_np_completo, apunte05_3sat_np_completo, apunte05_indset_np_completo [EXTRACTED 0.93]
- **Prueba Cook-Levin: mini-configuraciones + oblivious TM + CNF → SAT es NP-hard** — clase5_mini_configuraciones, clase5_maquina_oblivious, clase5_formula_cnf, clase5_sat_np_hard [EXTRACTED 0.95]
- **Equivalencia definición NP: verificador polinomial ↔ NDTime(n^c) ↔ árbol de cómputos** — clase4_np_alternativa_ndtime, clase4_ndtime, clase4_arbol_computos [EXTRACTED 0.92]
- **Jerarquía determinística: o-chica + re-codificación + diagonalización → DTime(f) ⊊ DTime(g)** — clase6_notacion_o_chica, clase6_recodificacion_maquinas, clase6_diagonalizacion, clase6_teorema_jerarquia_det [EXTRACTED 0.90]

## Communities

### Community 0 - "Complexity Classes & Time Bounds"
Cohesion: 0.1
Nodes (26): Notación asintótica O, Ω, Θ, o, ω, Tiempo de cómputo T(n), Tiempo polinomial, Certificado (testigo para NP), Clase NP (definición por verificador), Clase P (tiempo polinomial determinístico), Problema CON (conectividad de grafos), Clase DTime(T(n)) (+18 more)

### Community 1 - "NP-Completeness & Reductions"
Cohesion: 0.12
Nodes (19): Apunte CC: Reducción polinomial y NP-completos (cap.4), Lógica proposicional, Reducibilidad polinomial (≤_p), La clase coNP, Las clases ExpTime y NExpTime, Fórmula booleana en CNF (φ_F), Función F: evolución en un paso (codificación CNF), Máquina oblivious (+11 more)

### Community 2 - "TM Variants & Cook-Levin Proof"
Cohesion: 0.19
Nodes (14): MT de cinta única, Máquina oblivious, Problema INDSET (conjunto independiente), 3CNF, Problema 3SAT, Forma Normal Conjuntiva (CNF), Problema SAT, Satisfacibilidad de fórmulas (+6 more)

### Community 3 - "TM Encoding & Binary Representation"
Cohesion: 0.24
Nodes (13): Binary encoding ⟨v⟩ = ⟨[E], [t1], ..., [tk-2], [T1], ..., [Tk-2], [Z], [q]⟩ ∈ {0,1}*, Encoding ⟨δ⟩ of transition function as binary string in {0,1}*, Transition function δ: Q x Σ^(k-1) → {L,R,S} x Σ^(k-2) x {L,R,S}^(k-2) x (Σ∪{S}) x Q, Encoding of configuration tuple v = (E, t1, ..., tk-2, T1, ..., Tk-2, Z, q), Entrada (input) component {L, R, S} x Σ^(k-2), Multi-tape Turing Machine (k tapes), Salida (output) component (Σ ∪ {S}) x Q, Trabajo (work/tape) component {L, R, S}^(k-2) (+5 more)

### Community 4 - "TM Configuration & Computation"
Cohesion: 0.17
Nodes (12): Cómputo de MT, Configuración de MT, Función de transición δ, Máquina de Turing (MT), MT con 3 cintas, Codificación de máquinas ⟨M⟩, Función computable, Función parcial computable (+4 more)

### Community 5 - "Formal TM Definition"
Cohesion: 0.22
Nodes (9): Función de transición δ de TM, Máquina determinística (definición formal), Árbol de cómputos de máquina no-determinística, Cómputo aceptador (non-deterministic), Configuración final de máquina no-determinística, Lenguaje aceptado por máquina no-determinística, Máquinas no-determinísticas, Simulación determinística de máquina no-determinística (+1 more)

### Community 6 - "P vs NP Core"
Cohesion: 0.25
Nodes (8): La clase NP, La clase P, Complejidad Computacional UBA [1c-2026], La clase coNP, Teorema de Cook-Levin, Las clases EXPTIME y NEXPTIME, Máquinas de Turing, Problemas NP-completos

### Community 7 - "NP via NDTime"
Cohesion: 0.25
Nodes (8): Apunte CC: Tiempo polinomial, P, NP (cap.3), Clase NDTime(T(n)), NP = unión de NDTime(n^c) — definición alternativa, Prueba NP ⊆ ∪NDTime(n^c) via verificador determinístico, Tiempo de cómputo de máquina no-determinística T(n), Práctica 2: Lenguajes en NP (HAMPATH, CLIQUE, COLORING, ISOMORPHISM), Práctica 2: Lenguajes en P (COPRIME, POWER, TREE), Práctica 2: NP ⊆ RECURSIVE, HALTING ∉ NP

### Community 8 - "Hierarchy Theorem & Diagonalization"
Cohesion: 0.29
Nodes (8): Diagonalización para separar clases de complejidad, Máquina universal U (para jerarquía), Notación 'o chica' f=o(g), Conjetura NP ≠ coNP, Re-codificación de máquinas determinísticas (índices múltiples), Teorema jerarquía determinística: DTime(f(n)) ⊊ DTime(g(n)), Práctica 1: Órdenes de crecimiento (O, o, Ω, Θ), Rationale: re-codificar máquinas con infinitos índices permite que D se diferencie de todas las M_i en tiempo f(n)·log f(n)

### Community 9 - "Turing Machine Computable Functions"
Cohesion: 0.5
Nodes (4): Apunte CC: Configuración inicial y final de TM, Apunte CC: Funciones computables y funciones parciales, Apunte CC: Máquinas y cómputos (cap.2), Práctica 1: Modelos de cómputo (variantes de TM)

### Community 10 - "Time Hierarchy Separation"
Cohesion: 0.67
Nodes (3): Apunte CC: Separación de clases de complejidad (cap.5), Jerarquía de tiempos determinísticos, Jerarquía de tiempos no-determinísticos

### Community 11 - "Binary Representations"
Cohesion: 1.0
Nodes (2): Codificación autodelimitante de cadenas, Representación de objetos en binario

### Community 12 - "Decision Problems & Languages"
Cohesion: 1.0
Nodes (2): Lenguaje (L ⊆ {0,1}*), Problema de decisión (función booleana)

### Community 13 - "Uncomputability"
Cohesion: 1.0
Nodes (2): Funciones no computables, Numerabilidad de máquinas y funciones computables

### Community 14 - "Graph Optimization Problems"
Cohesion: 1.0
Nodes (2): Problema CAMHAM (camino hamiltoniano), Problema TSP (travelling salesman)

### Community 15 - "Non-Deterministic Machines"
Cohesion: 1.0
Nodes (1): Máquinas no-determinísticas

### Community 16 - "Polynomial Reducibility"
Cohesion: 1.0
Nodes (1): Reducibilidad polinomial

### Community 17 - "PSPACE & Space Complexity"
Cohesion: 1.0
Nodes (1): Espacio polinomial: PSPACE y NPSPACE

### Community 18 - "Polynomial Hierarchy"
Cohesion: 1.0
Nodes (1): La jerarquía polinomial

### Community 19 - "Boolean Circuits"
Cohesion: 1.0
Nodes (1): Circuitos booleanos

### Community 20 - "Alphabet"
Cohesion: 1.0
Nodes (1): Alfabeto (Γ)

### Community 21 - "Strings & Words"
Cohesion: 1.0
Nodes (1): Palabras y cadenas binarias (Γ*)

### Community 22 - "Bi-Infinite Tape TM"
Cohesion: 1.0
Nodes (1): MT con cintas bi-infinitas

### Community 23 - "Universal NTM"
Cohesion: 1.0
Nodes (1): NTM universal NU

### Community 24 - "Propositional Logic"
Cohesion: 1.0
Nodes (1): Lógica proposicional (fórmulas booleanas)

### Community 25 - "Knapsack Problem"
Cohesion: 1.0
Nodes (1): Problema KNAPSACK (mochila)

### Community 26 - "Course Introduction"
Cohesion: 1.0
Nodes (1): Apunte CC: Introducción y notación

### Community 27 - "Space Complexity (PSPACE/NL/L)"
Cohesion: 1.0
Nodes (1): Apunte CC: Espacio (PSpace, NL, L) (cap.6)

### Community 28 - "Polynomial Hierarchy (cap.7)"
Cohesion: 1.0
Nodes (1): Apunte CC: Jerarquía polinomial (cap.7)

### Community 29 - "Boolean Circuits (cap.8)"
Cohesion: 1.0
Nodes (1): Apunte CC: Circuitos booleanos (cap.8)

## Knowledge Gaps
- **62 isolated node(s):** `La clase P`, `La clase NP`, `Máquinas de Turing`, `Máquinas no-determinísticas`, `Reducibilidad polinomial` (+57 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `Binary Representations`** (2 nodes): `Codificación autodelimitante de cadenas`, `Representación de objetos en binario`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Decision Problems & Languages`** (2 nodes): `Lenguaje (L ⊆ {0,1}*)`, `Problema de decisión (función booleana)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Uncomputability`** (2 nodes): `Funciones no computables`, `Numerabilidad de máquinas y funciones computables`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Graph Optimization Problems`** (2 nodes): `Problema CAMHAM (camino hamiltoniano)`, `Problema TSP (travelling salesman)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Non-Deterministic Machines`** (1 nodes): `Máquinas no-determinísticas`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Polynomial Reducibility`** (1 nodes): `Reducibilidad polinomial`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `PSPACE & Space Complexity`** (1 nodes): `Espacio polinomial: PSPACE y NPSPACE`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Polynomial Hierarchy`** (1 nodes): `La jerarquía polinomial`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Boolean Circuits`** (1 nodes): `Circuitos booleanos`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Alphabet`** (1 nodes): `Alfabeto (Γ)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Strings & Words`** (1 nodes): `Palabras y cadenas binarias (Γ*)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Bi-Infinite Tape TM`** (1 nodes): `MT con cintas bi-infinitas`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Universal NTM`** (1 nodes): `NTM universal NU`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Propositional Logic`** (1 nodes): `Lógica proposicional (fórmulas booleanas)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Knapsack Problem`** (1 nodes): `Problema KNAPSACK (mochila)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Course Introduction`** (1 nodes): `Apunte CC: Introducción y notación`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Space Complexity (PSPACE/NL/L)`** (1 nodes): `Apunte CC: Espacio (PSpace, NL, L) (cap.6)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Polynomial Hierarchy (cap.7)`** (1 nodes): `Apunte CC: Jerarquía polinomial (cap.7)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Boolean Circuits (cap.8)`** (1 nodes): `Apunte CC: Circuitos booleanos (cap.8)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Clase NP (definición por verificador)` connect `Complexity Classes & Time Bounds` to `TM Variants & Cook-Levin Proof`?**
  _High betweenness centrality (0.073) - this node is a cross-community bridge._
- **Why does `Problema SAT` connect `TM Variants & Cook-Levin Proof` to `Complexity Classes & Time Bounds`?**
  _High betweenness centrality (0.066) - this node is a cross-community bridge._
- **What connects `La clase P`, `La clase NP`, `Máquinas de Turing` to the rest of the system?**
  _62 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Complexity Classes & Time Bounds` be split into smaller, more focused modules?**
  _Cohesion score 0.1 - nodes in this community are weakly interconnected._
- **Should `NP-Completeness & Reductions` be split into smaller, more focused modules?**
  _Cohesion score 0.12 - nodes in this community are weakly interconnected._