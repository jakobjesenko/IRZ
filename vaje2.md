## Jezik
**Problem = Jezik**

- Abeceda: $\Sigma$
- Beseda: $w = a_1 a_2 \dotso a_k$
- Stik množic: $A\cdot B = \{w_1 w_2 | w_1 \isin A, w_2 \isin B\}$
- $A^k = \underbrace{A \cdot A \dotsb A}_k$
- Kleenovo zaprtje: $A^* = \bigcup^\infin_{i=0}A^i$
- $L \subseteq \Sigma^*$  
  [ ($L$)  $\Sigma^*$  ] // euler diagram
- Problem, kjer je dogovor **da/ne** se imenuje odločitvrni problem.
  
### Kaj je računanje?

Rabimo stvar, ki ji podamo besedo iz vhodnega jezika, in iz nje preberemo odgovor.
```{mermaid}
flowchart LR
    input[beseda] --> machine --> output[da/ne]
    style input fill:#0000, stroke:#0000;
    style output fill:#0000, stroke:#0000;
```

### DKA

$$
\begin{equation*}
\begin{split}
    \text{DKA}\space M &= \braket{Q, \Sigma, \delta, q_0, F} \\
    Q &:= \text{množica stanj} \\
    \Sigma &:= \text{vhodna abeceda} \\
    q_0 &:= \text{začetno stanje} \\
    F \subseteq Q &:= \text{množica končnih stanj} \\
    \delta &:= \text{funkcija prehodov} \\
    \delta &: Q \times \Sigma \rarr Q \\
\end{split}
\end{equation*}
$$

#### Trenutni opis
$q\space aw \vdash rw$

#### Pimer 1
$\Sigma = \set{0, 1}$

Avtomat, ki sprejme sodo število ničel.

```{mermaid}
flowchart LR
start --> q0(((q0))) -- 1 --> q0
q0 -- 0 --> q1((q1)) -- 1 --> q1
q1 -- 0 --> q0
style start fill:#0000, stroke:#0000;
```


#### Pimer 2
$\Sigma = \set{0, 1}$

Avtomat, ki sprejme sodo število ničel in liho število enojk.

```{mermaid}
flowchart LR
q0((q0))
q1(((q1)))
q2((q2))
q3((q3))
start --> q0 -- 1 --> q1 -- 1 --> q0
q0 -- 0 --> q2 -- 0 --> q0
q1 -- 0 --> q3 -- 0 --> q1
q3 -- 1 --> q2
q2 -- 1 --> q3
style start fill:#0000, stroke:#0000;
```

#### Primer 3
$\Sigma = \set{0, 1}$  
Besede, ki se končajo z $001$: $L = \set{w001 | w \isin \set{0, 1}^*}$

```{mermaid}
flowchart LR
    q0((q0))
    q1((q1))
    q2((q2))
    q3(((q3)))
    start --> q0
    q0 -- 0 --> q1 -- 0 --> q2 -- 1 --> q3
    q0 -- 1 --> q0
    q1 -- 1 --> q0
    q2 -- 0 --> q2
    q3 -- 0 --> q1
    q3 -- 1 --> q0
style start fill:#0000, stroke:#0000;
```
$w=01001$  
$$
\begin{equation*}
\begin{split}
    q_0\space 010001 \vdash
    q_1\space 10001 \vdash
    q_0\space 0001 \vdash
    q_1\space 001 \vdash
    q_2\space 01 \vdash
    q_2\space 1 \vdash
    q_3\space
\end{split}
\end{equation*}$$

#### Primer 4
$\Sigma = \set{a, b, c}$  
Vsi $a$ so pred vsemi $b$, vsi $b$ so pred vsemi $c$.

```{mermaid}
flowchart LR
    q0(((q0)))
    q1(((q1)))
    q2(((q2)))
    q3(((q3)))
    qs((qs))

    start --> q0 -- a --> q0
    q0 -- b --> q1 -- a --> qs
    q0 -- c --> q2 -- a,c -->
    q2 -- b --> qs -- a,b,c --> qs
    q1 -- c --> q3 -- c --> q3
    q1 -- b --> q1
    q3 -- a,b --> qs

    
style start fill:#0000, stroke:#0000;
```

#### Primer 5
$\Sigma = \text{ascii}$  
$L = \set{for, to, do, downto, program, procedure, forward}$

```{mermaid}
flowchart LR
    q0((q0))
    q1(((q1)))
    q2(((q2)))
    q3(((q3)))
    q4(((q4)))
    q5(((q5)))
    q6((q6))
    q7(((q7)))
    q8(((q8)))
    start --> q0 -- for --> q1 -- ward --> q2
    q0 -- to --> q3
    q0 -- do --> q4 -- wnto --> q5
    q0 -- pro --> q6 -- gram --> q7
    q6 -- cedure --> q8 
style start fill:#0000, stroke:#0000;
```

**Vsi končni jeziki imajo Končni avtomat**

#### Primer 5
$\Sigma = \set{0,1}$  
$L = \set{w \equiv0 (mod 3) | w \isin \set{0, 1}^*}$
$$
\begin{equation*}
\begin{split}
w \equiv 0 (mod3)&: \\
    w0 &\rarr 3k \cdot 2 \equiv 3(2k) \underbar{+ 0} (mod 3) \\
    w1 &\rarr 3k \cdot 2 + 1 \equiv 3(2k) \underbar{+ 1} (mod 3) \\
w \equiv 1 (mod3)&: \\
    w0 &\rarr (3k + 1) \cdot 2 \equiv 3(2k) \underbar{+ 2} (mod 3) \\
    w1 &\rarr (3k + 1) \cdot 2 + 1 \equiv 3(2k) \underbar{+ 0} (mod 3) \\
w \equiv 2 (mod3)&: \\
    w0 &\rarr (3k+2) \cdot 2 \equiv 3(2k) \underbar{+ 1} (mod 3) \\
    w1 &\rarr (3k+2) \cdot 2 + 1 \equiv 3(2k) \underbar{+ 2} (mod 3)\\
\end{split}
\end{equation*}
$$

```{mermaid}
flowchart LR
    q0(((q0)))
    q1((q1))
    q2((q2))
    start --> q0 -- 0 --> q0 -- 1 --> q1 -- 1 --> q0
    q1 -- 0 --> q2 -- 1 --> q2 -- 0 --> q1
style start fill:#0000, stroke:#0000;
```

### NKA

$$
\begin{equation*}
\begin{split}
    \text{NKA}\space M &= \braket{Q, \Sigma, \delta, q_0, F} \\
    Q &:= \text{množica stanj} \\
    \Sigma &:= \text{vhodna abeceda} \\
    q_0 &:= \text{začetno stanje} \\
    F \subseteq Q &:= \text{množica končnih stanj} \\
    \delta &:= \text{funkcija prehodov} \\
    \delta &: Q \times \Sigma \rarr 2^Q \\
\end{split}
\end{equation*}
$$

#### Primer 1
$\Sigma = \set{0, 1}$  
Besede, ki se končajo z $001$: $L = \set{w001 | w \isin \set{0, 1}^*}$

```{mermaid}
flowchart LR
    q0((q0))
    q1((q1))
    q2((q2))
    q3(((q3)))
    start --> q0
    q0 -- 0 --> q1 -- 0 --> q2 -- 1 --> q3
    q0 -- 0,1 --> q0
style start fill:#0000, stroke:#0000;
```

interpretacija 1: Kako se obnaša avtomat, če ima neko dodatno informacijo.
interpretacija 2: Avtomat preizkusi vse možnosti

$w = 0110001$
```{mermaid}
flowchart TB
    0[q0 0110001] --> 20[q0 110001] --> 30[q0 10001]--> 40[q0 0001] --> 50[q0 001] --> 60[q0 01] --> 70[q0 1] --> 80[q0] --> x0[🗶]
    60 --> 71[q1 1] --> x1[🗶]
    50 --> 61[q1 01] --> 72[q2 1] --> 83[q3] --> y[🗸]
    40 --> 51[q1 001] --> 62[q2 01] --> x2[🗶]
style x0 fill:#0000, stroke:#0000, color:#f00, font-size:3rem;
style x1 fill:#0000, stroke:#0000, color:#f00, font-size:3rem;
style x2 fill:#0000, stroke:#0000, color:#f00, font-size:3rem;
style y fill:#0000, stroke:#0000, color:#0f0, font-size:3rem;

```