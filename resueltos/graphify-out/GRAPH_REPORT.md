# Graph Report - .  (2026-04-22)

## Corpus Check
- Corpus is ~7,386 words - fits in a single context window. You may not need a graph.

## Summary
- 14 nodes · 20 edges · 3 communities detected
- Extraction: 85% EXTRACTED · 15% INFERRED · 0% AMBIGUOUS · INFERRED: 3 edges (avg confidence: 0.71)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Complexity Classes P and NP|Complexity Classes P and NP]]
- [[_COMMUNITY_Arithmetic Algorithms|Arithmetic Algorithms]]
- [[_COMMUNITY_Graph Algorithms|Graph Algorithms]]

## God Nodes (most connected - your core abstractions)
1. `Complexity Class P` - 7 edges
2. `Complexity Class NP` - 4 edges
3. `Practica 2` - 3 edges
4. `COPRIME Language` - 3 edges
5. `POWER Language` - 3 edges
6. `TREE Language` - 3 edges
7. `HAMPATH Language` - 3 edges
8. `Breadth-First Search (BFS)` - 3 edges
9. `Polynomial Time Complexity` - 3 edges
10. `Euclidean Algorithm (GCD)` - 2 edges

## Surprising Connections (you probably didn't know these)
- `Complexity Class P` --conceptually_related_to--> `COPRIME Language`  [EXTRACTED]
  resueltos.md → resueltos.md  _Bridges community 0 → community 1_
- `Complexity Class P` --conceptually_related_to--> `TREE Language`  [EXTRACTED]
  resueltos.md → resueltos.md  _Bridges community 0 → community 2_
- `Breadth-First Search (BFS)` --conceptually_related_to--> `Polynomial Time Complexity`  [EXTRACTED]
  resueltos.md → resueltos.md  _Bridges community 2 → community 1_

## Hyperedges (group relationships)
- **Languages Proven in P via Polynomial Algorithms** — resueltos_coprime, resueltos_power, resueltos_tree, resueltos_finite_language, resueltos_complexity_class_p [EXTRACTED 1.00]
- **Graph Problems Decided via BFS** — resueltos_tree, resueltos_hampath, resueltos_bfs [EXTRACTED 1.00]
- **NP Membership Proof via Certificate-Verifier** — resueltos_hampath, resueltos_np_certificate, resueltos_complexity_class_np [EXTRACTED 1.00]

## Communities

### Community 0 - "Complexity Classes P and NP"
Cohesion: 0.47
Nodes (6): Complexity Class NP, Complexity Class P, Finite Language in P, NP Certificate / Verifier, Closure of P under Union, Intersection, Complement, Practica 2

### Community 1 - "Arithmetic Algorithms"
Cohesion: 0.5
Nodes (5): Binary Exponentiation, COPRIME Language, Euclidean Algorithm (GCD), Polynomial Time Complexity, POWER Language

### Community 2 - "Graph Algorithms"
Cohesion: 1.0
Nodes (3): Breadth-First Search (BFS), HAMPATH Language, TREE Language

## Knowledge Gaps
- **2 isolated node(s):** `Finite Language in P`, `NP Certificate / Verifier`
  These have ≤1 connection - possible missing edges or undocumented components.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Complexity Class P` connect `Complexity Classes P and NP` to `Arithmetic Algorithms`, `Graph Algorithms`?**
  _High betweenness centrality (0.537) - this node is a cross-community bridge._
- **Why does `Complexity Class NP` connect `Complexity Classes P and NP` to `Graph Algorithms`?**
  _High betweenness centrality (0.210) - this node is a cross-community bridge._
- **Why does `COPRIME Language` connect `Arithmetic Algorithms` to `Complexity Classes P and NP`?**
  _High betweenness centrality (0.112) - this node is a cross-community bridge._
- **What connects `Finite Language in P`, `NP Certificate / Verifier` to the rest of the system?**
  _2 weakly-connected nodes found - possible documentation gaps or missing edges._