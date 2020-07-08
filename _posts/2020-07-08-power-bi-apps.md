---
title: "Power BI aplikace"
published: true
---

Aplikace v Power BI je druh obsahu a způsob prezentace dat koncovým uživatelům.
Aplikace mohou obsahovat několik řídících panelů (*dashboards*) a několik sestav (*reports*). 

> Vytváření aplikací vyžaduje licenci Pro nebo Premium.

Vezměme si příklad, kdy vedení organizace potřebuje přístup na řídící panel s přehledem KPI (*key performance indicators*), zároveň ale potřebuje i přehled zaměstnanců a jejich vytíženosti, což vyžaduje i personální oddělení.
Do toho obchodní oddělení vyžaduje přehled prodejnosti zboží na jednotlivých pobočkách včetně detailních pohledů a vizualizací.

![Záložka pro náhled instalovaných aplikací v Power BI](/images/power-bi-apps/power-bi-apps-01.png)

V Power BI je všechna zmiňovaná data možné zpřístupnit za pomocí udělení práv uživatelům na **pracovní prostor**, kde jsou dané vizualizace vytvořeny.
To však nemusí být praktické vzhledem ke složitější správě práv (prohlížení dat vs úprava dat) jednotlivých uživatelů a uživatelských skupin.

Microsoft tento problém vyřešil vyčleněním aplikací jako samostatných konsolidovaných prezentačních jednotek vytvářených z *pracovních prostor* a s oddělenými uživatelskými právy.

Aplikace lze distribuovat v rámci celé organizace, jednotlivým lidem nebo organizačním skupinám.

![Záložka pro náhled seznamu dostupných aplikací v Power BI](/images/power-bi-apps/power-bi-apps-02.png)

## FAQ

### Jaký je rozdíl mezi pracovním prostorem a aplikací?

Pracovní prostor je shromaždiště datových zdrojů, sestav a řídících panelů a tyto entity je v něm možné vytvářet a upravovat.
Aplikace je vytvářená z pracovního prostoru jako konsolidovaný výběr zdrojů, sestav, pohledů v pracovním prostoru, pro prezentaci koncovým uživatelům.

### Jak aktuální jsou data v aplikacích?

Zde jsem na úrovni domněnek, protože jsem neměl možnost danou funcionalitu sám vyzkoušet.
Aktuálnost dat v aplikacích Power BI pravděpodobně záleží na způsobu jakým je aktuálnost dat zajišťována v sestavách.
Jestliže je využívaná funkce automatické obnovy dat, pak by i v aplikaci měli být aktuální data.
Jestliže je však aktuálnost dat závislá na obnově datového zdroje, pak bude pravděpodobně nutné pro aktuální data aktualizovat ručně celou aplikaci.

### Kolik aplikací mohu z pracovního prostoru vytvořit?

Ve verzi Power BI aktuální k datu psaní tohoto článku je možné vytvořit pouze jednu aplikaci z pracovního prostoru.
Zkazky na forech k Power BI naznačují, že v budoucnu bude možné vytvářet z jednoho pracovního prostoru aplikací více.

[01]: https://docs.microsoft.com/cs-cz/power-bi/consumer/end-user-apps
[02]: https://powerbi.microsoft.com/en-us/blog/distribute-to-large-audiences-with-power-bi-apps/
[03]: https://docs.microsoft.com/en-us/power-bi/connect-data/refresh-data
[04]: https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-automatic-page-refresh
