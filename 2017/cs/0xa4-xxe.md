# A4:2017 Externí entity XML (XXE)

| Původci hrozby/Vektor útoku | Bezpečnostní slabina           | Dopady               |
| -- | -- | -- |
| Aplikačně specifické : Zneužitelnost 2 | Rozšíření 2 : Zjistitelnost 2 | Technické 3 : Obchodní |
| Útočníci mohou zneužít zranitelné procesory XML, pokud mohou nahrát XML, zahrnout nepřátelský obsah do dokumentu XML nebo zneužít zranitelný kód, závislosti nebo integrace. | Mnoho starších procesorů XML umožňuje ve výchozím stavu specifikaci externí entity, identifikátoru URI, který je dereferencován a vyhodnocen během zpracování XML. Nástroje [SAST](https://www.owasp.org/index.php/Source_Code_Analysis_Tools) mohou tyto problémy objevit kontrolou závislostí a konfigurace. Nástroje [DAST](https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools) vyžadují k odhalení a zneužití tohoto problému další manuální kroky. Manuální testeři musí být vyškoleni v tom, jak XXE testovat. Od roku 2017 se totiž již běžně netestuje. | Tyto chyby lze využít k extrakci dat, spuštění vzdáleného požadavku ze serveru, skenování interních systémů, provedení útoku odmítnutí služby a také k provedení dalších útoků. |

## Je aplikace zranitelná?

Aplikace a zejména webové služby založené na XML nebo následné integraci mohou být zranitelné vůči útoku, pokud:

* Aplikace přijímá XML přímo nebo nahrává, zejména z nedůvěryhodných zdrojů, nebo vkládá nedůvěryhodná data do XML dokumentů, které pak analyzuje XML procesor.
* Kterýkoli z procesorů XML v aplikaci nebo ve webových službách založených na protokolu SOAP má povolenu [definici typu dokumentu (DTDs)](https://en.wikipedia.org/wiki/Document_type_definition). Přesný mechanismus deaktivace zpracování DTD se liší podle procesoru, proto je dobrým zvykem takové možnosti zkonzultovat [OWASP Cheat Sheet 'XXE Prevention'](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Prevention_Cheat_Sheet).
* Aplikace využívá standard SAML pro zpracování identity v rámci federovaného zabezpečení nebo jednotného přihlášení (SSO). SAML využívá XML pro tvrzení identity a může být zranitelný.
* Aplikace používá SOAP před verzí 1.2. Pravděpodobně je náchylná k útokům XXE, pokud jsou entity XML předávány do frameworku SOAP.
* Zranitelnost vůči XXE útokům pravděpodobně znamená, že aplikace je zranitelná vůči útokům odmítnutí služby (DoS), včetně útoku Billion Laughs

## Jak se mohu bránit?

Pro identifikaci a zmírnění XXE je zásadní školení vývojářů. Kromě toho prevence XXE vyžaduje:

* Kdykoli je to možné, používejte méně složité datové formáty, jako je JSON, a vyhněte se serializaci citlivých dat. 
* Opravte nebo proveďte upgrade všech procesorů XML a knihoven používaných aplikací nebo základním operačním systémem. Použijte nástroje pro kontrolu závislostí. Aktualizujte SOAP na SOAP 1.2 nebo vyšší
* Zakažte externí entitu XML a zpracování DTD ve všech analyzátorech XML v aplikaci, podle [OWASP Cheat Sheet 'XXE Prevention'](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Prevention_Cheat_Sheet). 
* Implementujte pozitivní („whitelisting“) ověření vstupu na straně serveru, filtrování nebo sanitaci, abyste zabránili nepřátelským datům v dokumentech XML, záhlavích nebo uzlech.
* Ověřte, zda funkce nahrávání souborů XML nebo XSL ověřuje příchozí XML pomocí XSD nebo podobného ověření.
* Nástroje SAST mohou pomoci detekovat XXE ve zdrojovém kódu, ačkoli ve velkých a složitých aplikacích s mnoha integracemi je nejvhodnější variantou manuální kontrola kódu.  

Pokud není možné tyto preventivní kroky vykonat, zvažte detekci, monitorování a blokování XXE útoků použitím virtuálních oprav, bezpečnostních bran API, nebo pomocí Web Application Firewalls (WAFs).

## Příklady útočných scénářů

Objevuje se početné množství veřejných XXE problémů, včetně napadení vestavěných zařízení. XXE se vyskytuje na mnoha neočekávaných místech, včetně hluboce vnořených závislostí. Nejjednodušší způsob je nahrát škodlivý soubor XML, pokud je přijat:

**Scénář #1**: Útočník se pokouší extrahovat data ze serveru:

```
  <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [
    <!ELEMENT foo ANY >
    <!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
    <foo>&xxe;</foo>
```

**Scénář #2**: Útočník sonduje privátní síť serveru změnou níže uvedeného řádku ENTITY na:

```
   <!ENTITY xxe SYSTEM "https://192.168.1.1/private" >]>
```

**Scénář #3**: Útočník se pokusí o útok typu odmítnutí služby (DoS) zahrnutím potenciálně nekonečného souboru:

```
   <!ENTITY xxe SYSTEM "file:///dev/random" >]>
```

## Odkazy

### OWASP

* [OWASP Application Security Verification Standard](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project#tab=Home)
* [OWASP Testing Guide: Testing for XML Injection](https://www.owasp.org/index.php/Testing_for_XML_Injection_(OTG-INPVAL-008))
* [OWASP XXE Vulnerability](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Processing)
* [OWASP Cheat Sheet: XXE Prevention](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: XML Security](https://www.owasp.org/index.php/XML_Security_Cheat_Sheet)

### Externí

* [CWE-611: Improper Restriction of XXE](https://cwe.mitre.org/data/definitions/611.html)
* [Billion Laughs Attack](https://en.wikipedia.org/wiki/Billion_laughs_attack)
* [SAML Security XML External Entity Attack](https://secretsofappsecurity.blogspot.tw/2017/01/saml-security-xml-external-entity-attack.html)
* [Detecting and exploiting XXE in SAML Interfaces](https://web-in-security.blogspot.tw/2014/11/detecting-and-exploiting-xxe-in-saml.html)
