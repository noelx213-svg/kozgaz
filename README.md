# Közgazdaságtan Fogalomtanuló

Tanulóapp a közgazdaságtan alapfogalmaihoz. **Mind a 72 fogalom** benne van a három előadás fogalomtárából, egy sem maradt ki.

| Modul | Téma | Fogalmak |
|---|---|---|
| 1 | Közgazdaságtan alapfogalmai | 17 |
| 2 | Munkamegosztás és piac | 41 |
| 3 | Rugalmasság | 14 |
| | **Összesen** | **72** |

## Mit tud

- **Napi tanulóterv**: megadod a vizsga dátumát, az app szétosztja a 72 fogalmat a rendelkezésre álló napokra, és az utolsó két napra ismétlést meg próbavizsgát tesz.
- **Leitner-dobozos ismétlés (spaced repetition)**: minden fogalom 1-től 5-ig terjedő dobozba kerül. Ha tudtad, 1, 2, 4, 8, majd 16 nap múlva kérdez rá újra. Ha nem, visszaesik az 1. dobozba és másnap jön vissza. Ez a módszer bizonyítottan a leghatékonyabb fogalomtanulásra.
- **Tanulókártyák**: minden fogalomnál pontos definíció, bővebb magyarázat, konkrét példa, vizsgatipp, és hogy mely fogalmakkal szokták összekeverni.
- **Villámkártyák**: koppintásra forduló kártyák, "tudtam / nem tudtam" értékeléssel.
- **Kvíz**: háromféle kérdéstípus (definícióból a fogalom, fogalomból a definíció, példából a fogalom), véletlen sorrendű válaszokkal. Rossz válasznál megmutatja, hogy amit választottál, az valójában melyik fogalom, és miért nem az a helyes.
- **Próbavizsga**: 30 kérdés, 20 perces visszaszámlálóval, pontszámmal.
- **Gamifikáció**: XP, szintek, napi sorozat, 10 kitűző.
- **Haladás nézet**: dobozonkénti bontás, fogalmankénti statisztika, pontosság.

Minden offline működik, a haladás a böngésző localStorage-ában tárolódik. **Nincs szükség adatbázisra, API kulcsra és semmilyen fizetős szolgáltatásra.**

## Fájlszerkezet

```
index.html          # a teljes app egyetlen fájlban (HTML + CSS + 72 fogalom + tanulómotor)
README.md
```

Az app szándékosan egyetlen önálló fájl: nincs build, nincs függőség, bárhol megnyitható, akár offline is.

## Helyi futtatás

Dupla kattintás az `index.html` fájlra. Ennyi.

## GitHub + Vercel deploy

1. Hozz létre egy új repót a GitHubon, például `kozgaz-app` néven (üresen, README nélkül).
2. A projektmappában:

```bash
git init
git add .
git commit -m "init: közgazdaságtan fogalomtanuló app, 72 fogalom"
git branch -M main
git remote add origin https://github.com/noelx213-svg/kozgaz-app.git
git push -u origin main
```

Ha a commit rossz e-mail címmel menne fel:

```bash
git config user.email "noelx213@gmail.com"
git config user.name "noelx213-svg"
```

3. Vercel: **vercel.com/new**, Import from GitHub, válaszd a `kozgaz-app` repót.
4. A beállításoknál **Framework Preset: Other**, Build Command üresen, Output Directory üresen. Statikus oldal, nincs mit buildelni.
5. Deploy. Nem kell egyetlen environment variable sem.

Minden későbbi `git push` automatikusan újra deployol.

## Új fogalom hozzáadása

Az `index.html`-ben keresd meg a `window.CONCEPTS` tömböt, és vegyél fel egy új objektumot:

```js
{
  id: "egyedi-azonosito",      // kötőjeles, ékezet nélkül
  m: "m2",                     // melyik modul
  name: "Fogalom neve",
  short: "A pontos definíció, ez kerül a kártya hátuljára és a kvízbe.",
  long: "Bővebb magyarázat saját szavakkal.",
  example: "Konkrét példa.",
  tip: "Vizsgatipp, memóriafogás.",
  confuse: ["masik-fogalom-id"] // amikkel könnyű összekeverni, ezekből lesznek a kvíz rossz válaszai
}
```

A kvízkérdések automatikusan generálódnak, kézzel nem kell kérdést írni.
