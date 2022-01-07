# Dungeon Crawler VS tutorial od [Hemisfera](https://www.hemisfera.sk). <img align="right" alt="hemisfera.sk" width="128px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/logo.png?raw=true" />
  
Tento návod ti pomôže vytvoriť vlastnú 2D hru žánru [Dungeon Crawler](https://www.youtube.com/watch?v=FQed13kgHSE). Hráč ovláda hrdinu, ktorý sa ocitol v mysterióznej jaskyni plnej nástrah a nepriatelov. Naprogramuj ho tak, aby sa mu podarilo z jaskyne dostať a zároveň, aby to pre teba ako hráča bola výzva.
  
Ak sa zasekneš alebo si nebudeš v niektorej časti istý, tak neváhaj spýtať sa lektora alebo jedného z tvojích spolužiakov. **Držíme ti palce!**
## Inštalácia
Aby si mohol začať programovat, tak potrebuješ mať stiahnuté unity, **verziu 2021** alebo novšiu. Ak ešte nemáš tak urob tak na [tomto linku](https://unity.com/download). Ak máš s inštaláciou problémy, tak skús si pozrieť [toto video](https://www.youtube.com/watch?v=9IKSJdNqzWg).
  
Ďalším krokom je stiahnuť si projekt z tejto github stránky. Takto nebudeš musiet nahadzovať grafiku, objekty do hernej scény a môžeš sa sústrediť na programovanie. V prípade, že máš grafiku vlastnú, tak **odporúčam ti aj tak si spraviť najprv všetko s touto grafikou** a potom na záver ju **vymeniť za vlasnú**.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/0.gif?raw=true" alt="Error" width="75%"/>
  
Keď máš projekt stiahnutí otvor si ho pomocou Unity Hubu. Ak máš nainštalovaných viacero verzii daj pozor aby si ju otvoril v tej 2021. 
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/01.gif?raw=true" alt="Error" width="75%"/>
  
Posledný krok je otvoriť si scénu **Level1**.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/02.gif?raw=true" alt="Error" width="75%"/>

## Pohyb hráča <img align="right" alt="hemisfera.sk" width="32px" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/player.png?raw=true" />
Poďme si rozpohybovať hráča. Nájdime si, kde v projekte máme objekt hráča uložený. Mal by sa nachádzať v **priečinku prefabs**. Následne si ho rozklikneme možnosťou **open prefab**. Tento krok je dôležitý, **nepreskakuj ho!** Keďže ide o hru s pohľadom zhora, tak hráč by sa mal vedieť hýbať do všetkých smerov.  

Pridajme hráčovi nový komponent typu Script machine, nazvime ho Player a uložme si tento graf do súboru.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/1.gif?raw=true" alt="Error" width="75%"/>
  
**Otvorme si graf** vo Visual Scripting editore a hurá! Môžeme sa pustiť do kódenia.
 >**_Tip 1: Zoom:_** Pomocou dvojkliku vo visual editor zóne si vieš zväčšiť alebo zmenšiť okno v ktoróm sa tvorí vizuálny skript. Pomôže ti to ak budeš tvoriť rozsiahlé skripty.

<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/2.gif?raw=true" alt="Error" width="75%"/>

Ako prvé musíme detekovať, kedy hráč stlačil klávesy na pohyb postavy. Najlepši spôsob je použiť príkaz **Get Axis Raw**. V ňom upresníme, či sa chceme snímať **horizontálny**(vľavo-vpravo) alebo **vertikálny**(hore-dole) pohyb. V našom prípade chceme oba typy sledovať, pretože hráč sa vie pohybovať do všetkých smerov.

>**_Príkaz: GetAxisRaw("Horizontal)_** funguje tak, že ak je stlačená šípka vpravo, tak príkaz da výslednu hodnotu 1. Naopak ak je stlačená šípka  vľavo, tak príkaz da výslednu hodnotu -1. To je pre nás užitočné lebo hodnotu použijeme na posun po X osy. Rovnako to platí pre vertikálny smer.

Výsledok príkazov si uložíme do nového **Vectoru3**(alebo Vectoru2, aj ten by fungoval správne, keďže robíme 2D hru).

>**_Príkaz: Vector3 Create_** nám vytvorí Vektor, ktorí hovorí o **smere a veľkosti** posunu pre ľubovolný herný objekt. Používať ho budeme vždy keď budeme chcieť hýbať objektami. 

<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/p1.gif?raw=true" alt="Error" width="75%"/>

Teraz keby si zavrel visual scripting okno a vrátil sa do hernej scény, môžeš hru pustiť. Všimni si, že hráč sa vie hýbať do všetkých smerov, akurat sa hýbe príšerne pomaly. Rýchlosť pohybu závisi od veľkosti vektora, ktorý posunieme do komponentu **RigidBody2D** *Set Velocity*. My mu teraz posúvame hodnoty -1, 1 poďla toho aké klávesy su stlačené. Prenásobme tieto hodnoty napríklad číslom 3 a uvidíme podstatné zrýchlenie. 
  
Dobrou praxou je si hodnotu 3 ktorou chceme prenásobiť rýchlosť hráča uložiť do **hernej premennej**, ktorú nazveme napríklad **speed**. Ak by niekto pozeral náš skript tak bude lepšie rozumieť slovu speed ako náhodnemu číslu 3. 
  
**Typy premenných:**
- **Float** predstavuje desatinné čísla naprílad: 0.5, -0.123, 1669, ...
- **Integer** predstavuje celé čísla: -1, 0, 1, 2, 3...
- **String** predstavuje textové reťazce: "Hello, World!", "Flying type", "Walking type" ...
- **Boolean** predstavuje logické hodnoty *True* alebo *False*. 
- **Iné:** Unity nám dovoľuje vytvárať premenné aj komplikovanejších typov ako napríklad *Vector3*, *GameObject*...

>**_Tip 2: Zrušenie prepojenia v grafe:_** ak chceš **zrušiť prepojenie** dvoch príkazov, tak jednoducho klikni **pravým tlačidlom myšky** na začiatok alebo koniec prepájacej čiary.

>**_Tip 3: Pomenovanie premenných:_** prográmatori sa dohodli, že herné premenné budú vždy nazývať malým písmenom. Ak ide o zloženie slov napríklad *playerLife*, tak prvé slovo je malým písmenom a každé ďaľšie slovo začína veľkým. Medzeri v názve nesmú byť!
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/p2.gif?raw=true" alt="Error" width="75%"/>

>**_Komponent RigidBody2D_** je spôsob akým vieme povedať nástroju Unity aby aplikoval fyzikálne pravidlá na daný herný objekt. My ho využívame iba na to aby sme mu priradili rýchlosť a pohli hráčom v danom smere pokiaľ nám neprekáža nejaký pevný objekt. V inom type hry by mohli byť užitočne aj iné vlastnosti *Rigidbody* komponentu ako gravitácia(napríklad pri platformer hre) alebo hmotnosť(pri zrážke dvoch rovnako rýchlych objektov odletí ďalej ten čo ma menšiu hmotnosť).
  
<img width="25%" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/rigdbody.PNG?raw=true" />
  
Rýchlosť hráča máme vyriešenú, pokiaľ chceš možeš mu pridať alebo ubrať z hodnoty 3. Ešte takým vizuálnym vylepšením by bolo otočiť obrázok hráča do smeru v ktoróm sa pohybuje. Najlepší spôsob riešenia je použitím komponentu **Sprite Renderer**. A to pomocou premennej **Flip X**. Ak hodnotu premennej označíš v editore ako pravdivú, hráč sa bude pozerať opačným smerom.
  
<img width="25%" src="https://github.com/Zuvix/DungeonGame/blob/main/Images/sprite.PNG?raw=true" />
  
Teraz podobnú vec spravíme vo visual scripte. Pomocou príkazu **if** rozdelíme hlavný tok programu na vetvu v ktorej hráč kráča smmerom vľavo a vetvu v ktorej kráča vpravo. Aby program vedel podľa čoho si má vetvu vybrať tak porovnáme veľkosť **X súracnice** s hodnotou 0. **Výsledok porovnania** potom vložíme ako vstup do príkazu **if**.
  
<img src="https://github.com/Zuvix/DungeonGame/blob/main/Images/p3.gif?raw=true" alt="Error" width="75%"/>

>**_Tip 4: Kopírovanie príkazov:_** najľahší spôsob ako kopírovať je pomocou **označenia príkazu na kopírovanie** a klávesovej skratky **Ctrl + D**.
