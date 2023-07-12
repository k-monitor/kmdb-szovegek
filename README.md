# K-Monitor Sajtóadatbázis Egységesítés
A ([K-Monitor sajtóadatbázisának](https://adatbazis.k-monitor.hu)) cikkeihez tartozó szövegek összegyűjtését, egységesítését és további felhasználását célul kitűző projekt.

Összes sajtóadat fájl szövegét egy jsonl fájlba news_id alapján egységesíteni ([eredeti repo itt](https://github.com/everybitmihaly/KMonitorSajtoadatEgysegesites)). 

# Meglévő összefoglalás 2023 Március - kmdb-export-20220302.csv alapján (52543 cikk)
A dump-ban 52880 sor van, ebből 52363 rekordnak van unique url+publication_date metaadata.

Colab az összeegyeztetéshez: https://colab.research.google.com/drive/13Cjig3iEvVIs6DGacqrc6TMlInNw_Qvq?usp=sharing

## Három forrás: 
- valszeg ok (k-monitor gyűjtés, főként a sajtóadatbázis első pár évéből) - https://drive.google.com/drive/folders/18Zm4l8g7LxDsm5QVUgDN4HSGZS9ZqA8P?usp=share_link
    - fájlok száma: 11590
    - fájl neve a sajtóadatbázisban ID-ként szerepel
    - fájlok formátuma:
        - .txt: 7438
        - .rtf: 3491
        - '': 448
        - .odt: 132
        - .doc: 63
        - .docx: 17
        - .PNG: 1

- belső link (k-monitor gyűjtés, főként a sajtóadatbázis legelső pár évéből) - https://drive.google.com/drive/folders/1beVKksfuaezmtKb2Y0hiLNjw_16UU-Jt
    - fájlok száma: 4534
    - fájl neve a sajtóadatbázisban Belső linkként szerepel
    - sajtóadatbázis export: https://shared.deepdata.hu/kmdb-export-20230321.zip
    - fájlok formátuma:
        - .doc: 3180
        - .rtf: 1341
        - .txt: 13
    
- boa gyűjtés (CommonCrawl)           - https://drive.google.com/drive/folders/1caz8KTtkcCY8iOjfjR16cKvpUKQr5-vR
    - fájlok száma: 24554
    - fájlok formátuma: .csv fájlban van tárova
    - * a valszeg_ok fájlok közül 2470 van meg itt (normalizálva)

# tervek, ötletek
- jó lenne egy vagy több scraper, ami automatikusan leszedi a felvitt cikkek szövegét a megadott url-ből. extrajó, ha valahogy a mostani admin felületbe épülve ellenőrzésre feladja a cikkbeviőnek (hogy ki tudjuk szűrni a fölös szövegrészeket, reklámokat).
- meg kellene oldani a szövegek tárolását, mert jelenleg ilyen-olyan drive-okon vannak. ezalatt értem azt is, hogy tudjuk ezt élő adatbázisként használni, bővíteni, elemzésre könnyen hozzáférhetővé tenni.
- ha ez az előző megvan, lehetne ötletelni, hogy hogyan tudjuk a szövegeket felhasználni AI segítségével a cikkbevitel automatizálásához. ez történhet több lépcsőben:
        - első körben url alapján címkejavaslatokat feladása, amit a cikkbevivő hagy jóvá
        - végső fázisban egy crawler keresi a hasonló és releváns cikkeket, amiket fel is címkéz
