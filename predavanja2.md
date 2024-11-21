## Končni avtomati in regularni izrazi

Avtomat je lahko strojna izvedba ali programska oprema.
Primeri:
- dvigalo
- božične lučke  

Finite state systems = sistemi s končno mnogo stanji -> imajo končno število stanj

### Deterministični končni avtomat DKA
DKA je objekt sestavljen iz 2 delov:
1. končno število stanj
2. množica prehodov med stanji, ki se zgodijo pri pranju simbolov iz abecede $\Sigma$
- za vsak simbol in vsako stanje obstaja natančno 1 prehod
- eno stanje (običajno $q_0$) je začetno, v katerem DKA začenja delovanje
- nekatera stanja so končna (so dvakrat obkrožena)
- DKA **sprejme** besedo, če obstaja zaporedje prehodov, ki ustreza vhodnim simbolom iz besede, in vodi DKA iz $q_0$ v končno stanje.
- DKA lahko predstavimo z diagramom
```{mermaid}
flowchart LR
    q[ ] -- start --> q0(((q0)))
    q0 -- 1 --> q1((q1)) -- 0 --> q3((q3)) -- 0 --> q1 -- 1 --> q0
    q0 -- 0 --> q2((q2)) -- 0 --> q0
    q2 -- 1 --> q3 -- 1 --> q2
    style q stroke:#0000, fill:#0000
```

#### Definicija
$$
\begin{equation*}
\begin{split}
    \text{DKA}\space M &= (Q, \Sigma, \delta, q_0, F) \\
    Q &:= \text{množica stanj} \\
    \Sigma &:= \text{vhodna abeceda} \\
    q_0 &:= \text{začetno stanje} \\
    F \subseteq Q &:= \text{množica končnih stanj} \\
    \delta &:= \text{funkcija prehodov} \\
    \delta &: Q \times \Sigma \rarr Q \\
\end{split}
\end{equation*}
$$

DKA lahko predstavimo kot nadzorno enoto in trak, na katerem je vpisana vhodna beseda

```{mermaid}
block-beta
columns 7
space:2 CU["nadzorna\nenota"]:3 space:2
space:7
s1["0"] s2["0"] s3["1"] s4["1"] s5["1"] s6["0"] s7["1"]
s3 --> CU
style s3 stroke-width:3px
```

Razširjena funkcija prehodov:
$$
\hat{\delta}(q, \epsilon) = q \\
\hat{\delta}(q, wa) = \delta(\hat{\delta}(p, w), a)
$$

```{mermaid}
flowchart LR
    q(("q"))
    r(("r"))
    p(("p"))
    q-.w..->r
    r -- a --> p
```

- DKA sprejme besedo $x$, če po sprejemanju vseh simbolov iz besede $x$ preide v končno stanje.
$$
\delta(q_0, x) = p; p \isin F
$$
- Jezik, ki ga sprejme DKA $M$ je množica vseh besed, ki jih sprejme.
$$
L(M) = \{ x \isin \Sigma^* | \delta(q_0, x) \isin F \}
$$
- Jezik $L'$ je regularen če obstaja nek DKA, katerega jezik je $L'$.
$$
\exists \text{DKA} \space M : L' = L(M)
$$

#### Primer
(glej diagram zgoraj)
$$
\begin{equation*}
\begin{split}
    Q &= \{q_0, q_1, q_2, q_3\} \\
    \Sigma &= \{0, 1\} \\
    F &= \{q_0\}
\end{split}
\end{equation*}
$$

$\delta$ | $0$| $1$  
---------|----|------
$q_0$ | $q_2$ | $q_1$
$q_1$ | $q_3$ | $q_0$
$q_2$ | $q_0$ | $q_3$
$q_3$ | $q_1$ | $q_2$

izpeljava:
$$
\begin{equation*}
\begin{split}
    \delta(q_0, 110101) &= \delta(q_1, 10101) \\
    &= \delta(q_0, 0101) \\
    &= \delta(q_2, 101) \\
    &= \delta(q_3, 01) \\
    &= \delta(q_1, 1) = q_0 \isin F
\end{split}
\end{equation*}
$$

### Nedeterministični končni avtomat NKA

```{mermaid}
flowchart LR
    q[ ] -- start --> q0(((q0))) -- 1 --> q1((q1)) -- 1 --> q2((q2)) -- 0 --> q3((q3))
    q0 -- 0 --> q2
    q0 -- 0 --> q3
    q1 -- 1 --> q3
    style q stroke:#0000, fill:#0000
```
pri določenem simbolu lahko avtomat preide v več stanj.

NKA **sprejme** besedo, če obstaja vsaj 1 pot do končnega stanja.

#### Nedeterminizem
- Kdo ugotovi ali NKA besedo sprejme?  
  **NKA sam.**
- Kako NKA to ugotovi?  
  **NKA je nerealističen model računanja, zato lahko rečemo, da se *nekako* odloči sam.**
- Čemu služijo ti nerealistični modeli?  
  **Uporabljamo jih za določanje spodnje meje računskih zahtevnosti, saj jih je v večini primerov lažje konstruirati.**

#### Definicija
$$
\begin{equation*}
\begin{split}
    \text{NKA}\space M &= (Q, \Sigma, \delta, q_0, F) \\
    Q &:= \text{množica stanj} \\
    \Sigma &:= \text{vhodna abeceda} \\
    q_0 &:= \text{začetno stanje} \\
    F \subseteq Q &:= \text{množica končnih stanj} \\
    \delta &:= \text{funkcija prehodov} \\
    \delta &: Q \times \Sigma \rarr 2^Q \\
\end{split}
\end{equation*}
$$

#### Primer

```{mermaid}
flowchart LR
    q[ ] -- start --> q0((q0)) -- 0 --> q3((q3)) -- 0 --> q4(((q4)))
    q0 -- 1 --> q1((q1)) -- 1 --> q2(((q2)))
    q0 -- 0,1 --> q0
    q4 -- 0,1 --> q4
    q2 -- 0,1 --> q2
    style q stroke:#0000, fill:#0000
```
$$
\begin{equation*}
\begin{split}
    Q &= \{q_0, q_1, q_2, q_3, q_4\} \\
    \Sigma &= \{0, 1\} \\
    F &= \{q_2, q_4\}
\end{split}
\end{equation*}
$$
$\delta$ | $0$| $1$  
---------|----|------
$q_0$ | {$q_0,q_3$} | {$q_0,q_1$}
$q_1$ | $\empty$ | {$q_2$}
$q_2$ | {$q_2$} | {$q_2$}
$q_2$ | {$q_4$} | $\empty$
$q_4$ | {$q_4$} | {$q_4$}

Razširjena funkcija prehodov:
$$
\hat{\delta}(q, \epsilon) = \{q\} \\
\hat{\delta}(q, wa) = \{p \isin Q | \exist r \isin \hat{\delta}(q, w): p \isin \delta(r, a)\} \\
\hat{\delta}(q, a) = \delta(q, a)
$$

- $\text{NKA}\space M$ sprejme besedo, če $\delta(q_0, x)$ vsebuje kako končno stanje.
  $$
  \delta(q_0, x) \cap F \ne \empty
  $$
- Jezik ki ga sprejme NKA M
  $$
  L(M) = \{x\isin \Sigma^* | \delta(q_0, x) \space \text{vsebuje neko končno stanje iz}\space F\}
  $$

### Ekvivalentnost DKA in NKA
Vsak DKA je tudi NKA.

Ali je NKA močnejši od DKA bomo izvedeli naslednjič 😉.