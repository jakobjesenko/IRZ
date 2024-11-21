## Pretvorba RI v KA
$\text{RI} \rarr \text{ε-NKA}$

### Definicija induktivnega razreda
#### Baza:  
$a$ (avtomat, ki sprejme znak $a$)
```{mermaid}
flowchart LR
    start --> q0((q0)) --a--> q1(((q1)))
    style start fill:#0000, stroke:#0000;
```

$ε$ (avtomat, ki sprejme prazno besedo)
```{mermaid}
flowchart LR
    start --> q0((q0)) --ε--> q1(((q1)))
    style start fill:#0000, stroke:#0000;
```

$\empty$ (avtomat, ki ne sprejme nobene besede)
```{mermaid}
flowchart LR
    start --> q0((q0)) ~~~ q1(((q1)))
    style start fill:#0000, stroke:#0000;
```

#### Pravila:  
$R_1$
```{mermaid}
flowchart LR
    start
    subgraph M1
    direction LR
    q0((q10)) ~~~ q1(((q11)))
    end
    start --> q0
    style start fill:#0000, stroke:#0000;
```
$R_2$
```{mermaid}
flowchart LR
    start
    subgraph M2
    direction LR
    q0((q20)) ~~~ q1(((q21)))
    end
    start --> q0
    style start fill:#0000, stroke:#0000;
```

##### 1. $R_1 + R_2$
Unija: vzporedno zvežemo avtomata
```{mermaid}
flowchart LR
    subgraph M2
        q20((q20)) ~~~ q21((q21))
    end
    subgraph M1
        q10((q10)) ~~~ q11((q11))
    end
    start --> q00((q00))
    q00 --ε--> q10 & q20
    q11 & q21 --ε--> q01(((q01)))

    style start fill:#0000, stroke:#0000;
```
##### 2. $R_1 R_2$
Stik: Zaporedno vežemo avtomata
```{mermaid}
flowchart LR
    subgraph M1
        q10((q10)) ~~~ q11((q11))
    end
    subgraph M2
        q20((q20)) ~~~ q21((q21))
    end
    start --> q10
    q11 --ε--> q20
    q21 --ε--> q01(((q01)))

    style start fill:#0000, stroke:#0000;
```

##### 3. $R_1^*$
Kleeneovo zaprtje: 
```{mermaid}
flowchart LR
    subgraph M1
        q10((q10)) ~~~ q11((q11))
    end
    q11 --ε--> q10
    start --> q00((q00)) --ε--> q10
    q11 --ε--> q01(((q01)))
    q00 --ε--> q01

    style start fill:#0000, stroke:#0000;
```


### Primer 1

$(01)^*001$
```{mermaid}
flowchart LR
    subgraph M[ ]
    q0
    q1
    q2
    q3
    q4
    end
    subgraph N[ ]
    q5((q6))
    q6((q6))
    q7((q7))
    q8((q8))
    q9((q9))
    q10((q10))
    q11(((q11)))
    end
    start --> q0((q0)) --0--> q1((q1)) --ε--> q2((q2)) --1--> q3((q3)) --ε--> q4((q4))
    q3 --ε--> q1
    q0 --ε--> q4
    q4 --ε--> q5 --0--> q6 --> q7 --ε--> q8 --0--> q9 --ε--> q10 --1--> q11
    style start fill:#0000, stroke:#0000;
    style M stroke:#0000, fill:#0000;
    style N stroke:#0000, fill:#0000;
```



## Lema o napihovanju za reguarne jezike

$$
\begin{equation*}
\begin{split}
    \forall L \isin RJ, \exist n \implies &\\
    \forall w \isin L, |w|\ge &n: \\
    w = xyz, |y|\ge &1, |xy| \le n \implies\\
    &\forall i\ge 0: xy^iz \isin L
\end{split}
\end{equation*}
$$
```{mermaid}
flowchart LR
    start --> q0(( )) -. x .-> q1(( )) -. y .-> q1(( )) -. z .-> qf((( )))
    style start fill:#0000, stroke:#0000;
```

### Primer 1
$L = \set{a^ib^i}$ (jezik, ki vsebuje besede z enakim številom $a$-jev in $b$-jev)  
**Avtomati ne znajo šteti!**  
Beseda, ki je gotovo dovolj dolga:  
$$w = a^n b^n$$
Pogledamo, kako se avtomat zacikla v prvih n znakih:
$$
\begin{equation*}
\begin{split}
    x&=a^k \\
    y&=a^l \\
    z&=a^{n-k-l}b^n
\end{split}
\end{equation*}
$$
Kaj se zgodi, če se večkrat zavrtim po delu $y$? (glej shemo avtomata)
$$
\begin{equation*}
\begin{split}
    x y^i z &= a^k a^{li} a^{n-l-k} b^n \\
    &= a^{n+l(i-1)} b^n\\
    i = 2 & \\
    & a^{n+l} b^n \not \isin L
\end{split}
\end{equation*}$$

### Dokazovajne
1. Izberemo besedo, ki je v jeziku in je dovolj dolga $\forall w \isin L, |w|\ge n$
2. Razbijemo besedo na vse možne načine na $w=xyz$
3. Za vzako razbitje poiščemo protiprimer trditve $\forall i\ge 0: xy^iz \isin L$

### Primer 1 ponovno
$$
    w = a^\frac n2 b ^\frac n2
$$
1.
$$
\begin{equation*}
\begin{split}
    x &= a^k\\
    y &= a^l \\
    z &= a^{\frac n2 -k-l} b ^\frac n2 \\
    \\
    x y^i z &= a^k a^{li} a^{\frac n2 -k-l} b ^\frac n2\\
    &= a^{\frac n2 + l(i-1)} b ^\frac n2 \\
    i = 2 \\
    & a^{\frac n2 + l} b ^\frac n2 \not\isin L \\
\end{split}
\end{equation*}
$$
2.
$$
\begin{equation*}
\begin{split}
    x &= a^\frac n2\\
    y &= b^l\\
    z &= b^{\frac n2 -k-l}\\
    \\
    x y^i z &= a^\frac n2 b^{li} b^{\frac n2 -k-l}\\
    &= a^\frac n2 b^{\frac n2 + l(i-1)}\\
    i = 2 \\
    & a^{\frac n2} b ^{\frac n2 + l} \not\isin L \\
\end{split}
\end{equation*}
$$
3.
$$
\begin{equation*}
\begin{split}
    x &= a^k\\
    y &= a^{\frac n2 - k} b^l\\
    z &= b^{\frac n2 - l}\\
    \\
    x y^i z &= a^k (a^{\frac n2 - k} b^l)^i b^{\frac n2 - l}\\
    i = 2 &\implies a \text{ in } b \text{ se pomešajo}
\end{split}
\end{equation*}
$$

### Primer 2
$L = \set{a^ib^j}, i \gt j$
$$
\begin{equation*}
\begin{split}
    w &= a^n b^{n-1} \\
    x &= a^k\\
    y &= a^l\\
    z &= a^{n-k-l} b^{n-1}\\
    \\
    x y^i z &= a^k a^{li} a^{n-k-l} b^{n-1} \\
    &= a^{n+l(i-1)}b^{n-1} \\
    \\
    i = 0\\ 
    & a^{n-l}b^{n-1} \not\isin L
\end{split}
\end{equation*}$$

### Primer 3
jezik palindromov iz a in b.  
$L = \set{w \isin \set{a,b}^*; w = w^r}$

$$
\begin{equation*}
\begin{split}
    w = a^n b^n a^n\\
    x &= a^k\\
    y &= a^l\\
    z &= a^{n-k-l}b^n a^n\\
    \\
    x y^i z &= a^k a^{li} a^{n-k-l}b^n a^n \\
    &= a^{n + l(i - 1)} b^n a^n \\
    i = 2 \\
    & a^{n+l} b^n a^n \not\isin L
\end{split}
\end{equation*}$$

### Primer 4
$L = \set{a^ib^j}; i \ne j$

$$
\begin{equation*}
\begin{split}
    w = a^{n+1}b^n \\
    x &= a^k\\
    y &= a^l\\
    z &= a^{n+1-k-l}b^n\\
    \\
    x y^i z &= a^k a^{li} a^{n+1-k-l}b^n \\
    &= a^{n+1+l(i-1)}b^n \\
    \\
    n+1+l(i-1) &\ne n\\
    \color{red}{\text{dokazovanje ni bilo uspešno}}
\end{split}
\end{equation*}$$

Poskusimo še enkrat

$$
\begin{equation*}
\begin{split}
    w = a^n b^{n+n!} \\
    x &= a^k\\
    y &= a^l\\
    z &= a^{n-k-l} b^{n+n!}\\
    \\
    x y^i z &= a^k a^{li} a^{n-k-l} b^{n+n!}\\
    &= a^{n + (l - i)} b^{n+n!} \\
    \\
    l(i-1) &= n! \\
    i-1 &= \frac{n!}{l} \\
    i &= \frac{n!}{l} + 1 \\
    & a^{n + (l - \frac{n!}{l} - 1)} b^{n+n!}
\end{split}
\end{equation*}$$

### Primer 5
Jezik pravilno gnezdenih oklepajev.
$$
\begin{equation*}
\begin{split}
    w = \textcolor{green}(^n \textcolor{green})^n \\
    x &= \textcolor{green}(^k\\
    y &= \textcolor{green}(^{li}\\
    z &= \textcolor{green}(^{n-k-l} \textcolor{green})^{n}\\
    \\
    x y^i z &= \textcolor{green}(^k \textcolor{green}(^{li} \textcolor{green}(^{n-k-l}  \textcolor{green})^{n} \\
    &= \textcolor{green}(^{n + l(i-1)}  \textcolor{green})^{n} \\
    i = 2 \\
    & \textcolor{green}(^{n + l} \textcolor{green})^{n} \not\isin L
\end{split}
\end{equation*}$$

### Primer 6

$L=\set{a^p}, p \text{ je praštevilo}$

$$
\begin{equation*}
\begin{split}
    w = a^r; r\text{ je praštevilo}, r\gt n\\
    x &= a^k\\
    y &= a^l\\
    z &= a^{r-k-l}\\
    \\
    x y^i z &= a^ka^{li} a^{r-k-l} \\
    &= a^{r +l(i-1)}\\
    \\
    & r + l(i - 1)\\
    i = r+1\\
    & r + l(r+1-1) = r(l + 1) \rarr \text{je očitno sestavljeno število}
\end{split}
\end{equation*}
$$

### Primer 7
$L = \set{0^{i^2}}$

$$
\begin{equation*}
\begin{split}
    w = 0^{n^2} \\
    x &= 0^k\\
    y &= 0^l\\
    z &= 0^{n^2-k-l}\\
    x y^i z &= 0^k 0^{li} 0^{n^2-k-l} \\
    &= 0^{n^2 +l(i-1)}\\
    \\
    n^2 +l(i-1) \text{ ne sme biti popoln kvadrat} \\
    i = 2 \\
    n^2 + l\\

    \text{razdalja med naslednjim popolnim kvadratom:}\\
    (n+1)^2-n^2 = 2n + 1\\
    0 \le l \le 2n+1 \\
    0^{n^2 +l} \not\isin L
\end{split}
\end{equation*}
$$