# A8:2017 Nezabezpečená deserializace

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 1 | Rozšíření 2 : Zjistitelnost 2 | Technické 3 : Obchodní |
| Zneužití neošetřené deserializace je poněkud obtížné, protože běžné prvoplánové pokusy zřídka fungují beze změny podkladového zdrojového kódu. | Tento problém je zahrnut v Top 10 na základě [průzkumu odvětví](https://owasp.blogspot.com/2017/08/owasp-top-10-2017-project-update.html), nikoli na kvantifikovatelných datech. Některé nástroje mohou objevit nedostatky deserializace, ale k ověření problému je často nutná lidská pomoc. Očekává se, že údaje o rozšíření zneužití nedostatků deserializace se budou hromadit s vývojem nástrojů, které by je pomohly identifikovat a řešit. | Dopad deserializačních chyb nelze podceňovat. Tyto chyby mohou vést například ke vzdálenému spuštění kódu, což je jeden z nejzávažnějších možných útoků. Obchodní dopady závisí na potřebách ochrany aplikace a dat. |

## Je aplikace zranitelná?

Aplikace a aplikační rozhraní (API) budou zranitelné, pokud deserializují pozměněné objekty podstrčené útočníkem.

To může mít za následek dva primární typy útoků:

* Útoky související s objektovou a datovou strukturou, kdy útočník upraví logiku aplikace nebo dosahne spuštění kódu na vzdáleném stroji (pokud má aplikace k dispozici třídy, které mohou změnit chování během deserializace nebo po ní).
* Typické útoky manipulující daty, jako jsou útoky související s řízením přístupu, kde se používají existující datové struktury, ale mění se jejich obsah.

Serializaci lze použít v aplikacích pro:

* Vzdálenou a meziprocesovou komunikaci (RPC / IPC)
* Drátové protokoly, webové služby, zprostředkovatele zpráv
* Mezipaměť / trvalé uložiště
* Databáze, cache servery, souborové systémy
* HTTP cookies, parametry formuláře HTML, autentizační tokeny API

## Jak se mohu bránit?

Jediným bezpečným architektonickým vzorem je nepřijímat serializované objekty z nedůvěryhodných zdrojů nebo používat média pro serializaci, která povolují pouze primitivní datové typy.

Pokud to není možné, zvažte jednu z následujících možností:

* Implementace kontrol integrity, jako jsou digitální podpisy na všech serializovaných objektech, aby se zabránilo vytváření škodlivých objektů nebo nedovolené manipulaci s daty.
* Zavedení přísné typové kontroly během deserializace před vytvořením objektu, protože kód obvykle očekává definovatelnou sadu tříd. Obcházení této techniky byly prokázány, takže spoléhání se pouze na ni se nedoporučuje.
* Izolace a spuštění kódu, který deserializuje v prostředích s nízkými oprávněními, pokud je to možné.
* Logování deserializačních výjimek a selhání. Například když příchozí typ není očekávaným typem, nebo deserializace vyvolá výjimku.
* Omezení nebo monitorování příchozího a odchozího připojení k síti z kontejnerů nebo serverů, které deserializují.
* Monitorování deserializace a upozornění, pokud uživatel deserializuje neustále.

## Příklady útočných scénářů

**Scénář č. 1**: Aplikace napsaná v Reactu volá sadu Spring Boot mikroslužeb. Programátoři se snažili zajistit, aby jejich kód byl neměnný. Řešení, které zvolili, je serializace stavu uživatele a jeho předávání tam a zpět s každým požadavkem. Útočník si všimne podpisu objektu Java „R00“ a pomocí nástroje Java Serial Killer dosáhne vzdáleného spuštění kódu na aplikačním serveru.

**Scénář č. 2**: Fórum napsané v PHP používá serializaci objektů PHP k uložení „super“ cookie, které obsahuje ID uživatele, roli, hash hesla a další stav:

`a:4:{i:0;i:132;i:1;s:7:"Bob";i:2;s:4:"user";i:3;s:32:"b6a8b3bea87fe0e05022f8f3c88bc960";}`

Útočník změní serializovaný objekt tak, že sám dostává oprávnění správce:
`a:4:{i:0;i:1;i:1;s:5:"Alice";i:2;s:5:"admin";i:3;s:32:"b6a8b3bea87fe0e05022f8f3c88bc960";}`

## Odkazy

### OWASP

* [OWASP Cheat Sheet: Deserialization](https://www.owasp.org/index.php/Deserialization_Cheat_Sheet)
* [OWASP Proactive Controls: Validate All Inputs](https://www.owasp.org/index.php/OWASP_Proactive_Controls#4:_Validate_All_Inputs)
* [OWASP Application Security Verification Standard: TBA](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP AppSecEU 2016: Surviving the Java Deserialization Apocalypse](https://speakerdeck.com/pwntester/surviving-the-java-deserialization-apocalypse)
* [OWASP AppSecUSA 2017: Friday the 13th JSON Attacks](https://speakerdeck.com/pwntester/friday-the-13th-json-attacks)

### Externí

* [CWE-502: Deserialization of Untrusted Data](https://cwe.mitre.org/data/definitions/502.html)
* [Java Unmarshaller Security](https://github.com/mbechler/marshalsec)
* [OWASP AppSec Cali 2015: Marshalling Pickles](http://frohoff.github.io/appseccali-marshalling-pickles/)
