# Riziko - Bezpečnostní rizika aplikací

## Co jsou bezpečnostní rizika aplikací?

Útočníci teoreticky mohou použít mnoho různých cest skrz vaši aplikaci, aby poškodili váš podnik nebo organizaci. Každá z takových cest představuje riziko, které může, či nemusí být natolik závažné, aby stálo za pozornost.

![App Security Risks](images/0x10-risk-1.png)

Nalezení a využití těchto cest je někdy jednoduché a někdy velmi obtížné. Obdobně způsobená škoda může být bez následků, ale může i zablokovat vaše podnikání. Chcete-li určit riziko pro svou organizaci, můžete posoudit pravděpodobnost, která je spojena s každým původcem hrozeb, vektorem útoku a bezpečnostní slabinou, a zkombinovat ji s odhadem technického a obchodního dopadu na svou organizaci. Celkové riziko určují tyto faktory společně.

## Jaké riziko plyne pro mě?

[OWASP Top 10](https://www.owasp.org/index.php/Top10) se zaměřuje na identifikaci nejzávažnějších bezpečnostních rizik webových aplikací pro širokou škálu organizací. Ke každému z těchto rizik poskytujeme obecné informace o pravděpodobnosti a technickém dopadu pomocí následujícího jednoduchého schématu hodnocení, které je založeno na OWASP Risk Rating Methodology.  

| Aktéři hrozby | Využitelnost | Rozšíření slabiny | Zjistitelnost slabiny | Technické dopady | Obchodní dopady |
| -- | -- | -- | -- | -- | -- |
| Specifi | Snadný 3 | Rozsáhlé 3 | Snadné 3 | Vážné 3 | Business     |
| cké pro | Průměrný 2 | Běžné 2 | Průměrná 2 | Střední 2 | Specifi |
| aplikaci| Obtížný 1 | Vzácné 1 | Obtížná 1 | Malé 1 |       |

V tomto vydání jsme aktualizovali systém hodnocení rizik, abychom pomohli vypočítat pravděpodobnost a dopad daného rizika. Další podrobnosti naleznete v části [Note About Risks](0xc0-note-about-risks.md). 

Neexistují žádné identické organizace, stejně jako neexistují identičtí útočníci, jejich cíle a dopady útoků. Jestliže jedna organizace používá určitý systém řízení
obsahu (CMS) pro publikování zpráv a systém zdravotní péče používá stejný systém pro ukládání lékařských dat, potom hrozby a rizika pro tyto organizace budou velmi odlišné. Je velmi důležité určit rizika pro vaši organizaci na základě hrozeb, které se na ni vztahují, a potenciálního dopadu útoků.

Where possible, the names of the risks in the Top 10 are aligned with [Common Weakness Enumeration](https://cwe.mitre.org/) (CWE) weaknesses to promote generally accepted naming conventions and to reduce confusion.

Pokud je to možné, jsou názvy rizik v Top 10 sladěny se slabými místy [Common Weakness Enumeration] (https://cwe.mitre.org/) (CWE), které podporují obecně přijímané konvence o pojmenovávání a snižují nejasnosti.

Kde to je možné, jsou názvy rizik v Top 10 sladěny se zranitelnostmi uvedenými v seznamu [Common Weakness Enumeration] (https://cwe.mitre.org/) (CWE), jež podporuje obecně přijímané kovvence pojmenování a zabraňují tak nejasnostem.

## Odkazy

### OWASP

* [OWASP Risk Rating Methodology](https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology)
* [Article on Threat/Risk Modeling](https://www.owasp.org/index.php/Threat_Risk_Modeling)

### Externí

* [ISO 31000: Risk Management Std](https://www.iso.org/iso-31000-risk-management.html)
* [ISO 27001: ISMS](https://www.iso.org/isoiec-27001-information-security.html)
* [NIST Cyber Framework (US)](https://www.nist.gov/cyberframework)
* [ASD Strategic Mitigations (AU)](https://www.asd.gov.au/infosec/mitigationstrategies.htm)
* [NIST CVSS 3.0](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
* [Microsoft Threat Modelling Tool](https://www.microsoft.com/en-us/download/details.aspx?id=49168)
