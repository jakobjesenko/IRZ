## Uproaba leme o napihovanju za RJ
Uporablja se za dokazovajne, da nek jezik ni regularen.
$$
\begin{equation*}
\begin{split}
    \text{Jezik } L \text{ je regularen} \implies \\
    \forall w \isin L: \exist x, y, z: w=xyz \implies \\
    \forall i \ge 0: x y^i z \isin L
\end{split}
\end{equation*}
$$
Lemo obrnemo v negirano obliko, da jo lahko uporabljamo za dokazovanje.
$$
\begin{equation*}
\begin{split}
    \exist w \isin L: \forall x,y,z: w=xyz \implies \\
    \exist i \ge 0: x y^i z \not\isin L \implies \\
    L \text{ ni regularen}
\end{split}
\end{equation*}
$$

### Metoda dokazovanja
Za dani jezik $L$ želimo dokazati, da ni regularen.

Obstaja dovolj dolga beseda ($|w| \ge n$), ki je v jeziku $L$, za katero velja: Za vsako razbitje besede $w=xyz$ obstaja konstanta $i \ge 0$, tako da beseda napihnjenka $x y^i z$ pade izven jezika $L$. Tak jezik ni regularen.
$$
\exist w \isin L \wedge |w| \ge n: \forall x,y,z: w = xyz: \exist i \ge 0: x y^i z \not\isin L
$$
1. $n$ je konstanta odvisna samo od jezika $L$
2. Izberemo dovolj dolgo besedo iz jezika $L$