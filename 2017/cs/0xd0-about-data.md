# +MD Metodika a data

Na summitu projektu OWASP aktivní účastníci a členové komunity se rozhodli představit dvě slibné třídy zranitelnosti, pořadím definovaným částečně kvantitativními daty a částečně kvalitativními průzkumy.
 
## Průzkum podle odvětví

Pro tuto studii jsme vybrali kategorie zranitelností, které byly dříve označovány jako "na vrcholu" nebo byly zmíněny ve zpětné vazbě pro 2017 RC1 v Top 10 e-mailové konferenci. Hodnotili jsme tato data a požádali respondenty, aby identifikovali čtyři top zranitelnosti, které by by měly být zahrnuty do OWASP top 10 - 2017. Průzkum byl proveden od 2. srpna do 18. září 2017. Bylo shromážděno 516 odpovědí, podle nichž byla stanovena kritičnost zranitelností.

| Kritičnost | Kategorie zranitelnosti podle průzkumu | Skóre |
| -- | -- | -- |
| 1 | Exposure of Private Information ('Privacy Violation') [CWE-359] | 748 |
| 2 | Cryptographic Failures [CWE-310/311/312/326/327]| 584 |
| 3 | Deserialization of Untrusted Data [CWE-502] | 514 |
| 4 | Authorization Bypass Through User-Controlled Key (IDOR & Path Traversal) [CWE-639] | 493 |
| 5 | Insufficient Logging and Monitoring [CWE-223 / CWE-778]| 440 |

Exposure of Private Information (Expozice soukromých informací) je bezpochyby nejkritičtější zranitelností, ale pouze dopňuje stávající kategorii **A3:2017 Expozice citlivých dat**. To zahrnuje také zranitelná místa, související se šifrováním. Nejistá deserializace byla v průzkumu na třetím místě, takže vyhodnocení rizika byla přidána do Top 10 jako kategorie **A8:2017 Nezabezpečená deserializace**. Pod čtvrtou zranitelností byla uvedena položka týkající se týkající se uživatelských klíčů, kerá je zahrnuta pod **A5:2017 Nefunkční řízení přístupu**. Je dobré vidět, že se v průzkumu umístila na vysoké pozici, protože není mnoho údajů o slabých stránkách autorizace. Páté na seznamu byly chyby v protokolování a monitorování, které se přidaly do kategorie Top 10 **A10:2017 Nedostatečné logování a monitorování**. Přenesli jsme se do bodu, kdy aplikace musí být schopny definovat, co může být útok a zaznamenávat související události a zobrazovat a reagovat na výstrahy. 

## Otevřený sběr dat

Tradičně byla data shromažďována a analyzována na základě četnosti: kolik zranitelností bylo nalezeno aplikace. Jak je dobře známo, že nástroje tradičně hlásí všechny nalezené případy zranitelnosti a lidé tradičně hlásí jeden nález s řadou příkladů. Proto je při analýze obtížné kombinovat tyto dva přístupy.

Pro rok 2017 byla míra výskytu zranitelnosti vypočítána na základě počtu aplikací, které mají jednu nebo více zranitelnosti určitého typu. Většina dat byla poskytována ve dvou verzích: První byl tradiční frekvenční styl počítání každé instance zjištěné zranitelnosti, zatímco druhý byl počet aplikací, ve kterých byla každá zranitelnost nalezena (jednou nebo vícekrát). Navzdory nedokonalosti tento přístup umožňuje porovnat získané údaje z nástrojů asistovaných člověkem (Human Assisted Tools) a lidí asistovaných nástroji (Tool Assisted Humans). Nezpracovaná data a výsledky analýz jsou [k dispozici na  GitHubu] (https://github.com/OWASP/Top10/tree/master/2017/datacall). [k dispozici v GitHubu] (https://github.com/OWASP/Top10/tree/master/2017/datacall). Pro budoucí verze Top 10 pro tyto účely se plánuje vytvoření další struktury.

Na výzvu k shromažďování informací jsme obdrželi více než 40 datových souborů. Většina z nich byla identická se získanými během počátečního sběru (na základě přístupu založeného na frekvenci), takže jsme použili pouze 23 zdrojů pokrývající ≈ 114 tisíc aplikací. Kdykoli to bylo možné, převzali jsem data od jednoho zdroje za období jednoho roku. Většina aplikací je jedinečná, i když uznáváme, že  existuje možnost opakovaných aplikací (Veracode). 23 použitých datových souborů bylo identifikováno buď jako testování pomocí lidí asistovaných nástroji, nebo konkrétně za předpokladu míry výskytu z testování pomocí nástrojů asistovaných člověkem. Anomálie ve vybraných datech s frekvencí nad 100% byly upraveny na max. 100%. Pro výpočet míry výskytu jsme vypočítali procento z celkového počtu aplikací, u kterých bylo zjištěno, že obsahují daný typ zranitelnosti. Pořadí výskytu bylo použito pro výpočet rozšířenosti v celkovém riziku pro zařazení do Top 10.
