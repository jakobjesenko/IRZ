## Avtomati s tihimi prehodi (ε-NKA)

Vsi računski modeli (avtomati) so ekvivalentni.  
Vpeljali bomo tudi en nov formalizem: Regularni izrazi in prehod med $\text{RI} \lrarr \text{KA}$.  
Jezik, ki ga opisuje RI ali KA je **regularni jezik**.

## Regularni izrazi
induktivni razred

Baza: 
$$
\begin{equation*}
\begin{split}
    a &\isin \Sigma, a \isin \text{RI} \\
    \epsilon  &\isin RI \\
    \empty &\isin RI
\end{split}
\end{equation*}
$$
Pravila: 
$$
R_1, R_2 \isin RI \\
R_1 + R_2 \\
R_1 R_2 \\
R_1^*
$$

Pomen:  
$\{a\}$: jezik v katerem je beseda $a$  
$\{\epsilon\}$: jezik, ki vsebuje prazno besedo  
$\emptyset$: prazen jezik

$L(R_1)\cup L(R_2)$: Unija jezikov  
$L(R_1)L(R_2)$: Stik jezikov  
$L(R_1)^*$: Kleeneovo zaprtje

### Primer 1
$\Sigma = \set{0, 1}$  
Vsi nizi, ki se končajo z 001
$$
\begin{equation*}
\begin{split}
    (0 + 1)^* 001
\end{split}
\end{equation*}
$$

### Primer 2
$\Sigma = \set{0, 1}$  
vse besede, ki se ne končajo z 00
$$
\epsilon + 0 + 1 + (0+1)^*(00+10+01)
$$

### Primer 3
$\Sigma = \set{0, 1}$  
vse besede, ki vsebujejo sodo mnogo enojk.
$$
0^* + (0^* 1 0^* 1 0^*)^*
$$

### Primer 4
$\Sigma = \textrm{ascii}$  
zapiši RI za veljavnost e-mail naslova.(približno)
$$
    (\text{ascii}-\set{@})(\text{ascii}-\set{@})^*@(\text{ascii}-\set{@})(\text{ascii}-\set{@}).((\text{ascii}-\set{@})^2+(\text{ascii}-\set{@})^3)
$$

## Ekvivalenca KA

pretvorba: $\text{NKA} \rarr \text{DKA}$  

### Primer 5

```{mermaid}
flowchart LR
    q0((q0))
    q1(((q1)))
    q2((q2))
    start --> q0 -- a --> q0 -- a -->q1 -- b --> q0
    q1 -- a --> q1 -- b --> q2 -- a,b --> q2 -- b --> q1
    style start fill:#0000, stroke:#0000;
```

drevo izvajanja: na besedi aabbb

```{mermaid}
%%{
    init: {
        "flowchart": {
            "curve": "stepBefore"
        }
    }
}%%
flowchart TD
    0_0[q0 aabbb] --> 1_0[q0 abbb] --> 2_0[q0 bbb]
    1_0 --> 2_1[q1 bbb] --> 3_0[q0 bb]
    2_1 --> 3_1[q2 bb] --> 4_0[q1 b]
    4_0 --> 5_0[q0]
    4_0 --> 5_1[q2]
    3_1 --> 4_1[q2 b] --> 5_2((q1))
    4_1 --> 5_3[q2]
    classDef default fill:#0000, stroke:#0000, height:1.5rem
    style 5_2 stroke:#000;
```


$$
M = \braket{Q, \Sigma, \delta, q_0, F} \\
M' = \braket{2^Q, \Sigma, \delta', \set{q_0}, F'} \\
F' = \set{S \isin 2^Q | S \cap F \ne \empty} \\
\delta'(S,a) = \bigcup_{q\isin S}\delta(q,a)
$$

### Primer 6
Pretvorimo NKA v DKA.

```{mermaid}
flowchart LR
    q0((q0))
    q1(((q1)))
    q2((q2))
    start --> q0 -- 0,1 --> q0 -- 0 --> q1 -- 1 --> q2
    style start fill:#0000, stroke:#0000;
```

$2^Q$           | 0                | 1
----------------|------------------|-----
$\empty$        | $\empty$         | $\empty$
$q_0$           | $\set{q_0, q_1}$ | $\set{q_1}$
$q_1$           | $\empty$         | $\set{q_2}$
$q_2$           | $\empty$         | $\empty$
$q_0, q_1$      | $\set{q_0, q_1}$ | $\set{q_1, q_2}$
$q_0, q_2$      | $\set{q_0, q_1}$ | $\set{q_0}$
$q_1, q_2$      | $\empty$         | $\set{q_2}$
$q_0, q_1, q_2$ | $\set{q_0, q_1}$ | $\set{q_0, q_2}$


```{mermaid}
flowchart LR
    empty((∅))
    q0((q0))
    q1((q1))
    q2((q2))
    q0q1((q0q1))
    q1q2((q1q2))
    q0q2((q0q2))
    q0q1q2((q0q1q2))
    start --> q0
    empty -- 0,1 --> empty
    q0 -- 0 --> q0q1
    q0 -- 1 --> q1
    q1 -- 0 --> empty
    q1 -- 1 --> q2
    q2 -- 0,1 --> empty
    q0q1 -- 0 --> q0q1
    q0q1 -- 1 --> q1q2
    q1q2 -- 0 --> q0q1
    q1q2 -- 1 --> q0
    q0q1q2 -- 0 --> q0q1
    q0q1q2 -- 0 --> q0q2
    style start fill:#0000, stroke:#0000
```

izbrišemo vsa stanja, ki niso dosegljiva (imajo samo povezave ven) in označimo stanja, ki vsebujejo končna stanja iz NKA kot končna.

```{mermaid}
flowchart LR
    empty((∅))
    q0((q0))
    q1(((q1)))
    q2((q2))
    q0q1(((q0q1)))
    q1q2(((q1q2)))
    start --> q0
    empty -- 0,1 --> empty
    q0 -- 0 --> q0q1
    q0 -- 1 --> q1
    q1 -- 0 --> empty
    q1 -- 1 --> q2
    q2 -- 0,1 --> empty
    q0q1 -- 0 --> q0q1
    q0q1 -- 1 --> q1q2
    q1q2 -- 0 --> q0q1
    q1q2 -- 1 --> q0
    style start fill:#0000, stroke:#0000
```


### Primer 7

Pretvori NKA v DKA.

```{mermaid}
flowchart LR
    q0((q0))
    q1(((q1)))
    q3(((q3)))
    q2(((q2)))
    start --> q0 -- a --> q1 -- a --> q0 -- b --> q0 -- a --> q2 -- b --> q3 -- b --> q3 -- a --> q2
    q3 -- b --> q1
    style start fill:#0000, stroke:#0000;
```

```{mermaid}
flowchart LR
    q0((q0))
    start --> q0
    q0 -- a --> q1q2(((q1q2)))
    q0 -- b --> q0
    q1q2 -- a --> q0
    q1q2 -- b --> q3(((q3)))
    q3 -- a --> q2(((q2)))
    q3 -- b --> q1q3(((q1q3)))
    q2 -- a --> empty((∅)) -- a,b --> empty
    q2 -- b --> q3
    q1q3 -- a --> q0q2(((q0q2)))
    q1q3 -- b --> q1q3
    q0q2 -- a --> q1(((q1)))
    q0q2 -- b --> q0q3(((q0q3)))
    q1 -- a --> q0
    q1 -- b --> empty
    q0q3 -- a --> q1q2
    q0q3 -- b --> q0q1q3(((q0q1q3)))
    q0q1q3 -- a --> q0q1q2(((q0q1q2)))
    q0q1q3 -- b --> q0q1q3
    q0q1q2 -- a --> q0q1q2
    q0q1q2 -- b --> q0q3
    style start fill:#0000, stroke:#0000;
```


## Pretvorba ε-NKA v NKA

Pretvorbo $\epsilon$-NKA v NKA delamo s pomočjo epsilon-zaprtja (epsilon-closure = $\textit{ε-cl}$), ki nam za dano stanje pove katera stanja lahko dosežemo s samo tihimi prehodi.

### Primer 8

```{mermaid}
flowchart LR
    q1((q1))
    q2((q2))
    q3((q3))
    q4(((q4)))
    q5((q5))
    start --> q1 --b--> q2 -- a --> q2 -- b --> q3
    q5 -- b --> q3
    q2 -- ε --> q5
    q1 -- ε --> q4
    q3 -- ε --> q4
    q5 -- ε --> q1
    style start fill:#0000, stroke:#0000;
```


$$
\begin{equation*}
\begin{split}
    \textit{ε-cl}(q1) &= \set{q1,q4} \\
    \textit{ε-cl}(q2) &= \set{q2,q5,q4} \\
    \textit{ε-cl}(q3) &= \set{q3,q4} \\
    \textit{ε-cl}(q4) &= \set{q4} \\
    \textit{ε-cl}(q5) &= \set{q5,q4}
\end{split}
\end{equation*}
$$


zbrišemo epsilone
če $\textit{ε-cl}(q_n)$ vsebuje končno stanje mora tudi stanje $q_n$ biti končno.  
Torej lahko funkcijo prehodov definiramo takole:
$$
\delta(q, a) = \textit{ε-cl}(\delta(\textit{ε-cl}(q), a))
$$

```{mermaid}
flowchart LR
    q1(((q1)))
    q2((q2))
    q3((q3))
    q4(((q4)))
    q5((q5))
    start --> q1 --b--> q2 -- a --> q2 -- b --> q3
    q5 -- b --> q3
    q1 -- b --> q5
    q1 -- b --> q4
    q2 -- a --> q5
    q2 -- a,b --> q4
    q5 -- b --> q4
    style start fill:#0000, stroke:#0000;
```
