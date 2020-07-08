---
title: "Výměna datového zdroje v Power BI"
published: true
---

Datové modely potřebují čas od času revidovat nebo přizpůsobit nově nastalé situaci.
Jestliže nechceme ohrozit funkčnost stávajících sestav Power BI a současně potřebujeme udělat závažnější zásah do datového modelu, tak by se hodilo, abychom byli schopni pro sestavy přepnout zdroj dat.

![Ukázka závislostí zdroje dat, modelu, sestav (reportů) a dashboardu](/images/power-bi-switch-data-source/switch-source-02.png)

Udejme příklad: návrhář má dostupný datový zdroj 1 a sestavu A.
Návrhář zjistí, že je potřeba udělat zásah do struktury modelu, ale nechce si rozbít model stávající.
Vytvoří kopii datového zdroje 1, tedy datový zdroj 2 a kopii sestavy A, sestavu B.
Návrhář přepne datový zdroj pro sestavu B, udělá změny v datovém zdroji 2, na sestavě B ověří, že změny nejsou pro sestavu destruktivní.
Jestliže je návrhář se změnou spokojen a model se sestavou fungují, může přepnout datový zdroj sestavy A z 1 na 2, a následně sestavu B a zdroj 1 smazat.

![Schéma přepnutí datových zdrojů](/images/power-bi-switch-data-source/switch-source-01.png)

Tato funkcionalita se hodí i v případě, že bychom měli načtených několik modelů stejné struktury s odlišnými daty.
Bylo by tak možné využít jednu sestavu pro prohlížení více zdrojů.

## Jak na to?

V **Power BI Desktop** otevřeme sestavu jejíž datový zdroj chceme změnit.
V záložce `Domů -> Transformovat data` kliněte na **Nastavení zdroje dat**.

![Změna zdroje dat 1](/images/power-bi-switch-data-source/switch-source-03.png)

Ze seznamu datových sad vyberte model, který chcete na sestavu aplikovat a klikněte na tlačítko **Vytvořit**.

![Změna zdroje dat 2](/images/power-bi-switch-data-source/switch-source-04.png)

Pro aplikování změn klikněte na tlačítko **Aktualizovat**, změny v modelu nebo datech by se tímto měli vypropagovat do sestavy.

![Změna zdroje dat 2](/images/power-bi-switch-data-source/switch-source-05.png)

## Závěr

Možnost vyměnit zdroj dat je velice důležitá funcionalita, jejíž absence by mohla způsobovat mnoho problémů.
Současné řešení není zrovna flexibilní, jelikož zdroj dat musí být nahrán do webové aplikace Power BI a možnost přepnutí je omezena pouze na desktopovou aplikaci.

[01]: https://www.c-sharpcorner.com/article/how-to-change-data-source-of-existing-report-in-power-bi/
[02]: https://windowsreport.com/change-data-source-power-bi/
