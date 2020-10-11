# +A: Aplikační manažeři, co dál?

## Spravujte celý životní cyklus aplikace

Aplikace patří k nejsložitějším systémům, které lidé pravidelně vytvářejí a udržují. Správa aplikace by měla být prováděna IT specialisty, kteří jsou zodpovědní za její celkový životní cyklus. Navrhujeme zavedení role správce aplikací jako technického protějšku vlastníka aplikace. Správce aplikací má na starosti celý životní cyklus aplikace z pohledu IT, od shromažďování požadavků až po proces archivace systémů, který je často přehlížen.

## Požadavky a správa zdrojů

* Shromažďujte a vyjednávejte obchodní požadavky na aplikaci s obchodím oddělením, včetně požadavků na ochranu s ohledem na důvěrnost, autenticitu, integritu a dostupnost všech datových aktiv a očekávanou obchodní logiku.
* Sestavte technické požadavky včetně funkčních a nefunkčních bezpečnostních požadavků.
* Naplánujte a vyjednejte rozpočet, který pokrývá všechny aspekty návrhu, sestavení, testování a provozu, včetně činností spjatých se zaručením bezpečnosti.

## Žádost o návrhy (RFP) a uzavírání smluv

* Vyjednejte požadavky s interními i externími vývojáři, včetně pokynů a bezpečnostních požadavků týkajících se vašeho bezpečnostního programu např.: Secure Development Lifecycle – SDLC, osvědčené postupy atd.
* Ohodnoťte splnění všech technických požadavků, včetně fáze plánování a návrhu.
* Vyjednejte všechny technické požadavky, včetně designu, zabezpečení a dohod o úrovni služeb (Service Level Agreement – SLA).
* Přijměte šablony a kontrolní seznamy, například [OWASP Secure Software Contract Annex](https://www.owasp.org/index.php/OWASP_Secure_Software_Contract_Annex). **Poznámka**: Příloha se vztahuje na smluvní právo USA, proto vzorovou přílohu před použitím konzultujte s kvalifikovaným právním poradenstvím.

## Plánování a design

* Vyjednávejte plánování a design s vývojáři a interními akcionáři, např.: bezpečnostnimi specialisty.
* Definujte architekturu zabezpečení, ovládací prvky a protiopatření odpovídající potřebám ochrany a očekávané úrovni ohrožení. Vše uvedené by mělo být podporováno bezpečnostními specialisty.
* Zajistěte, aby vlastník aplikace přijal zbývající rizika nebo poskytl další zdroje.
* V každém sprintu zajistěte vytvoření příběhů spjatých se zabezpečením, které obsahují omezení přidaná pro nefunkční požadavky.

## Nasazení, testování a zavedení

* Automatizujte zabezpečené nasazení aplikace, rozhraní a všech požadovaných komponent, včetně potřebných oprávnění.
* Vyzkoušejte technické funkce a integraci s IT architekturou a koordinujte obchodní testy.
* Vytvářejte testovací případy „použití“ a „zneužití“ z technického a obchodního hlediska.
* Spravujte bezpečnostní testy podle interních procesů, potřeb ochrany a předpokládané úrovně ohrožení aplikací.
* Uveďte aplikaci do provozu a v případě potřeby proveďte migraci z dříve používaných aplikací.
* Dokončete veškerou dokumentaci, včetně CMDB a bezpečnostní architektury.

## Provoz a řízení změn

* Provoz musí zahrnovat pokyny pro správu zabezpečení aplikace (např.: správu oprav).
* Zvýšte povědomí o zabezpečení uživatelů a vyřešte konflikty ohledně použitelnosti vs. bezpečnosti.
* Plánujte a spravujte změny, např.: migrujte na nové verze aplikace nebo jiné komponenty, jako je OS, middleware a knihovny.
* Aktualizujte veškerou dokumentaci, včetně CMDB a bezpečnostní architektury, ovládacích prvků a protiopatření, včetně definic rutinních postupů nebo projektové dokumentace.

## Archivace systémů

* Veškerá požadovaná data by měla být archivována. Všechna ostatní data by měla být bezpečně vymazána.
* Bezpečně odstraňte aplikaci, včetně odstranění nepoužívaných účtů, rolí a oprávnění.
* Nastavte stav aplikace na vyřazený v CMDB.