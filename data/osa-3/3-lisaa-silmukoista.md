---
path: '/osa-3/3-lisaa-silmukoista'
title: 'Lisää silmukoista'
hidden: false
---

<text-box variant='learningObjectives' name='Oppimistavoitteet'>

Tämän osion jälkeen

- Osaat keskeyttää silmukan `break`-komennolla
- Osaat siirtyä silmukan seuraavalle kierrokselle `continue`-komennolla
- Ymmärrät sisäkkäisen silmukan toiminnan

</text-box>

## break-komento

Aiemmin silmukoiden yhteydessä tutustuttiin `break`-komentoon. Komennolla voidaan katkaista silmukan suoritus välittömästi. Tyypillinen esimerkki komennon käytöstä on silmukka, jossa kysytään käyttäjältä syötteitä, ja suoritus päättyy, kun käyttäjä antaa tietyn syötteen.

Vastaavaan toiminnallisuuteen päästään myös ilman `break`-komentoa sopivan ehdon avulla. Alla olevat esimerkit toteuttavat molemmat ohjelman, joka laskee käyttäjän syötteiden summan kun käyttäjä syöttää luvun -1:

```python
# 1. versio break-komennon avulla

summa = 0

while True:
    luku = int(input("Anna luku, -1 lopettaa: "))
    if luku == -1:
        break
    summa += luku

print ("Summa on", summa)
```

```python
# 2. versio ilman break-komentoa

summa = 0
luku = 0

while luku != -1:
    luku = int(input("Anna luku, -1 lopettaa: "))
    if luku != -1:
        summa += luku

print ("Summa on", summa)
```

Molempien ohjelmien esimerkkisuoritus voisi näyttää seuraavalta:

<sample-output>

Anna luku, -1 lopettaa: **2**
Anna luku, -1 lopettaa: **4**
Anna luku, -1 lopettaa: **5**
Anna luku, -1 lopettaa: **3**
Anna luku, -1 lopettaa: **-1**
Summa on 14

</sample-output>

Molemmat versiot ovat toiminnallisuudeltaan siis käytännössä samanlaisia. Ensimmäinen tapa on kuitenkin käytännössä parempi, koska ehto `luku == -1` riittää kirjoittaa vain kerran eikä muuttujaa `luku` tarvitse alustaa silmukan ulkopuolella.

Komentoa `break` voidaan käyttää myös silloin, kun silmukassa on annettu jokin muu ehto kuin pelkkä totuusarvo `True`. Esimerkiksi seuraava silmukka jatkuu niin kauan, kuin annettujen lukujen summa on enintään 100. Kuitenkin silmukka katkeaa myös, jos käyttäjä antaa luvun -1.

```python
summa = 0

while summa <= 100:
    luku = int(input("Anna luku, -1 lopettaa: "))
    if luku == -1:
        break
    summa += luku

print("Summa on", summa)
```

Mahdollisia suorituksia:

<sample-output>

Anna luku, -1 lopettaa: **15**
Anna luku, -1 lopettaa: **8**
Anna luku, -1 lopettaa: **21**
Anna luku, -1 lopettaa: **-1**
Summa on 44

</sample-output>

<sample-output>

Anna luku, -1 lopettaa: **15**
Anna luku, -1 lopettaa: **8**
Anna luku, -1 lopettaa: **21**
Anna luku, -1 lopettaa: **45**
Anna luku, -1 lopettaa: **17**
Summa on 106

</sample-output>

Ensimmäisessä tapauksessa silmukka päättyy, koska käyttäjä antaa luvun -1. Toisessa tapauksessa silmukka päättyy, koska lukujen summa on yli 100.

Toisaalta voisimme toteuttaa vastaavasti toimivan silmukan myös näin:

```python
summa = 0

while True:
    luku = int(input("Anna luku, -1 lopettaa: "))
    if luku == -1:
        break
    summa += luku
    if summa > 100:
        break

print("Summa on", summa)
```
## continue-komento

Komento `continue` on toinen tapa vaikuttaa silmukan suoritukseen. Kun silmukan sisällä tulee vastaan komento `continue`, hyppää suoritus välittömästi silmukan alkuun riville, jossa on silmukan ehto. Tämän jälkeen silmukan suoritus jatkuu normaalisti ehdon tarkastamisella:

<img src="3_3.png">

Esimerkiksi seuraava ohjelma laskee summaan mukaan vain luvut, jotka ovat pienempiä kuin 10. Jos luku on 10 tai suurempi, suoritus palaa silmukan alkuun eikä lukua lisätä summaan.

```python
summa = 0

while True:
    luku = int(input("Anna luku, -1 lopettaa: "))
    if luku == -1:
        break
    if luku >= 10:
        continue
    summa += luku

print("Summa on", summa)
```

<sample-output>

Anna luku, -1 lopettaa: **4**
Anna luku, -1 lopettaa: **7**
Anna luku, -1 lopettaa: **99**
Anna luku, -1 lopettaa: **5**
Anna luku, -1 lopettaa: **-1**
Summa on 16

</sample-output>

## Sisäkkäiset silmukat

Silmukoita voidaan kirjoittaa toisten silmukoiden sisään. Esimerkiksi seuraava ohjelma kysyy käyttäjältä silmukassa luvun ja tulostaa sen avulla lukujonon toisen silmukan avulla:

```python
while True:
    luku = int(input("Anna luku: "))
    if luku == -1:
        break
    while luku > 0:
        print(luku)
        luku -= 1
```

<sample-output>

Anna luku: **4**
4
3
2
1
Anna luku: **3**
3
2
1
Anna luku: **6**
6
5
4
3
2
1
Anna luku: **-1**

</Sample-output>

Huomaa, että kun silmukkoja on sisäkkäin, komennot `break` ja `continue` vaikuttavat vain sisimpään silmukkaan. Esimerkiksi voisimme toteuttaa äskeisen ohjelman vähän eri tavalla myös näin:

```python
while True:
    luku = int(input("Anna luku: "))
    if luku == -1:
        break
    while True:
        if luku <= 0
            break
        print(luku)
        luku -= 1
```

Nyt jälkimmäinen `break`-komento keskeyttää vain sisimmän silmukan, joka tulostaa lukuja, jos ehto `luku <= 0` pätee.


<in-browser-programming-exercise name="Sanojen ensimmäiset kirjaimet" tmcname="osa03-16_sanojen_ensimmaiset_kirjaimet">

Tee ohjelma, joka kysyy käyttäjältä lauseen. Ohjelma tulostaa jokaisen sanan ensimmäisen kirjaimen ruudulle omille riveilleen.

Esimerkkisuoritus:

<sample-output>

Anna lause: **Vesihiisi sihisi hississä**
V
s
h

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Kertomat" tmcname="osa03-17_kertomat">

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun. Jos käyttäjä syöttää negatiivisen luvun tai nollan, ohjelman suoritus päättyy. Muuten ohjema tulostaa luvun kertoman.

Kertoma lasketaan kertomalla keskenään luku ja kaikki sitä pienemmät positiiviset kokonaisluvut. Esim. luvun 5 kertoma on 1 * 2 * 3 * 4 * 5 == 120.

Esimerkkisuorituksia:

<sample-output>

Anna luku: **3**
Luvun 3 kertoma on 6
Anna luku: **4**
Luvun 4 kertoma on 24
Anna luku: **-1**
Kiitos ja moi!

</sample-output>

<sample-output>

Anna luku: **1**
Luvun 1 kertoma on 1
Anna luku: **0**
Kiitos ja moi!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Parit ympäri" tmcname="osa03-18_parit_ympari">

Tee ohjelma, joka tulostaa luvut 1:stä käyttäjän antamaan lukuun. Luvut on kuitenkin käännetty pareittain ympäri.

<sample-output>

Anna luku: **5**
2
1
4
3
5

</sample-output>

<sample-output>

Anna luku: **6**
2
1
4
3
6
5

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Vuorotellen" tmcname="osa03-19_vuorotellen">

Tee ohjelma, joka kysyy käyttäjältä luvun ja tulostaa sitten lukuja vuorotellen seuraavien esimerkkien mukaisesti.

<sample-output>

Anna luku: **5**
1
5
2
4
3

</sample-output>

<sample-output>

Anna luku: **6**
1
6
2
5
3
4

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Kirjainruudukko" tmcname="osa03-20_kirjainruudukko">

Tee ohjelma, joka tulostaa kirjainruudukon oheisten esimerkkien mukaisesti. Voit olettaa, että kerroksia on enintään 26.

<sample-output>

Kerrokset: **3**
<pre>
CCCCC
CBBBC
CBABC
CBBBC
CCCCC
</pre>

</sample-output>

<sample-output>

Kerrokset: **4**
<pre>
DDDDDDD
DCCCCCD
DCBBBCD
DCBABCD
DCBBBCD
DCCCCCD
DDDDDDD
</pre>

Varoitus: tämä tehtävä on suhteellisen haastava, eli älä masennu, jos et saa tätä heti ratkaistua. Älä juutu tähän tehtävään, vaan tee ensin osa loppuun ja palaa tehtävään sen jälkeen. Voi myös olla ihan viisasta jättää tämä tehtävä kokonaan myöhemmäksi.

</sample-output>

</in-browser-programming-exercise>

<quiz id="7398bca5-c470-5fba-8721-e6f40fc2e4a1"></quiz>
