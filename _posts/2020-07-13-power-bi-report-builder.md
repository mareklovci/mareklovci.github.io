---
title: "Použití nástroje Power BI Report Builder"
published: false
---

- [ ] TODO: Add folder `power-bi-report-builder/`

Společnost Microsoft ma vedle svého standardního nástroje **Power BI** nástroj **Power BI Report Builder**.
Ten slouží k vytváření stránkovaných sestav (paginated reports).
Rozdíl ve vlastnostech těchto dvou nástrojů jsou dobře shrnuty v přednášce [Microsoft Power BI: Designing Professional Paginated Reports with Report Builder][03].

| Paginated Reports          | Power BI Reporst             |
|:--------------------------:|:----------------------------:|
| Pages                      | Data mashup                  |
| Pixel perfect              | Interactive                  |
| Control over all elements  | Ad-hoc reporting             |
| Print friendly             | Visual                       |
| No export row limit        | Customer visuals             |
| Export to Multiple formats | Higher Level Aggregated Data |

Z výše uvedené tabulky lze vyčíst, že stránkované sestavy poskytují naprostou kontrolu nad obsahem, který je zobrazen.
Svým zaměřením se tedy hodí spíše pro vytváření sestav pro tisk nebo pro export do PDF nebo Word dokumentů.

## Tvorba stránkovaného reportu na základě sdíleného datasetu Power BI

V této části vycházím z oficiální dokumentace dostupné na stránce [Create a paginated report based on a Power BI shared dataset][01].

Po spuštění nástroje Power BI Report Builder a zavření uvítacího dialogového okna lze v pravém sloupci klinout pravým tlačítkem myši na položku **Data Sources**.
Poté se zobrazí nabídka **Add Power BI Dataset Connection**.

![Přidání sdíleného datasetu Power BI 1](/images/report-builder-01.png)

Poté lze vybrat zdroj, ze kterého chceme data čerpat.

![Přidání sdíleného datasetu Power BI 2](/images/report-builder-02.png)

Jakýkoliv pohled na data v nástroji vychází z tabulek.
Nelze jen překopírovat již vytvořené vizuály v Power BI a použít je v *Report Builder*.
Pro každý vizuál, který chceme "zkopírovat" je nutné vzít jeho podkladová data ve formě tabulky, které dostaneme DAX dotazem a tabulku na požadovaný vizuál dodatečně transformovat.
Kdybychom se pokusili vzít data rovnou ve takové formě, kterou dostaneme z DAX dotazů například pro kontingenční tabulky (*matrix*), tak se nám to nepodaří z podstaty toho, jak *DAX queries* fungují - pro složení kontingenční tabulky je nutné se dotázat na více dat, dostáváme tedy jakýsi stránkovaný objekt dat, který ale nedokáže *Report Builder* zpracovat.

### Jak získat DAX dotaz

> Následující část je jen volným překladem z [dokumentace](https://docs.microsoft.com/en-us/power-bi/paginated-reports/report-builder-shared-datasets#steps-to-get-the-dax-query)

- [ ] TODO

## Závěr

## Zdroje

1. [Create a paginated report based on a Power BI shared dataset][01]
2. [Stránkované sestavy][02]
3. [Microsoft Power BI: Designing Professional Paginated Reports with Report Builder][03]

[01]: https://docs.microsoft.com/en-us/power-bi/paginated-reports/report-builder-shared-datasets
[02]: https://docs.microsoft.com/cs-cz/power-bi/paginated-reports/report-builder-power-bi
[03]: https://youtu.be/uHWfzPls50c
