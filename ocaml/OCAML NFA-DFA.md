# π« OCAML NFA-DFA
Class: [[OCAML]]
Subject: #
Date: 2023-03-09
Topics: #, #, # 

---

# π¬ Intro to Non-Deterministic Finite Automata (NFA)

Theoretical concept in computer science that defines a mathematical model for recognizing regular languages.

NFA are useful to recognize a wide range of patterns that can be expressed as regular expressions. Used in many programming languages and software tools for pattern matching, parsing, and lexing.

The NFA determines whether a given string of input symbols is accepted. One accepted string needs to follow all possible paths that the machine can take, and see if any of them lead to an accepting state. If there is at least one path that leads to an accepting state, then the string is accepted by the NFA. Otherwise, it is rejected.

An NFA is represented by digraphs called state diagram.
-   The vertices represent the states.
-   The arrows with an input alphabet show the transitions.
-   The initial state is denoted by an empty single arrow.
-   The final state is indicated by double circles.

# Formal Definition
NFA β { Q, β, β, q0, F}
- β β Finite non-empty set of input symbols. 
- Q β Finite non-empty set of states. 
- $q_{0}$ β Beginning state. 
- F β Final State
- β β Transitional Function. 

# NFA Example
Let a non-deterministic finite automaton be

![](../Assets/nfa-accept.png)

- β is alphabet β a , b
- Q nonempty states β s0 , s1 , s2 , s3 , s4 , s5 , s6
- q0 start stateΒ β s0
- F ending state β s4 , s6
- β list of possible transitions β 
	- [(s1 , a, s3) , __ , __ ]


# π NFA vs DFA
- NFA can have epsilon (Ξ΅) transitions, multiple transitions coming out of one state
- DFA cannot have Ξ΅-transitions and cannot have multiple transitions

# β‘ Convert NFA to DFA
## Ξ΅-closure
- `Ξ΅-closure(Ξ΄, p)`Β returns the set of states reachable from p using Ξ΅-transitions alone.
- Returned set always has `p`

Let the following NFA:

<img src="https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/IMG_25D323DF4D1D-1.jpeg" width="50%" height="50%" />

All possible transitions with epsilons (Ξ΅)
- Ξ΅-closure(p1) β {p1 , p2 , p3}
- Ξ΅-closure(p2) β {p2 , p3}
- Ξ΅-closure(p3) β { p3 }
- Ξ΅-closure({p1,p3}) β {p1 , p2 , p3} U {p2 , p3} = {p1 , p2 , p3}

## move
- Simpler version of Ξ΅-closure
- `move(Ξ΄,p,Ο)`Β returns the set of states reachable from `p` using exactly one transition on symbol `Ο`.

Let the following NFA:

<img src="https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/IMG_99C79063E044-1.jpeg" width="50%" height="50%" />

All possible `move`
- move(p1 , a) β {p2 , p3}
- move(p1 , b) β ΓΈ
- move(p2 , b) β {p3}
- move(p3 , a) β ΓΈ
- move(p3 , b) β ΓΈ
- move({p1 , p2} , b) β ΓΈ U {p3} = {p3}

### Note
`move` doesn't use Ξ΅ free transitions

<img src="https://raw.githubusercontent.com/lamula21/cheat-sheets/main/Assets/IMG_7B4FFB7D31E6-1.jpeg" width="50%" height="50%" />

- move(p1,b) = ΓΈ

## Algorithm
Let $r_0$ = $\varepsilon\text{-closure}(\delta, q_0)$, add it to $R$\
While $\exists$ an unmarked state $r \in R$:\
$\qquad$ Mark $r$
$\qquad$ For each $\sigma \in \Sigma$\
$\qquad$$\qquad$Let $E = \text{move}(\delta, r, \sigma)$\
$\qquad$$\qquad$Let $e = \varepsilon\text{-closure}(\delta, E)$\
$\qquad$$\qquad$$\qquad$If $e \notin R$\
$\qquad$$\qquad$$\qquad$$\qquad$Let $R = R \cup \\{e\\}$\
$\qquad$$\qquad$$\qquad$Let $\delta' = \delta \cup \\{ r, \sigma, e \\} $\
Let $F = \\{r \mid \exists s \in r \text{ with } s \in F_n \\}$

## Example
