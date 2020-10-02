# A10:2017 Nedostatečné logování a monitorování

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 2 | Rozšíření 3 : Zjistitelnost 1 | Technické 2 : Obchodní |
| Nedostatečné logování a monitorování je základem téměř každé závažné události. Útočníci se spoléhají na nedostatečné monitorování a zanedbanou včasnou reakci při dosahování svých cílů, aniž by byli odhaleni. | Toto číslo je zahrnuto v Top 10 na základě [průzkumu odvětví](https://owasp.blogspot.com/2017/08/owasp-top-10-2017-project-update.html). Jednou ze strategií pro určení, zda máte dostatečné monitorování, je prozkoumání logů po penetračním testování. Činnosti testerů by měly být dostatečně zaznamenány, aby bylo zřejmé, jaké škody mohou být způsobeny. | Nejúspěšnější útoky začínají zkoumáním zranitelnosti. Umožnění pokračování těchto sond může zvýšit pravděpodobnost úspěšného zneužití na téměř 100 %. V roce 2016 trvalo zjištění narušení zabezpečení [průměrně 191 dní](https://www-01.ibm.com/common/ssi/cgi-bin/ssialias?htmlfid=SEL03130WWEN&) – spousta času na způsobení škody. |

## Je aplikace zranitelná?

K nedostatečnému logování, detekci, monitorování a aktivní odezvě dochází kdykoli když:

* Nejsou zaznamenávány auditovatelné události, jako jsou přihlášení, neúspěšná přihlášení a důležité transakce.
* Varování a chyby generují neadekvátní nebo nejasné zprávy v logu nebo nejsou logovány vůbec.
* Protokoly aplikací a API nejsou sledovány kvůli podezřelé aktivitě.
* Protokoly se ukládají pouze lokálně.
* Nejsou nastaveny vhodné prahové hodnoty a procesy eskalace odezvy nejsou zavedeny, nebo jsou neúčinné.
* Penetrační testování a skenování nástroji [DAST](https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools) (například [OWASP ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)) nespouští upozornění.
* Aplikace není schopna detekovat nebo upozorňovat na aktivní útoky v reálném čase nebo s mírným spožděním a případně předávat k dodatečným konktrolám.

Vůči úniku informací jste zranitelní, pokud nezabezpečíte logy a upozornění před uživateli nebo útočníky (viz A3: Expozice citlivých informací 2017).

## Jak se mohu bránit?

Podle rizika dat uložených nebo zpracovaných aplikací:

* Zajistěte, aby všechna přihlášení, selhání řízení přístupu a selhání ověření vstupu na straně serveru mohla být zaznamenávána s dostatečným uživatelským kontextem pro identifikaci podezřelých nebo škodlivých účtů a archivována po dostatečně dlouhou dobu, aby bylo možné provést zpětnou forenzní analýzu.
* Zajistěte, aby se logy generovaly ve formátu, který lze snadno zpracovat centralizovanými řešeními pro správu logů.
* Zajistěte, aby důležité transakce procházely integritním auditem, aby se zabránilo neoprávněné manipulaci nebo odstranění. Lze použít například databázové tabulky které umožňují pouze vložení nových záznamů.
* Zaveďte účinné monitorování s výstrahami tak, aby byly podezřelé aktivity detekovány a existovala možnost na ně včas reagovat.
* Vytvořte nebo převezměte plán reakce a obnovy po nastalém incidentu, například [NIST 800-61 rev 2](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final) nebo novější.

Existují komerční a open-source řešení pro ochranu aplikací, jako je [OWASP AppSensor](https://www.owasp.org/index.php/OWASP_AppSensor_Project), firewall webových aplikací, jako je [ModSecurity s OWASP ModSecurity Core Rule Set](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) a software pro kumulaci logů s možností vizualizace statistik a nastavením upozornění.

## Příklady útočných scénářů

**Scénář č. 1**: Open-source software pro tvorbu veřejného fóra provozovaný malým týmem byl napaden pomocí chyby v tomto software. Útočníkům se podařilo vymazat interní úložiště zdrojového kódu obsahující další verzi a veškerý obsah fóra. Přestože bylo možné zdroj obnovit, nedostatečné monitorování, absence logů nebo upozornění vedly k mnohem horšímu konci. Projekt již není v důsledku tohoto problému aktivní.

**Scénář č. 2**: Útočník vyhledává uživatele používající běžné heslo. V průběhu času může útočník vyhledat všechny uživatele používající takové heslo. U všech ostatních uživatelů nastane během tohoto pokusu o odhalení hesla pouze jedno nezdařilé přihlášení. Po několika dnech může být útok opakován s jiným heslem.

**Scénář č. 3**: Přední americký prodejce měl údajně interní sandbox pro analýzu malwaru, který analyzoval přílohy. Softwarový sandbox detekoval potenciálně nežádoucí software, ale na tuto detekci nikdo nereagoval. Nástroj už nějakou dobu emitoval upozornění, než bylo prolomení ochrany zjištěno kvůli podvodným transakcím s kartami externí bankou.

## Odkazy

### OWASP

* [OWASP Proactive Controls: Implement Logging and Intrusion Detection](https://www.owasp.org/index.php/OWASP_Proactive_Controls#8:_Implement_Logging_and_Intrusion_Detection)
* [OWASP Application Security Verification Standard: V8 Logging and Monitoring](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Testing Guide: Testing for Detailed Error Code](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Cheat Sheet: Logging](https://www.owasp.org/index.php/Logging_Cheat_Sheet)

### Externí

* [CWE-223: Omission of Security-relevant Information](https://cwe.mitre.org/data/definitions/223.html)
* [CWE-778: Insufficient Logging](https://cwe.mitre.org/data/definitions/778.html)
