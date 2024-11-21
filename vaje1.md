# Vaje 1

## Opravljanje predmeta
- vsota kolokvijev 50% -> narejene vaje  
- vsak kolokvij nad 80% -> verjerno zaključen predmet
- Izpit: 50% na teoretičnem in praktičnem delu

## 3 miti računalništva

### 1. Mit:
**Računalniki izračunajo vse**  
- neizračunljivost: nikoli ne bomo imeli algortma za rešitev takih problemov
- računska zahtevnost: algoritmi porabijo preveč sredstev ($P=NP$)

### 2. Mit:
**Hitrost sprememb**
- uporabniki: stvari se prehitro spreminjajo - ljudje so nezadovoljni
- razvijalci: stvari se ne spreminjajo tako hitro (c: 50 let, Java: 30 let, Python: 30 let), tehnologije iz 80-ih let... Povečuje se količina novih tehnologij, ki so med sabo lahko zelo različne.
- koncepti/temelji: so zelo fiksni in jih ni tako veliko. Če poznaš temelje si lahko zelo prilagodljiv pri uporabi različnih tehnologij. **Pri IRZ se bomo ukvarjali s koncepti**

### 3. Mit:
**Računalniki so taki**: Von Neuman, proceduralni jeziki, ...
- Pregledali bomo Turingov stroj, na katerem temelji tudi tudi Von Neumanov model
- Lambda račun: funkcijski jeziki, arhitktura: beta-flow, bolje podpirajo paralelizem in varnost
- DNK računanje
- Kvantno računanje

## Tehnike dokazovanja

**Dokaz je serija korakov, pri katerem verjamemo vsem izmed njih.**  
Definicija je kontekst, ki je dogovorjen (preimenovanja ipd.), izrek pa lahko dokažemo. Lema je izrek, ki sam po sebi ni zanimiv, lahko pa ga uporabimo pri dokazovanju.

### Direktni/neposrednji dokazi
Dokazi, ki vsebujejo zamo elementarne načine (aritmetične zakone, premetavanje, ...)  
$$
\text{Izrek: Kvadriranje ohranja pariteto} \\
\forall n \isin \natnums : n \equiv  n^2 (mod 2) \\
\begin{equation*}
\begin{split}
    2k&: (2k)^2 = 4k^2 = 2 \cdot 2k \\
    2k - 1&: (2k - 1)^2 = 4k^2 - 4k + 1 = 2\cdot 2(k^2 - k) + 1
\end{split}
\end{equation*}
$$

### Golobnjak
Imomo n lukenj in k golobov. Ali lahko vse golobe razporedimo v luknje

Izrek: vsak graf ki ima vsaj 2 vozlišči mora imeti 2 vozlišči iste stopnje.

A - B - C  
A B  

$$
\forall G = <V,E>, |V|\ge 2, \exist u, v\isin V: deg(u)= deg(v)
$$
golobi: vozlišča  
$0 \ge deg(v) \ge |V|-1$  
Ali lahko naredimo graf, v katerem je hkrati vozlišce stopnje $n - 1$ in stopnje $n = 0$? Ne ta dva grafa se izključujeta.

$$
\exist v: deg(v) = 0 \implies deg(u) \isin [0, n - 2] \\
\not\exist v: deg(v) = 0 \implies deg(u) \isin [1, n - 1]
$$

### Indukcja
Induktivni razred $I$
1. Baza  
2. Pravila
   $a\isin I \implies f(a) \isin I$

- Primer: $\natnums$  
Baza: 1  
pravilo: $n\isin\natnums \implies n+1 \isin \natnums$

Pokažemo, da neka lastnost velja za bazo. Dokažemo, da nobeno pravilo ne pokvari te lastnosti.

- Primer: Zidovi  
Baza: $▭ \isin Zid$
Pravila: 
1. $z \isin Zid \implies \frac{▭}{z} \isin Zid$
2. $z \isin Zid \implies z▭ \isin Zid$

- Primer: Drevo z $n$ vozlišči ima $n-1$ povezav.

Baza: o  
Pravila:
1.dodamo vozlišče in ga povežemo s katerimkoli prejšnjim vozliščem

Baza: o: $n = 1, e = 0$  
pravilo: $T{n, n-1} \rarr T'{n+1, n}$

### Protislovje
Konstruktivisti ne priznavajo protislovja kot dokaz - dokaz je manjše kvalitete.

Velja $p$ ali $\neg p$.

Primer: praštevil je neskončno
$$
p: \text{Praštevil je neskončno} \\
\neg p: \text{Praštevil je končno mnogo}\\
P = \{p_1, p_2, \dotso, p_k\} \\
p' = \prod_{i = 1}^{k}p_i + 1 \text{je tudi praštevilo} \implies \text{praštevil ni končno mnogo}
$$

### Moč množic

Če med dvema množicama $A, B$ obstaja bijekcija, sta enako močni.

$\natnums$ vs $2\natnums$:
$$
\natnums \rarr 2\natnums \\
f(x) \mapsto 2x \\
\text{inverz}: f^{-1}(x) = \frac{x}{2} \implies f(x) \space \text{je bijskcija}
$$

Naravnih števil je enako kot sodih.

$\natnums$ vs $ℚ^+$:

```{mermaid}
block-beta
    columns 7
    4/1 space 4/2 space 4/3 space 4/4
    space:7
    3/1 space 3/2 space 3/3 space 3/4
    space:7
    2/1 space 2/2 space 2/3 space 2/4
    space:7
    1/1 space 1/2 space 1/3 space 1/4
    1/1 --> 2/1
    2/1 --> 1/2
    1/2 --> 1/3
    1/3 --> 2/2
    2/2 --> 3/1
    3/1 --> 4/1
    4/1 --> 3/2
    3/2 --> 2/3
    2/3 -- "..." --> 1/4
```

S taku ureditvijo pozitivnih racionalnih števil dokažemo, da jih je enako kot naravnih. Dodati še negativna racionalna števila pa je trivialno.