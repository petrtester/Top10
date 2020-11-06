# A2:2017 Chybná autentizace

| Původci hrozeb/Vektor útoku | Bezpečnostní slabina         | Dopady               |
| -- | -- | -- |
| Access Lvl : Zneužitelnost 3 | Prevalence 2 : Zjistitelnost 2 | Technické 3 : Business |
| Útočníci mají přístup ke stovkám miliónů platných kombinací uživatelských jmen a hesel pro "credential stuffing", výchozí seznamy účtů pro správu, automatizovanou hrubou sílu a slovníkové útočné nástroje. Útoky na správu relací jsou dobře pochopeny, zejména ve vztahu k nevypršeným tokenům relací. | Prevalence chybné autentizace je rozšířená díky návrhu a implementaci většiny kontrol identity a přístupu. Správa relací je základem autentizace a řízení přístupu a je přítomna ve všech stavových aplikacíh. Útočníci mohou detekovat chybnou autentizaci s použitím ručních prostředků a zneužít je pomocí automatických nástrojů se seznamy hesel a slovníkovými útoky. | Útočníci musí získat přístup pouze k několika málo účtům, nebo pouze k jednomu účtu správce (admin účtu), aby narušili bezpečnost systému. V závislosti na doméně aplikace to může umožnit praní špinavých peněz, podvody se sociálním zabezpečením, krádež identity nebo zveřejnit legálně chráněné vysoce citlivé informace. |

## Je aplikace zranitelná?

Potvrzení identity uživatele, autentizace a správa relace jsou zásadní pro ochranu před útoky, které souvisí s autentizací.

Mohou existovat slabiny autentizace, pokud aplikace:

* Povoluje automatizované útoky, jako je "credential stuffing" [credential stuffing](https://www.owasp.org/index.php/Credential_stuffing), kde má útočník seznam platných uživatelských jmen a hesel.
* Povoluje hrubou sílu nebo jiné automatizované útoky.
* Povoluje výchozí, slabá nebo dobře známá hesla, např. "Heslo1" nebo "admin/admin".
* Používá slabé nebo neúčinné procesy pro obnovení pověření nebo pro zapomenuté heslo, např. "odpovědi založené na znalostech", které nelze zajistit.
* Používá prostý text, šifrovaná nebo slabě hashovaná hesla (see **A3:2017-Sensitive Data Exposure**).
* Má chybějící nebo neúčinné vícefaktorové ověřování.
* Odhaluje ID relací v URL (např. přepis URL).
* Nemění ID relcí po úspěšném přihlášení.
* Nesprávně zneplatňuje ID relace. Uživatelské relace nebo autentizační tokeny (zejména tokeny jednotného přihlášení (SSO)) nejsou během odhlašování nebo období nečinnosti správně zneplatněny.

## Jak tomu zabránit

* Pokud je to možné, implementujte vícefaktorové ověřování, abyste zabránili automatizovaným útokům, "credential stuffing", hrubé síle a odcizení opětovného použití pověření. 
* Neposílejte ani nenasazujte žádné výchozí přihlašovací údaje, zejména pro uživatele v roli admin/správce.
* Implementuje kontroly slabých hesel, například testování nových nebo změněných hesel proti seznamu 10000 nejhorších hesel [top 10000 worst passwords](https://github.com/danielmiessler/SecLists/tree/master/Passwords).
* Slaďte délku hesel, složitosti a frekvence změny hesel s [NIST 800-63 B's guidelines in section 5.1.1 for Memorized Secrets](https://pages.nist.gov/800-63-3/sp800-63b.html#memsecret) nebo jinými moderními zásadami hesel založenými na důkazech.
* Zajistěte, aby registrace, obnovení pověření a cesty API obrněny proti útokům na výčet účtů s použitím stejných zpráv pro všechny výstupy.
* Omezte nebo stále více odkládejte neúspěšné pokusy o přihlášení. Zaznamenávejte všechna selhání a upozorněte administrátory, když jsou detekovány údaje o "credential stuffing", hrubá síla či jiné útoky.
* Využijte zabezpečeného integrovaného správce relací na straně serveru, který po přihlášení vygeneruje nové náhodné ID relace s vysokou entropií. ID relace by neměla být v adrese URL, měla by být bezpečně uložena a zneplatněna po odhlášení, nečinnosti a absolutních časových limitech.

## Příklady útočných scénářů

Scénář #1: [Credential stuffing](https://www.owasp.org/index.php/Credential_stuffing), použití [lists of known passwords](https://github.com/danielmiessler/SecLists), je běžným utékem. Pokud v aplikaci není implementována automatická ochrana před hrozbami nebo "credential stuffing", může být použita jako věštec hesla k určení, zda jsou pověření platná.

**Scénář #2**: K většině útoků na autentizaci dochází v důsledku dalšího používání hesel jako jediného faktoru.    !!!Once considered best practices, password rotation and complexity requirements are viewed as encouraging users to use, and reuse, weak passwords. Organizations are recommended to stop these practices per NIST 800-63 and use multi-factor authentication.!!!

**Scenario #3**: Časové limity relací aplikace nejsou správně nastaveny. Uživatel používá pro přístup k aplikaci veřejný počítač, Místo výběru "odhlášení" uživatel jednoduše zavře kartu prohlížeče a odejte. Útočník o hodinu později použije stejný prohlížeč a uživatel zústává stále autentizovaný.

## Odkazy

### OWASP

* [OWASP Proactive Controls: Implement Identity and Authentication Controls](https://www.owasp.org/index.php/OWASP_Proactive_Controls#5:_Implement_Identity_and_Authentication_Controls)
* [OWASP Application Security Verification Standard: V2 Authentication](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Application Security Verification Standard: V3 Session Management](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Testing Guide: Identity](https://www.owasp.org/index.php/Testing_Identity_Management)
 and [Authentication](https://www.owasp.org/index.php/Testing_for_authentication)
* [OWASP Cheat Sheet: Authentication](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
* [OWASP Cheat Sheet: Credential Stuffing](https://www.owasp.org/index.php/Credential_Stuffing_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: Forgot Password](https://www.owasp.org/index.php/Forgot_Password_Cheat_Sheet)
* [OWASP Cheat Sheet: Session Management](https://www.owasp.org/index.php/Session_Management_Cheat_Sheet)
* [OWASP Automated Threats Handbook](https://www.owasp.org/index.php/OWASP_Automated_Threats_to_Web_Applications)

### Externí

* [NIST 800-63b: 5.1.1 Memorized Secrets](https://pages.nist.gov/800-63-3/sp800-63b.html#memsecret) - pro důkladné, moderní, na důkazech založené rady ohledně autentizace.
* [CWE-287: Improper Authentication](https://cwe.mitre.org/data/definitions/287.html)
* [CWE-384: Session Fixation](https://cwe.mitre.org/data/definitions/384.html)
