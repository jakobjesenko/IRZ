# Izračunljivost in računska zahtevnost (IRZ)

## Uvodno predavanje

### Motivacija
Kaj pomeni računati? Kakšni so računski problemi? Obstajajo odločitveni (da/ne) in bolj zahtevni (rezultat je število,...). Ali lahko problem rešimo v vsakem primeru? Če ne - je tak problem nerešljiv. Kako dokazujemo ali je problem izračunljiv?

Probleme delimo na:
1. neizračunljive
2. izračunljive:  
   - koliko časa rabimo za zrešitev problema?


Imeli bomo 2 kolokvija (novembra, januarja) in bosta pogoj za izpit 😢.

### Računalništvo
1. Aplikativno
2. teoretično  
   cilji:
   - kaj je že uresničeno
   - kaj se še da uresničiti
   - česa se ne da uresničiti

Kaj je **model računanja**?
model računanja je formalna definicija osnovnih pojmov in sestavin algoritmičnega računanja.

Spoznali bomo naslednje:
- Končni avtomati
- Skladovni avtomati
- Turingovi stroji

### Formalni jezik
- Simbol ($a, b, c,\dotso$)
- beseda = kočno zaporedje *Staknjenih* simbolov ($aabcc$)
- spremenljivke (besedne) zavzemajo vrednosti, ki so besede ($x, y, z,\dotso$)
- Dolžina besede: $|w| = l$
- Prazna beseda: $|\epsilon| = 0$
- Predpona/pripona (je prava, če ni enaka besedi sami)
- Stik/konkatenacija $u=aa, v=bb \iff uv=aabb$
- Abeceda je končna množica simbolov
- Formalni jezik nad abecedo je množica nekaterih besed iz simbolov dane abecede. Tudi $\{\epsilon\}$ in $\empty$
- jezik $\Sigma^*$ je množca ivseh besed nad abecedo $\Sigma$

### Matematična indukcija
*Se pusti bralcu za vajo 😉*