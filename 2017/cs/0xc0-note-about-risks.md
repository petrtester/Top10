# +R Poznámky k rizikům

## Jde o rizika, která představují slabiny

Metodika pro hodnocení rizik Top 10 je založena na [Metodice hodnocení rizik OWASP] (https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology). 
Pro každou kategorii Top 10 jsme na základě hodnocení nedostatků charakteristických pro standardní webovou aplikaci odhadli typické riziko, a to spolešným zkoumáním faktroů pravděpodobnosti a dopadových faktorů. Poté jsme seřadili Top 10 podle slabin, které obvykle představují nejvýznamnější riziko apro aplikaci. Tyto faktory jsou aktualizovány s každu novou verzí Top 10 podle toho, jak se věci mění a vyvíjejí.

[Metodika hodnocení rizik OWASP] (https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology) definuje řadu faktorů, které pomáhají vypočítat riziko zjištěné zranitelnosti. Top 10 však musí hovořit o obecnostech, nikoli o konkrétních zranitelnostech v reálných aplikacích a API. Při výpočtu rizik peo jednotlivé aplikace proto nikdy nemůžeme být tak přesní, jako vlastníci nebo správci apikací. Vy máte nejlepší předpoklady k tomu, abyste mohli posoudit důležitost vašich aplikací a dat, jaké jsou vaše hrozby, jak byl váš systém vybudován a provozován.

Naše metodologie zahrnuje tři faktory pravděpodobnosti pro každou slabost (prevalence, detekovatelnost a snadnost zneužití) a jeden faktor dopadu (technický dopad). Úroveň rizikovosti každého faktoru je klasifikována od 1 (nízká) do 3 (vysoká) s terminologií specifickou pro každý faktor. Rozšířenost je faktor, který obvykle nemusíte počítat. K údajům o rozšířenosti nám byly dodány statistiky rozšířenosti od řady různých organizací (jak je uvedeno v části Poděkování na straně 25), tato data jsme agregovali, abychom společně vytvořili seznam 10 nejpravděpodobnějších výskytů podle rozšířenosti. K výpočtu pravděpodobnosti každé zranitelnosti tato data byla poté zkombinována s dalšími dvěma faktory pravděpodobnosti (zjistitelnost a snadnost zneužití). Výsledná hodnota byla vynásobena průměrnou hodnotou závažnosti technického dopadu, což vedlo k celkovému hodnocení rizika pro každou položku v Top 10 (čím vyšší je výsledek, tím vyšší je riziko). Zjistitelnost, snadnost zneužití a dopad byly vypočteny na základě hlášených CVE přidružených ke každé kategorii z Top 10. 

**Poznámka**: Tento přístup nebere v úvahu pravedpodobnost aktéra hrozeb. Nezohledňuje ani žádné z různých technických podrobností souvisejících s vaší konkrétní aplikací. Kterýkoli z těchto faktorů by mohl významně ovlivnit celkovou pravděpodobnost, že útočník najde a zneužije konkrétní zranitelnost. Klasifikace rovněž nebere v úvahu skutečné důsledky pro váš obor. Vaše organizace bude muset rozhodnout, kolik bezpečnostních rizik z aplikací a API je ochotna přijmout vzhledem ke své kultuře, odvětví a regulačnímu prostředí. Účelem OWASP Top 10 není provádět tuto analýzu rizik za vás.

Následující obrázek ilustruje náš výpočet rizika pro **A6:2017-Security Misconfiguration**

![Risk Calculation for A6:2017-Security Misconfiguration](images/0xc0-risk-explanation.png)

