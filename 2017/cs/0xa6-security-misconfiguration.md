# A6:2017 Chybná konfigurace zabezpečení

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 3 | Rozšíření 3 : Zjistitelnost 3 | Technické 2 : Obchodní |
| Útočníci se často pokusí zneužít neopravené chyby nebo získat přístup k výchozím účtům, nepoužívaným stránkám, nechráněným souborům a adresářům atd., aby získali neoprávněný přístup nebo znalosti systému. | K chybné konfiguraci zabezpečení může dojít na jakékoli úrovni, včetně síťových služeb, platformy, webového serveru, aplikačního serveru, databáze, rozhraní, vlastního kódu a předinstalovaných virtuálních strojů, kontejnerů nebo úložišť. Automatické skenery jsou užitečné pro zjišťování chybných konfigurací, použití výchozích účtů nebo konfigurací, zbytečných služeb, starších možností atd. | Takové chyby často útočníkům umožňují neoprávněný přístup k některým systémovým datům nebo funkcím. Občas takové chyby vedou k úplnému zkompromitování systému. Obchodní dopad závisí na potřebách ochrany aplikace a dat. |

## Je aplikace zranitelná?

Aplikace může být zranitelná pokud:

* Chybí vhodné posílení zabezpečení v jakémkoliv SW vybavení, které aplikace používá, nebo jsou nesprávně nakonfigurovaná oprávnění pro cloudové služby.
* Jsou povoleny nebo nainstalovány nepotřebné funkce (např.: nepotřebné porty, služby, stránky, účty nebo oprávnění).
* Výchozí účty a jejich hesla jsou stále povolena a nezměněna.
* Informace o zpracování chyb nebo jiné příliš informativní chybové zprávy jsou přístupné uživatelům.
* U upgradovaných systémů jsou nejnovější funkce zabezpečení deaktivovány nebo nejsou bezpečně nakonfigurovány.
* Nastavení zabezpečení v aplikačních serverech, aplikačních rámcích (např. Struts, Spring, ASP.NET), knihovnách, databázích atd. není nastaveno na bezpečné hodnoty.
* Server neodesílá bezpečnostní hlavičky ani směrnice nebo není nastaven na bezpečné hodnoty.
* Software je zastaralý nebo zranitelný (viz **A9: 2017 – Používání komponent se známými bezpečnostními chybami**).

Bez koordinovaného a opakovatelného procesu konfigurace zabezpečení aplikace jsou systémy vystaveny vyššímu riziku.

## Jak se mohu bránit?

Měly by být implementovány procesy zabezpečené instalace, včetně následujících bodů:

* Opakovatelný proces, který umožňuje rychlé a snadné nasazení jiného prostředí, které je správně uzamčeno. Vývojová, testovací (QA) a produkční prostředí by měla být všechna nakonfigurována identicky s různými pověřeními používanými v každém prostředí. Tento proces by měl být automatizován, aby se minimalizovalo úsilí potřebné k nastavení nového zabezpečeného prostředí.
* Minimalistická platforma bez zbytečných funkcí, komponent, dokumentace a vzorků. Odeberte nebo neinstalujte nepoužívané funkce a aplikační rámce.
* Úkol zkontrolovat a aktualizovat konfigurace odpovídající všem bezpečnostním poučkám, aktualizacím a opravám jako součást procesu správy oprav (viz **A9: 2017 - Používání komponent se známými bezpečnostními chybami**). Zkontrolujte zejména oprávnění cloudového úložiště (např.: oprávnění S3 Buckets).
* Segmentovaná aplikační architektura, která poskytuje efektivní a bezpečné oddělení komponent, a to se segmentací, kontejnerizací nebo cloudovými bezpečnostními skupinami (Access Control List – ACL).
* Odesílání bezpečnostních směrnic klientské straně, např.: [bezpečnostní hlavičky](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project).
* Automatizovaný proces ověřující efektivitu konfigurací a nastavení ve všech prostředích.

## Příklady útočných scénářů

**Scénář č. 1**: Aplikační server je dodáván s ukázkovými aplikacemi, které nejsou odebrány z produkčního serveru. Tyto ukázkové aplikace mají známé bezpečnostní chyby, které útočníci používají ke kompromitaci serveru. Pokud je jednou z těchto aplikací správcovská konzole a výchozí účty nebyly změněny, útočník se přihlásí pomocí výchozích hesel a převezme kontrolu.

**Scénář č. 2**: Zobrazení seznamu adresářů není na serveru zakázáno. Útočník zjistí, že může jednoduše vypsat dostupné adresáře. Útočník najde a stáhne zkompilované třídy Java, které dekompiluje a zobrazení si kód pomocí reverzního inženýrství. Útočník poté v aplikaci najde závažnou chybu v řízení přístupu.

**Scénář č. 3**: Konfigurace aplikačního serveru umožňuje vypisování podrobných chybových zpráv uživatelům, např.: kroky zásobníku. To potenciálně odhaluje citlivé informace nebo podkladové chyby, jako jsou verze knihoven, u nichž je známa jejich zranitelnost.

**Scénář č. 4**: Poskytovatel cloudových služeb má výchozí oprávnění ke sdílení otevřená všem uživatelům internetu. To umožňuje přístup k citlivým datům uloženým v cloudovém úložišti.

## Odkazy

### OWASP

* [OWASP Testing Guide: Configuration Management](https://www.owasp.org/index.php/Testing_for_configuration_management)
* [OWASP Testing Guide: Testing for Error Codes](https://www.owasp.org/index.php/Testing_for_Error_Code_(OWASP-IG-006))
* [OWASP Security Headers Project](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project)

For additional requirements in this area, see the Application Security Verification Standard [V19 Configuration](https://www.owasp.org/index.php/ASVS_V19_Configuration).

### Externí

* [NIST Guide to General Server Hardening](https://csrc.nist.gov/publications/detail/sp/800-123/final)
* [CWE-2: Environmental Security Flaws](https://cwe.mitre.org/data/definitions/2.html)
* [CWE-16: Configuration](https://cwe.mitre.org/data/definitions/16.html)
* [CWE-388: Error Handling](https://cwe.mitre.org/data/definitions/388.html)
* [CIS Security Configuration Guides/Benchmarks](https://www.cisecurity.org/cis-benchmarks/)
* [Amazon S3 Bucket Discovery and Enumeration](https://blog.websecurify.com/2017/10/aws-s3-bucket-discovery.html)
