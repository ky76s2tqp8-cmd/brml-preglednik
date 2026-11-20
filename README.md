# BRML preglednik

Web-aplikacija za pregled difraktograma praha:

- Bruker **.brml** (DIFFRAC.SUITE), binarni Bruker **.raw** (v1, v2, v3/RAW1.01, v4), PANalytical **.xrdml**, Philips **.rd/.sd** i **.udf** te tekstne XY datoteke
- zumiranje, očitanje 2θ / d / I, prianjanje uz vrh, oznake
- preklapanje više difraktograma (pomak, normiranje)
- učitavanje **.cif** i izračun položaja i relativnih intenziteta refleksa

Datoteke se obrađuju isključivo lokalno u pregledniku. Nakon prvog otvaranja radi i bez interneta
(na iPhoneu: Safari → Dijeli → „Dodaj na početni zaslon”).

## Amorfni udio (`amorfno.html`)

Zasebna web-aplikacija za semikvantitativnu procjenu udjela amorfne faze, bez CIF-a i strukturnog modela
(postupak s dvjema krivuljama, po uzoru na procjenu kristalnosti u DIFFRAC.EVA):

- **ovojnica A(2θ)** nebraggovskog intenziteta — Whittakerovo izglađivanje s iterativnim isključivanjem točaka više od t·σ iznad krivulje (σ = c·√I, c iz drugih diferencija sirovih podataka)
- **instrumentalna pozadina B(2θ)** — Čebiševljev polinom (+ član c/2θ, c ≥ 0) prilagođen donjoj strani ovojnice asimetričnim najmanjim kvadratima
- X<sub>am</sub> = K·I<sub>a</sub> / (K·I<sub>a</sub> + I<sub>c</sub>), I<sub>c</sub> = ∫(I − A) d2θ, I<sub>a</sub> = ∫max(A − B, 0) d2θ
- raspon osjetljivosti (L × 0,75–1,25, t ± 0,5, stupanj ± 1), tablica za sve učitane uzorke, izvoz CSV/TXT
- predlošci postavki: „Staklasti uzorak” (pepeo, staklo) i „Pretežno kristalni” (klinker, filer)

Drugi postupak, **prilagodba profila** (bez strukturnog modela): pseudo-Voigtovi maksimumi s Kα1/Kα2 dubletom
(pojedinačni položaji i širine, zajednički η), jedan ili dva Gaussova haloa i Čebiševljeva pozadina (+ c/2θ);
linearni koeficijenti nenegativnim težinskim najmanjim kvadratima, nelinearni Gauss–Newtonovim koracima, maksimumi
se dodaju iz ostatka. Lorentzovi repovi i preklopljene skupine refleksa time ostaju u kristalnom doprinosu, što
je važno za klinker i filer. Uz rezultat se navode R<sub>wp</sub>, GOF, statistička nesigurnost i raspon osjetljivosti;
izračun se odvija u pozadinskoj niti (Web Worker).

Rezultat je udio integriranog intenziteta, a ne maseni udio (vidi „Metoda i ograničenja” u aplikaciji).
Na iPhoneu: otvorite `amorfno.html` u Safariju → Dijeli → „Dodaj na početni zaslon”.

