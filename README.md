# Babická plošina – Speleologické mapy (Therion)

Tento repozitář obsahuje kompletní speleologickou mapovou a měřičskou dokumentaci krasových jevů Babické plošiny v jižní části CHKO Moravský kras (k. ú. Babice nad Svitavou, Kanice, Ochoz u Brna).

Měřické a průzkumné práce provádí **ZO ČSS 6-28 Babická speleologická skupina**.

---

## 📊 Statistický přehled lokalit a jeskyní

| Skupina / Lokalita | Číslo | Název jeskyně / jevu | Délka polygonu | Hloubka / Denivelace | Nadm. výška vchodu | Poznámka |
|---|---|---|---|---|---|---|
| **01 Zadní pole** | 1318 | **Větrná propast** | **610 m** | **-124,5 m** | cca 528 m n. m. | Nejhlubší jeskyně Babické plošiny, aktivní průvan |
| **01 Zadní pole** | 1303 | **Dvanáctka (Závrt č. 12)** | **75,5 m** (289 m celkem) | **-35,1 m** | cca 526 m n. m. | V hloubce -22 m fyzicky propojena s Větrnou |
| **01 Zadní pole** | 1319 | **Devítka (Závrt č. 9)** | **34,5 m** | **-19,5 m** | cca 527 m n. m. | Výrazný propasťovitý závrt |
| **01 Zadní pole** | 1320 | **Desítka (Závrt č. 10)** | povrch | – | cca 527 m n. m. | Povrchový závrt v řadě |
| **01 Zadní pole (celek)** | – | **Celá skupina Zadní pole** | **934 m** | **124,5 m** | 526–528 m n. m. | 1 098 měřických bodů, 10 smyček, chyba 1,54 % |
| **02 Člopy a okolí** | 1302 | **Ve Člopech** | **26,9 m** | **-17,0 m** | cca 478 m n. m. | Ponorový kras |
| **03 Skalky** | 1313 | **Babička & Babička II** | **336,4 m** | **25,0 m** | cca 470 m n. m. | Skupina vývěrové větve u Kanic |

---

## 🗺️ Publikační mapy Zadního pole (nové exporty)

Pro publikační účely a tisk byly vytvořeny dedikované layouty a konfigurační soubory s prefixem `new_` (původní soubory repozitáře zůstávají nedotčeny):

1. **Celkový plán skupiny Zadní pole (1 : 250)**:
   - Konfigurace: `babice/01_zadni_pole/new_zadni_pole.thconfig`
   - Výstup: `babice/01_zadni_pole/_output/new_zadni_pole_plan.pdf`
   - Výstup (barevný dle hloubky): `babice/01_zadni_pole/_output/new_zadni_pole_alt.pdf`
   - *Obsahuje kompletní situaci jeskynního systému včetně povrchových závrtů č. 9, 10, 12 a Větrné propasti.*

2. **Detailní plán jeskynního systému (1 : 200)**:
   - Konfigurace: `babice/01_zadni_pole/new_zadni_pole_jeskyne.thconfig`
   - Výstup: `babice/01_zadni_pole/_output/new_zadni_pole_jeskyne_plan.pdf`
   - Výstup (barevný dle hloubky): `babice/01_zadni_pole/_output/new_zadni_pole_jeskyne_alt.pdf`
   - *Fokusovaný výřez s maximální čitelností a detaily chodeb (1318 Větrná propast, 1303 Dvanáctka, 1319 Devítka).*

### Vlastnosti publikačního layoutu:
- **Podklad**: Čistý bílý papír (`color map-bg 100`) optimalizovaný pro tisk a odbornou publikaci.
- **Výplň chodeb**: Přírodní pastelový vápencový tón (`color map-fg [92 88 82]`), který neruší morfologii a sedimenty.
- **Kartografické značky**: Mezinárodní norma UIS doplněná o automatické textury sedimentů (bloky, hlíny, písky, sintry).
- **Legenda a typografie**: Kompletní české texty (`language cz`), strukturované záhlaví, metrické grafické měřítko a přehledná dvou-sloupcová legenda.

---

## 🌐 Geodetický a souřadnicový systém

- Původní projekty využívaly definice `cs JTSK` / `cs iJTSK`, které v moderních knihovnách PROJ 9 vyžadovaly nedostupný transformační grid a způsobovaly chyby kompilace.
- Projekt byl kompletně sjednocen na mezinárodní standard **S-JTSK / Křovák East-North (`EPSG:5514`)**.
- Body totální stanice v [babice/povrchova_mereni/totalka.th](babice/povrchova_mereni/totalka.th) jsou zapsány ve standardním tvaru:
  ```therion
  cs EPSG:5514
  fix  <bod_id>  -Y  -X  Z
  ```
- Tím je zajištěna stoprocentní kompatibilita s moderními GIS aplikemi (QGIS, ArcGIS) i nástrojem Therion na všech platformách (Linux, macOS, Windows).

---

## 🛠️ Jak kompilovat mapy

### Požadavky
- [Therion](https://therion.speleo.sk/) (doporučena verze >= 6.0)
- [Survex](https://survex.com/) (`cavern` vyžadován Therionem pro vyrovnání polygonových sítí)
- TeX distribuce (TeX Live / pdfTeX)

### Kompilační příkazy

```bash
# 1. Kompilace celého přehledu Babic (1:2000)
cd babice
therion babice.thconfig

# 2. Kompilace nových publikačních map Zadního pole (1:250 celková / 1:200 jeskyně)
cd 01_zadni_pole
therion new_zadni_pole.thconfig
therion new_zadni_pole_jeskyne.thconfig

# 3. Kompilace skupiny Skalky (1313 Babička)
cd ../03_skalky
therion skalky.thconfig
```

---

## 📁 Struktura adresářů

```
├── layouts                                    # Společné šablony a styly Therionu
├── README.md                                  # Tento dokument
└── babice/
    ├── babice.thconfig                        # Hlavní souhrnný projekt celé oblasti
    ├── povrchova_mereni/                      # Geodetická povrchová měření (totální stanice)
    ├── 01_zadni_pole/                         # Oblast Zadní pole (Větrná, Dvanáctka, Devítka)
    │   ├── new_zadni_pole.thconfig            # Publikační mapa Zadní pole (1:250)
    │   ├── new_zadni_pole_jeskyne.thconfig     # Publikační mapa jeskyní (1:200)
    │   ├── zadni_pole.thconfig                # Původní konfigurace
    │   ├── 1318_vetrna_propast/               # 1318 Větrná propast
    │   ├── 1303_dvanactka/                    # 1303 Dvanáctka
    │   └── 1319_devitka/                      # 1319 Závrt č. 9
    ├── 02_clopy_a_okoli/                      # Ponorová oblast Ve Člopech
    └── 03_skalky/                             # Skupina Skalky u Kanic (Babička)
```

---

## 📜 Licence a autorství

Měřická data, skici a mapy: **ZO ČSS 6-28 Babická speleologická skupina** (1974–2026).
Všechna práva vyhrazena. Použití dat a map pro publikaci podléhá souhlasu ZO ČSS 6-28.
