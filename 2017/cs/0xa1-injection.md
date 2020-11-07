# A1:2017 Injektování

| Původci hrozeb/Vektory útoku | Bezpečnostní slabina | Dopady |
| -- | -- | -- |
| Úroveň přístupu : Využitelnost 3 | Prevalence 2 : Zjistitelnost 3 | Technická úroveň 3 : Obchodní úroveň |
| Injekčním vektorem může být téměř jakýkoli zdroj dat, proměnné prostředí, parametry, externí a interní webové služby a všechny typy uživatelů. [Injekční chyby](https://www.owasp.org/index.php/Injection_Flaws) nastávají, když útočník může odeslat nepřátelská data interpretovi. | Injekční chyby jsou velmi rozšířené, zejména ve starším kódu. Zranitelná místa se často nacházejí v SQL, LDAP, XPath nebo NoSQL dotazech, OS příkazech, XML analyzátorech, SMTP hlavičkách, výrazových jazycích nebo ORM dotazech. Injekční chyby lze při kontrole kódu snadno odhalit. Skenery a fuzzery mohou útočníkům pomoci najít prostor pro injekční chyby. | Injektáž může vyústit ve ztrátu dat, poškození, zpřístupnění neoprávněným stranám, ztrátě odpovědnosti nebo odepření přístupu. Injektáž může občas vést až k úplnému převzetí hostitelem. Dopad podnikání závisí na potřebách aplikace a dat. |

## Je aplikace zranitelná?

Aplikace je náchylná k útoku v těchto případech:

* Aplikace neprovádí ověření, filtraci ani dezinfekci uživatelem zadaných dat 
* Dynamické dotazy nebo neparametrizovaná volání bez kontextově sensitivního escapování se používají přímo v interpretovi.
* Nepřátelská data se používají v rámci parametrů vyhledávání objektově-relačního mapování (ORM) k extrakci dalších citlivých záznamů.
* Nepřátelská data jsou přímo používána nebo spojována tak, že SQL nebo příkaz obsahuje strukturovaná i nepřátelská data v dynamických dotazech, příkazech nebo uložených procedurách.
* Některé z běžnějších injektáží jsou SQL, NoSQL, OS příkaz, Objektově-relační mapování (ORM), LDAP, Expression Language (EL) nebo výrazový jazyk Object Graph Navigation Library (OGNL). Koncept je u všech interpretů stejný. Kontrola zdrojového kódu je nejlepší metodou zjišťování, zda jsou aplikace zranitelné vůči injektáži. Následuje důkladné automatizované testování všech parametrů, záhlaví, URL, cookies, JSON, SOAP a datových vstupů XML. Organizace mohou zahrnout statický zdroj ([SAST](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)) a využít nástroje pro dynamický test aplikace ([DAST](https://www.owasp.org/index.php/Category:Vulnerability_Scanning_Tools)) do CI/CD pipeline k identifikaci nově zavedených injektovaných chyb ještě před nasazením na produkci.

## Jak tomu předcházet?

Prevence injektování vyžaduje uchovávání dat odděleně od příkazů a dotazů.

* Preferovanou možností je použití bezpečného rozhraní API, které zcela zamezí použití interpreta nebo poskytne parametrizované rozhraní nebo migruje za účelem použití nástrojů pro mapování relačních objektů (ORM). ** Poznámka **: I v případě parametrizace, mohou uložené procedury stále zavádět SQL injekci. Děje se tak pokud PL/SQL nebo T-SQL spojí dotazy a data, nebo při provedení příkazu s nepřátelskými daty pomocí EXECUTE IMMEDIATE nebo exec ()
* Použijte pozitivní nebo „whitelist“ ověření na straně serveru. Nejedná se však o úplnou obranu, protože mnoho aplikací vyžaduje speciální znaky, například textové oblasti nebo rozhraní API pro mobilní aplikace.
* U jakýchkoli zbytkových dynamických dotazů použijte speciální znaky pomocí speciální escape syntaxe pro daného interpreta. ** Poznámka **: Názvy tabulek, názvy sloupců ad. ve struktuře SQL nemohou být escapovány, a proto jsou uživatelem zadané názvy struktur nebezpečné. Toto je běžný problém softwaru pro psaní zpráv.
* V rámci dotazů používejte příkaz LIMIT a další ovládací prvky SQL, abyste zabránili hromadnému zveřejnění záznamů v případě SQL injektáže.

## Ukázkové scénáře útoku

**Scénář č. 1**: Aplikace používá při vytvoření následujícího zranitelného volání SQL nedůvěryhodná data:

`String query = "SELECT * FROM accounts WHERE custID='" + request.getParameter("id") + "'";`

**Scénář č. 2**: Podobně slepá důvěra aplikace k frameworku může vyústit v dotazy, které jsou stále zranitelné (např. Hibernate Query Language (HQL)):

`Query HQLQuery = session.createQuery("FROM accounts WHERE custID='" + request.getParameter("id") + "'");`

V obou případech změní útočník hodnotu parametru ’id’ v prohlížeči tak, aby poslal ' or '1'='1. Například:

`http://example.com/app/accountView?id=' or '1'='1`

Tím se změní význam obou dotazů tak, že se vrátí všechny záznamy z tabulky „accounts“. Nebezpečnější útoky mohou změnit nebo odstranit data či dokonce vyvolat uložené procedury.

## Odkazy

### OWASP

* [OWASP Proactive Controls: Parameterize Queries](https://www.owasp.org/index.php/OWASP_Proactive_Controls#2:_Parameterize_Queries)
* [OWASP ASVS: V5 Input Validation and Encoding](https://www.owasp.org/index.php/ASVS_V5_Input_validation_and_output_encoding)
* [OWASP Testing Guide: SQL Injection](https://www.owasp.org/index.php/Testing_for_SQL_Injection_(OTG-INPVAL-005)), [Command Injection](https://www.owasp.org/index.php/Testing_for_Command_Injection_(OTG-INPVAL-013)), [ORM injection](https://www.owasp.org/index.php/Testing_for_ORM_Injection_(OTG-INPVAL-007))
* [OWASP Cheat Sheet: Injection Prevention](https://www.owasp.org/index.php/Injection_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: SQL Injection Prevention](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: Injection Prevention in Java](https://www.owasp.org/index.php/Injection_Prevention_Cheat_Sheet_in_Java)
* [OWASP Cheat Sheet: Query Parameterization](https://www.owasp.org/index.php/Query_Parameterization_Cheat_Sheet)
* [OWASP Automated Threats to Web Applications – OAT-014](https://www.owasp.org/index.php/OWASP_Automated_Threats_to_Web_Applications)

### Externí

* [CWE-77: Command Injection](https://cwe.mitre.org/data/definitions/77.html)
* [CWE-89: SQL Injection](https://cwe.mitre.org/data/definitions/89.html)
* [CWE-564: Hibernate Injection](https://cwe.mitre.org/data/definitions/564.html)
* [CWE-917: Expression Language Injection](https://cwe.mitre.org/data/definitions/917.html)
* [PortSwigger: Server-side template injection](https://portswigger.net/kb/issues/00101080_serversidetemplateinjection)
