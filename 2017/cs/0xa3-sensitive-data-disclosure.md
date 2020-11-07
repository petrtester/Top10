# A3:2017 Expozice citlivých dat

| Původci hrozeb/Vektor útoku | Bezpečnostní slabina | Dopady |
| -- | -- | -- |
| Access Lvl : Zneužitelnost 2 | Rozšíření 3 : Zjistitelnost 2 | Technické 3 : Business |
| Místo přímého útoku na šifrovaná data útočníci kradou klíče, provádějí útoky typu man-in-the-middle, nebo kradou čistá textová data mimo server zatímco probíhá přenos, nebo od klienta uživatele, např. prohlížeče. Manuální útok je obecně vyžadován. Dříve načtené databáze hesel mohly být vynuceny jednotkami grafického zpracování (Graphics Processing Units (GPUs)).  | Za posledních několik let se jednalo o nejčastější významný útok. Nejběžnější chybou prostě je, že nejsou citlivá data šifrovaná. Častěji chybí šifrování důvěrných dat, a pokud je k dispozici, často používá nespolehlivé algoritmy, protokoloy, šifry, metody ukládání slabě hashovaných hesel nebo metody pro vytváření a správu klíčů. Též je snadné najít slabiny na straně serveru v případě přenášených dat, zatímco je to těžší v případě dat nepřenášených.| Chyba často ohrožuje data, který by měla být chráněna. Tyto informace typicky zahrnují citlivá osobní data, jako jsou zdravotní záznamy, pověření, osobní údaje, kreditní karty, které často vyžadují ochranu definovanou podle zákonů nebo předpisů, jako je EU GDPR nebo místní zákony o ochraně osobních údajů. |

## Je aplikace zranitelná?

První věcí je určit potřeby ochrany dat, ať jsou či nejsou přenášena. Například hesla, čísla kreditních karet, zdravotní záznamy, osobní údaje a obchodní tajemství vyžadují zvláštní ochranu, zejména pokud tyto údaje spadají pod zákony o ochraně osobních údajů, např. General Data Protection Regulation (GDPR), nebo předpisy, např. finanční ochrana dat jako je PCI Data Security Standard (PCI DSS). Pro všechna taková data:

* Jsou některá data přenášena jako prostý text? To se týká protokolů, jako jsou HTTP, SMTP a FTP. Obzvláště nebezpečný je externí internetový provoz. Ověřte veškerý interní provoz, např. mezi nástroji pro vyrovnávání zatížení, webovými servery nebo systémy back-end.
* Používají se zastaralé nebo slabé kryptografické algoritmy buď ve výchozím nastavení, nebo ve starším kódu?
* Jsou používány výchozí šifrovací klíče, jsou generovány nebo znovu použity slabé šifrovací klíče, nebo chybí dostatečná správa nebo rotace klíčů?
* Není šifrování vynuceno, např. chybí nějaké bezpečnostní směrnice nebo záhlaví uživatelského agenta (prohlížeče)?
* Neověřuje uživatelský agent (např. aplikace, poštovní klient), zda je přijatý certifikát serveru platný?

Navštivte ASVS [Crypto (V7)](https://www.owasp.org/index.php/ASVS_V7_Cryptography), [Data Protection (V9)](https://www.owasp.org/index.php/ASVS_V9_Data_Protection) and [SSL/TLS (V10)](https://www.owasp.org/index.php/ASVS_V10_Communications).

## Jak tomu zabránit

Proveďte přinejmenším následující a prostudujte si odkazy:

* Klasifikujte zpracovaná data, uložená nebo přenášená aplikací. Identifikujte citlivá data podle zákonů o ochraně soukromí, regulačních požadavků nebo obchodních potřeb.
* Použijte ovládací prvky podle klasifikace.
* Neukládejte zbytečně citlivá data. Zničte je co nejdříve, nebo použijte tokenizaci vyhovující PCI DSS nebo použijte zkrácení. Data, která nejsou uchovávána, nemohou být odcizena.
* Zajistěte zašifrování všech citlivých dat, která jsou v klidu. (AT REST)
* Zajistěte, aby byly k dispozivi aktuální a silné standardní algoritmy, protokoly a klíče; používejte správnou správu klíčů.
* Šifrujte všechna přenášená data pomocí zabezpečených protokolů, jako je TLS, s šiframi Perfect Forward Secrecy (PFS), prioritou šifry serverem a zabezpečenými parametry. Vynuťte šifrování pomoví směrnic, jako je HTTP Strict Transport Security (HSTS).
* Zakažte kešování stránek, které obsahují citlivá data.
* Ukládejte hesla pomocí silných adaptivních a hashovacích funkcí s pracovním faktorem (faktor zpoždění), například [Argon2](https://www.cryptolux.org/index.php/Argon2), [scrypt](https://wikipedia.org/wiki/Scrypt), [bcrypt](https://wikipedia.org/wiki/Bcrypt) or [PBKDF2](https://wikipedia.org/wiki/PBKDF2).
* Nezávisle ověřujte efektivnost konfigurace a nastavení.

## Příklady útočných scénářů

**Scénář #1**: Aplikace, která šifruje čísla kreditních karet v databázi, používá automatické šifrování databáze. Tato data se však při načtení automaticky dešifrují, což umožňuje chybě SQL injection načíst čísla kreditních karet ve dormátu prostého textu.

**Scénář #2**: Webové stránky nepoužívají nebo nevynucují TLS pro všechny stránky nebo podporují slaboé šifrování. Útočník monitoruje provoz v síti (např. jako otevřené bezdrátové sítě), degraduje připojení z HTTPS na HTTP, zachycuje požadavky a získává soubory cookie relace uživatele. Útočník potom znovu přehraje tento soubor cookie a unese uživatelkou (autentizovanou) relaci, přistupuje nebo upravuje soukromá data uživatele. Místo výše zmiňovaného mohli změnit všechna přenášená data, např. příjemce převodu peněz.

**Scénář #3**: Databáze hesel používá pro ukládání všech hesel nesolené nebo jednoduché hashe. Chyba při nahrávání souboru umožňuje útočníkovi získat databázi hesel. Všechny nesolené  hashe mohou být odkryty pomocí tzv. duhové tabulky předpočítaných hashů. Hashe generované jednoduchými nebo rychlými hashovacími funkcemi mohou být prolomeny GPU, ikdyž byly solené.

## Odkazy

* [OWASP Proactive Controls: Protect Data](https://www.owasp.org/index.php/OWASP_Proactive_Controls#7:_Protect_Data)
* [OWASP Application Security Verification Standard]((https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project)): [V7](https://www.owasp.org/index.php/ASVS_V7_Cryptography), [9](https://www.owasp.org/index.php/ASVS_V9_Data_Protection), [10](https://www.owasp.org/index.php/ASVS_V10_Communications)
* [OWASP Cheat Sheet: Transport Layer Protection](https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet)
* [OWASP Cheat Sheet: User Privacy Protection](https://www.owasp.org/index.php/User_Privacy_Protection_Cheat_Sheet)
* [OWASP Cheat Sheet: Password](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet) and [Cryptographic Storage](https://www.owasp.org/index.php/Cryptographic_Storage_Cheat_Sheet)
* [OWASP Security Headers Project](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project); [Cheat Sheet: HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)
* [OWASP Testing Guide: Testing for weak cryptography](https://www.owasp.org/index.php/Testing_for_weak_Cryptography)

### Externí

* [CWE-220: Exposure of sens. information through data queries](https://cwe.mitre.org/data/definitions/220.html)
* [CWE-310: Cryptographic Issues](https://cwe.mitre.org/data/definitions/310.html); [CWE-311: Missing Encryption](https://cwe.mitre.org/data/definitions/311.html)
* [CWE-312: Cleartext Storage of Sensitive Information](https://cwe.mitre.org/data/definitions/312.html)
* [CWE-319: Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html)
* [CWE-326: Weak Encryption](https://cwe.mitre.org/data/definitions/326.html); [CWE-327: Broken/Risky Crypto](https://cwe.mitre.org/data/definitions/327.html)
* [CWE-359: Exposure of Private Information - Privacy Violation](https://cwe.mitre.org/data/definitions/359.html)
