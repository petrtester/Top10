# +O Organizace, co dál?

## Spusťte ihned program zabezpečení aplikací

Zabezpečení aplikací již není pouze volbou. Mezi rostoucími útoky a regulačními vyhláškami musí organizace zavést efektivní procesy a metody, které vedou ke zvýšení zabezpečení jejich aplikací a aplikačních rozhraní (API). Vzhledem k ohromujícímu množství kódu v mnoha aplikacích a aplikačních rozhraních, které jsou již v produkci, mnoho organizací zápasí se zvládnutím enormního množství chyb zabezpečení.

OWASP doporučuje organizacím zavést program zabezpečení aplikací, aby získaly přehled a zlepšily zabezpečení svých aplikací a API. Dosažení efektivního zabezpečení aplikací vyžaduje spolupráci mnoha různých částí organizace, včetně bezpečnostního a auditního sektoru, vývoje softwaru, obchodu a managementu. Zabezpečení by mělo být viditelné a měřitelné, aby jednotlivé zainteresované strany mohly vidět a porozumět pozici zabezpečení aplikace v organizaci. Zaměřte se na činnosti a výsledky, které ve skutečnosti pomáhají zlepšit zabezpečení podniku odstraněním nebo snížením rizika. [OWASP SAMM](https://www.owasp.org/index.php/OWASP_SAMM_Project) a [OWASP Application Security Guide for CISOs](https://www.owasp.org/index.php/Application_Security_Guide_For_CISOs) jsou zdroje většiny klíčových činností v tomto seznamu.

### Začněte

* Dokumentujte všechny aplikace a související datová aktiva. Větší organizace by za tímto účelem měly zvážit implementaci databáze pro správu konfigurace (Configuration Management Database – CMDB).
* Vytvořte [program zabezpečení aplikace](https://www.owasp.org/index.php/SAMM_-_Strategy_&_Metrics_-_1) a osvojte si ho.
* Proveďte [analýzu nedostatku schopností](https://www.owasp.org/index.php/SAMM_-_Strategy_&_Metrics_-_3) porovnáním vaší organizace s vašimi kolegy a definováním klíčových oblastí pro vylepšení a prováděcího plánu.
* Získejte souhlas vedení a vytvořte [kampaň na zvýšení povědomí o bezpečnosti aplikací](https://www.owasp.org/index.php/SAMM_-_Education_&_Guidance_-_1) pro celou IT organizaci.

### Přístup k portfoliu založený na riziku

* Určete [potřeby ochrany](https://www.owasp.org/index.php/SAMM_-_Strategy_&_Metrics_-_2) svého [portfolia aplikací](https://www.owasp.org/index.php/SAMM_-_Strategy_&_Metrics_-_2) z obchodního hlediska. Toto by mělo být částečně řízeno zákony na ochranu osobních údajů a dalšími předpisy souvisejícími s ochranou dat.
* Vytvořte společný [model hodnocení rizika](https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology) s konzistentní sadou pravděpodobnosti a dopadových faktorů odrážejících toleranci vaší organizace vůči riziku.
* Podle toho změřte a uspořádejte dle priority všechny své aplikace a API. Přidejte výsledky do své CMDB.
* Stanovte postupy pro zajištění správného definování pokrytí a požadované úrovně závažnosti.

### Poskytněte možnosti s pevnými základy

* Vytvořte soubor cílených [zásad a standardů](https://www.owasp.org/index.php/SAMM_-_Policy_&_Compliance_-_2), které poskytnou základní úroveň zabezpečení aplikace pro všechny vývojové týmy.
* Definujte společnou sadu [opakovaně použitelných ovládacích prvků zabezpečení](https://www.owasp.org/index.php/OWASP_Security_Knowledge_Framework), která doplní tyto zásady a standardy a poskytne pokyny k jejich začlenění v rámci návrhu a vývoje.
* Vytvořte [osnovy školení v oblasti bezpečnosti aplikací](https://www.owasp.org/index.php/SAMM_-_Education_&_Guidance_-_2), které budou povinné a zaměřené na různé vývojové role a témata.

### Začleňte zabezpečení do stávajících procesů

* Definujte a integrujte [bezpečnou implementaci](https://www.owasp.org/index.php/SAMM_-_Construction) a [ověřovací aktivity](https://www.owasp.org/index.php/SAMM_-_Verification) do stávajících vývojových a provozních procesů.
* Aktivity zahrnují [modelování hrozeb](https://www.owasp.org/index.php/SAMM_-_Threat_Assessment_-_1), zabezpečený [design a recenze designu](https://www.owasp.org/index.php/SAMM_-_Design_Review_-_1), zabezpečené kódování a [kontrola kódu](https://www.owasp.org/index.php/SAMM_-_Code_Review_-_1), [penetrační testování](https://www.owasp.org/index.php/SAMM_-_Security_Testing_-_1) a nápravu.
* Zajistěte si odborníky na konkrétní problematiku a [podpůrné služby pro vývojové a projektové týmy](https://www.owasp.org/index.php/SAMM_-_Education_&_Guidance_-_3), abyste byli úspěšní.

### Zajistěte viditelnou správu

* Řiďte s podporou metrik. Podpořte rozhodování o zlepšování a financování na základě zachycených metrik a analytických dat. Mezi metriky patří dodržování bezpečnostních postupů a činností, seznámení se se zranitelnostmi, snížení zranitelnosti, pokrytí aplikací, hustota závad podle typu a počtu instancí atd.
* Analyzujte data z implementačních a verifikačních činností, abyste zjistili, jaké jsou hlavní příčiny a vzorce zranitelnosti, a abyste mohli řídit strategická a systémová vylepšení v celém podniku. Poučte se z chyb a podporujte přicházející návrhy na vylepšení.
