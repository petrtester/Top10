# A5:2017 Nefunkční řízení přístupu

| Původci hrozby/Vektor útoku | Bezpečnostní slabina  | Dopady |
| -- | -- | -- |
| Access Lvl : Zneužitelnost 2 | Rozšíření 2 : Zjistitelnost 2 | Technické 3 : Business |
| Zneužití kontroly přístupu je základní dovednostní útočníků [SAST](https://www.owasp.org/index.php/Source_Code_Analysis_Tools) a [DAST](https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools) nástroje mohou detekovat absenci kontroly přístupu, ale nemohou ověřit, zda je funkční, když je přítomna. Řízení přístupu je detekovatelné s využitím ručních prostředků, nebo případně automatizací pro absenci kontroly přístupu v určitých frameworcích. | Slabiny řízení přístupu jsou běžné kvůli nedostatku automatické detekce a nedostatku efektivního testování vývojaři aplikací. Detekce řízení přístupu není obvykle přístupná automatizovanému statickému nebo dynamickému testování. Manuální testování je nejlepším způsobem pro detekci nebo neefektivní kontrolu přístupu, včetně HTTP metod (GET vs PUT, atd.), controllerů, přímých odkazů na objekty, atd. | Technickým dopadem jsou útočníci vystupující jako uživatelé nebo administrátoři, nebo uživatelé využívající privilegované funkce, nebo vytvářející, přistupující nebo aktualizující či mazající každý záznam. Dopad podnikání závisí na potřebách ochrany aplikace a dat.|

## Je aplikace zranitelná?

Řízení přístupu vynucuje zásady tak, aby uživatelé nemohli jednat mimo jejich zamýšlená oprávnění. Poruchy obvykle vedou k neoprávněnému vyzrazení informací, modifikaci nebo zničení všech dat nebo k provedení obchodní funkce mimo limity uživatele. Mezi běžné chyby zabezpečení patří:

* Vynechání kontrol řízení přístupu změnou adresy URL, stavu interní aplikace nebo stránky HTML nebo jednoduše pomocí vlastního nástroje útoku API.
* Umožnění změny primárního klíče na záznam uživatele jiného uživatele, povolení prohlížení nebo úpravy účtu někoho jiného.
* Povýšení privilegia. Vystupovat jako uživatel bez přihlášení, nebo jako administrátor, když jste přihlášeni jako uživatel.
* Manipulace s metadaty, jako je přehrávání nebo manipulace s tokenem řízení přístupu JSON Web Token (JWT) nebo cookie nebo skryté pole manipulované za účelem zvýšení oprávnění nebo zneužití zneplatnění JWT.
* Chybná konfigurace CORS umožňuje neoprávněný přístup API.
* Vynutit procházení na ověřené stránky jako neověřený uživatel nebo na privilegované stránky jako standardní uživatel. Přístup k API s chybějícími ovládacími prvky pro POST, PUT a DELETE.

## Jak tomu zabránit

Řízení přístupu je účinné pouze v případě, že je vynuceno v důvěryhodném kódu na straně serveru nebo API bez serveru, kde útočník nemůže upravit kontrolu přístupu nebo metadata.

* S výjimkou veřejných zdrojů ve výchozím nastavení zakázat.
* Implementujte mechanismy řízení přístupu jednou a znovu je používejte v celé aplikaci, včetně minimalizace využití CORS.
* Modelové řízení přístupu by mělo vynucovat vlastnictví záznamu, nikoli přijímat, že uživatel může vytvořit, číst, aktualizovat nebo odstranit jakýkoli záznam.
* Unikátní požadavky na obchodní limity aplikací by měly být vynucovány doménovými modely.
* Zakažte výpis adresářů webového serveru a zajistěte, aby se ve webových kořenech nenacházely metadata souborů (např. .git) a záložní soubory.
* Zaznamenejte selhání řízení přístupu, upozorněte administrátory, když je to vhodné (např. opakovaná selhání).
* Ohodnoťte limit API a kontroleru přístupu, abyste minimalizovali škody způsobené nástroji automatizovaného útoku.
* Tokeny JWT by měly být na serveru po odhlášení zneplatněny.
* Vývojáři a zaměstnanci QA by měli zahrnovat funkční jednotku kontroly přístupu a integrační testy.

## Příklady útočných scénářů

**Scenario #1**: Aplikace používá neověřená data při volání SQL, které přistupuje k informacím o účtu.

```
  pstmt.setString(1, request.getParameter("acct"));
  ResultSet results = pstmt.executeQuery();
```

Útočník jednoduše modifikuje parametr "acct" v prohlížeči tak, aby odeslal jakékoliv číslo účtu, které chce. Pokud není správně ověřen, může útočník získat přístup k účtu libovolného uživatele.

`http://example.com/app/accountInfo?acct=notmyacct`

**Scenario #2**: Útočník jednoduše vynutí procházení k cílovým URL adresám. Adminova práva jsou požadována pro přístup do adminovy stránky.

```
  http://example.com/app/getappInfo
  http://example.com/app/admin_getappInfo
```

Pokud má neautentizovaný uživatel přístup na kteroukoliv stránku, jedná se o chybu. Pokud má neadministrátor přístup do stránek admina, jedná se o chybu.

## Odkazy

### OWASP

* [OWASP Proactive Controls: Access Controls](https://www.owasp.org/index.php/OWASP_Proactive_Controls#6:_Implement_Access_Controls)
* [OWASP Application Security Verification Standard: V4 Access Control](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Testing Guide: Authorization Testing](https://www.owasp.org/index.php/Testing_for_Authorization)
* [OWASP Cheat Sheet: Access Control](https://www.owasp.org/index.php/Access_Control_Cheat_Sheet)

### Externí

* [CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')](https://cwe.mitre.org/data/definitions/22.html)
* [CWE-284: Improper Access Control (Authorization)](https://cwe.mitre.org/data/definitions/284.html)
* [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)
* [CWE-639: Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)
* [PortSwigger: Exploiting CORS misconfiguration](https://portswigger.net/blog/exploiting-cors-misconfigurations-for-bitcoins-and-bounties)
