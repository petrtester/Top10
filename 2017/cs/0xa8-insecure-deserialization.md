# A8:2017 Nezabezpečená deserializace

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 1 | Rozšíření 2 : Zjistitelnost 2 | Technické 3 : Obchodní |
| Zneužití neošetřené deserializace je poněkud obtížné, protože běžné prvoplánové pokusy zřídka fungují beze změny podkladového zdrojového kódu. | Tento problém je zahrnut v Top 10 na základě [průzkumu odvětví](https://owasp.blogspot.com/2017/08/owasp-top-10-2017-project-update.html), nikoli na kvantifikovatelných datech. Některé nástroje mohou objevit nedostatky deserializace, ale k ověření problému je často nutná lidská pomoc. Očekává se, že údaje o rozšíření zneužití nedostatků deserializace se budou hromadit s vývojem nástrojů, které by je pomohly identifikovat a řešit. | Dopad deserializačních chyb nelze podceňovat. Tyto chyby mohou vést například ke vzdálenému spuštění kódu, což je jeden z nejzávažnějších možných útoků. Obchodní dopady závisí na potřebách ochrany aplikace a dat. |

## Je aplikace zranitelná?

Applications and APIs will be vulnerable if they deserialize hostile or tampered objects supplied by an attacker.

This can result in two primary types of attacks:

* Object and data structure related attacks where the attacker modifies application logic or achieves arbitrary remote code execution if there are classes available to the application that can change behavior during or after deserialization.
* Typical data tampering attacks such as access-control-related attacks where existing data structures are used but the content is changed.

Serialization may be used in applications for:

* Remote- and inter-process communication (RPC/IPC) 
* Wire protocols, web services, message brokers
* Caching/Persistence
* Databases, cache servers, file systems 
* HTTP cookies, HTML form parameters, API authentication tokens 

## Jak se mohu bránit?

The only safe architectural pattern is not to accept serialized objects from untrusted sources or to use serialization mediums that only permit primitive data types.

If that is not possible, consider one of more of the following:

* Implementing integrity checks such as digital signatures on any serialized objects to prevent hostile object creation or data tampering.
* Enforcing strict type constraints during deserialization before object creation as the code typically expects a definable set of classes. Bypasses to this technique have been demonstrated, so reliance solely on this is not advisable.
* Isolating and running code that deserializes in low privilege environments when possible.
* Log deserialization exceptions and failures, such as where the incoming type is not the expected type, or the deserialization throws exceptions.
* Restricting or monitoring incoming and outgoing network connectivity from containers or servers that deserialize.
* Monitoring deserialization, alerting if a user deserializes constantly.


## Příklady útočných scénářů

**Scenario #1**: Aplikace napsaná v Reactu volá sadu Spring Boot mikroslužeb. Programátoři se snažili zajistit, aby jejich kód byl neměnný. Řešení, které zvolili, je serializace stavu uživatele a jeho předávání tam a zpět s každým požadavkem. Útočník si všimne podpisu objektu Java „R00“ a pomocí nástroje Java Serial Killer dosáhne vzdáleného spuštění kódu na aplikačním serveru.

**Scenario #2**: Fórum napsané v PHP používá serializaci objektů PHP k uložení „super“ cookie, které obsahuje ID uživatele, roli, hash hesla a další stav:

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
