# Symmetry Reduction in combinatorial optimization

This repository explores the application of symmetry reduction techniques to combinatorial optimization (CO) problems. Many such problems exhibit structural symmetries, that is, transformations of the solution space that preserve both feasibility and objective value. The presence of symmetry partitions the feasible region into equivalence classes called orbits, where all solutions within an orbit share the same objective value. From an optimization perspective, exploring multiple solutions in the same orbit is redundant, and identifying a single canonical representative per orbit suffices.

The notebooks in this repository present classical combinatorial optimization problems formulated as integer linear programs, analyze their symmetry structures, and apply symmetry reduction techniques to decrease the effective solution space. The goal is to illustrate how exploiting symmetry can reduce computational effort in solution enumeration and analysis.

This repository is intended as a pedagogical resource and a foundation for extending these techniques to other combinatorial problems.

## Repository Structure

```
symmetry-reduction-CO/
├── README.md
├── CO_problems_notebooks/
│   ├── shortest_path.ipynb
│   ├── graph_coloring.ipynb
│   ├── max_cut.ipynb
│   └── traveling_salesman.ipynb
└── references/
    └── bibliography.bib
```

## Notebooks Overview

- **shortest_path.ipynb:** Applies *static lexicographic symmetry breaking* to the shortest path problem on undirected graphs. Presents the ILP formulation with flow conservation constraints, introduces graph automorphisms and solution orbits, and implements lexicographic ordering constraints over symmetric nodes adjacent to the source. Two examples are developed: a diamond graph (4 nodes, |Aut(G)| = 2) and a symmetric ladder graph (8 nodes, Aut(G) ≅ ℤ₂×ℤ₂×ℤ₂). Solution enumeration is performed with and without symmetry breaking to quantify the reduction in equivalent optimal solutions.

- **graph_coloring.ipynb:** Applies *static lexicographic symmetry breaking* to the graph coloring problem, where the goal is to assign colors to vertices such that no two adjacent vertices share the same color. This problem exhibits two independent symmetry sources: color permutation symmetry (any relabeling of colors yields an equivalent solution, generating k! redundant solutions for chromatic number k) and vertex symmetry induced by graph automorphisms. Lexicographic ordering constraints on color activation variables are used to eliminate redundant colorings.

- **max_cut.ipynb:** Applies *symmetry breaking by variable fixing* to the maximum cut problem, where the goal is to partition the vertices of a graph into two sets such that the number of edges between the sets is maximized. The problem exhibits a **flip symmetry**: any cut \(S\) and its complement \(\bar{S}\) produce the same objective value, generating pairs of equivalent optimal solutions. A symmetry breaking constraint is introduced by fixing the partition assignment of a reference vertex (e.g., \(z_1 = 0\)), eliminating redundant symmetric solutions while preserving optimality. A complete example on the graph \(K_4\) illustrates the ILP formulation, the symmetry structure of the solution space, and the reduction in equivalent optimal cuts obtained after symmetry breaking.

- **traveling_salesman.ipynb:** Applies *symmetry breaking by arc fixing* to the traveling salesman problem, where a salesman must visit each city exactly once and return to the starting city with minimum total cost. The problem exhibits **dihedral symmetry** $D_n$: any tour can be represented in $n$ rotations and $2$ directions of traversal,
generating $2n$ equivalent directed representations per essentially distinct tour. The MTZ (Miller-Tucker-Zemlin) ILP formulation is presented with subtour elimination constraints, and a single arc-fixing constraint ($x_{12} = 1$) is introduced to break both rotational and reflective symmetry simultaneously. An example on $K_5$ with uniform weights illustrates the reduction from $120$ total directed tours to $12$ canonical representatives, achieving a reduction factor of $|D_5| = 10$.

## Implementation

### Prerequisites

- [Julia 1.9](https://julialang.org/downloads/) or higher 
- [Jupyter Notebook](https://jupyter.org/install) with [IJulia](https://github.com/JuliaLang/IJulia.jl)

### Required Julia Packages

```julia
using Pkg; Pkg.add(["JuMP", "HiGHS"])
```

### Modeling and Solver

The optimization models are formulated using [JuMP](https://jump.dev/), a domain-specific algebraic modeling language for mathematical optimization in Julia. The choice of solver depends on the problem formulation; linear and mixed-integer programs are solved using [HiGHS](https://highs.dev/), interfaced through the [HiGHS.jl](https://github.com/jump-dev/HiGHS.jl) package, while other formulations may require alternative solvers.

### Running the Notebooks

- Launch Jupyter:
```bash
jupyter notebook
```
- Navigate to the ```CO_problems_notebooks/``` directory and select the desired notebook.

Each notebook covers:
1. Formulating the problem as a mathematical program
2. Identifying and characterizing structural symmetries
3. Applying symmetry reduction techniques
4. Analyzing the impact on the solution space

## Contributing

Contributions to this repository are welcome. Please open an issue or submit a pull request for suggestions, improvements, or bug fixes. You can also reach out via [Isaac Oliva-González's homepage](https://iolivag.github.io).

## License

This project is licensed under the MIT License.
