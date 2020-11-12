# PV Poznámky k vydání

## Co se změnilo ve verzi 2017 oproti 2013?

Poslední čtyři roky se toho změnilo hodně, proto OWASP Top 10 také potřeboval změny. Top 10 jsme kompletně reorganizovali, aktualizovali metodiku, aplikovali nový proces sběru dat, navázali interakci s komunitou, přeuspořádali jsme naše rizika, přepsali každé riziko od základu a přidali jsme odkazy na běžně používané aplikační rámce (frameworks) a jazyky.

V posledních letech se základní technologie a aplikační architektura hodně změnily:

* Mikroslužby napsané v node.js a Spring Boot nahrazují tradiční monolitické aplikace. Mikroslužby přicházejí s vlastními bezpečnostními výzvami, jako je navázání důvěry mezi mikroslužbami, kontejnery, správou citlivých dat atd. Starý kód, u něhož se nikdy neočekávalo, že bude přístupný z internetu, je nyní umístěn za API nebo RESTful webovými službami, které budou využívat jednostránkové aplikace (Single Page Applications) (SPA) a mobilní aplikace. Architektonické předpoklady kódu, jako jsou trusted callers, již nejsou platné.
* Jednostránkové aplikace napsané v JavaScriptových aplikačních rámcích (například Angular a React) umožňují vytváření vysoce modulární, multičunkcní rozhraní. Funkce na straně klienta, která je tradičně poskytována na straně serveru, přináší své vlastní bezpečnostní výzvy.
* JavaScript je v současné době hlavním jazykem webu s node.js běžícím na straně serveru a moderními webovými aplikačními rámci (například Bootstrap, Electron, Angular a React) běžícími na klientovi.

## Nové problémy zdůrazněné daty

* **A4:2017-XML External Entities (XXE)** is a new category primarily supported by source code analysis security testing tools ([SAST](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)) data sets.
* **A4:2017-XML External Entities (XXE)** je nová kategorie, která byla nalezena hlavně prostřednictvím nástroje SAST (Source Code Analysis Security TestTools) ([SAST](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)).

## Nové problémy zdůrazněné komunitou

Požádali jsme komunitu, aby zvážila dvě slibné kategorie hrozeb. Po obdržení více než 500 recenzí a vyloučení již identifikovaných hrozeb (např. Sensitive Data Exposure a XXE) byly stanoveny následující kategorie:

* **A8:2017-Insecure Deserialization**, které umožňuje vzdálené spuštění kódu nebo manipulaci s citlivými objekty na postižených platformách.
* **A10:2017-Insufficient Logging and Monitoring**, které mohou narušit detekci škodlivých akcí nebo hackerů, reakci na incidenty, stejně jako vyšetřování počítačové kriminality.

## Sloučeny nebo v ústraní, ale nezapomenuty

* **A4-Insecure Direct Object References** a **A7-Missing Function Level Access Control** spojeny do **A5:2017-Broken Access Control**.
* **A8-Cross-Site Request Forgery (CSRF)** byl nalezen pouze u 5 % aplikací, protože většina aplikačních růmců má [orchranu před](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)).
* **A10-Unvalidated Redirects and Forwards** i když bylo nalezeno asi u 8 % aplikací, byla tato kategorie nahrazena XXE.

![0x06-release-notes-1](images/0x06-release-notes-1.png)
