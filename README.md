# Azure Migration Readiness Assessment

## 1. Dokumentový kontext

- **Typ dokumentu:** Consultant delivery document (Readiness Assessment)
- **Účel:** Podklad pro rozhodnutí o migraci, hybridním modelu nebo ponechání workloadů on-premise
- **Časový rámec:** 8 týdnů (Discovery + Assessment)
- **Primární publikum:** CIO/CTO, IT management, enterprise architektura, finance, bezpečnost, OT/výrobní IT

## 2. Executive Summary

Cílem této fáze není realizovat migraci, ale vytvořit rozhodovací podklady pro management. Hodnocení je založené na měřených provozních datech, mapě technických závislostí, licenční pozici a finančním modelu variant.

Rozhodnutí pro každý workload musí být přiřazeno do 6R strategie (Rehost, Replatform, Refactor, Repurchase, Retire, Retain) a zdokumentováno včetně dopadu na náklady, rizika, provozní model a interní kapacity.

## 3. Cíle a očekávané výsledky

### 3.1 Cíle

- Vytvořit ověřený katalog systémů a jejich vlastníků.
- Získat výkonová data potřebná pro right-sizing.
- Zmapovat aplikační a datové závislosti.
- Vyhodnotit licenční možnosti a omezení.
- Připravit porovnání TCO pro relevantní cílové varianty.
- Navrhnout migrační vlny a pořadí realizace.

### 3.2 Očekávané výsledky

- Rozhodovací matice workloadů podle 6R.
- Prioritizovaná roadmapa další fáze.
- Seznam klíčových rizik a mitigací.
- Ekonomický model s transparentními předpoklady.

## 4. Rozsah a mimo rozsah

### 4.1 In-scope

- Discovery serverové a aplikační vrstvy (enterprise IT).
- Sběr výkonových metrik a dependency mapping.
- TCO model a licenční assessment.
- Návrh cílového modelu (cloud/hybrid/on-prem).
- Governance návrh pro navazující implementační fázi.

### 4.2 Out-of-scope

- Produkční migrace workloadů.
- Refactoring aplikací v této fázi.
- Detailní implementační design cílové platformy.
- Kompletní změnové řízení provozních týmů.

## 5. Pracovní předpoklady a závislosti

- Dostupnost technických ownerů systémů.
- Přístup do virtualizační a síťové vrstvy pro discovery nástroje.
- Poskytnutí podkladů k licencím (Windows/SQL/VMware).
- Potvrzené bezpečnostní podmínky pro sběr dat.
- Schopnost provozu sběru alespoň 30 dní (preferovaně 6–8 týdnů).

## 6. Metodika a pracovní postup

### 6.1 Stream A — Discovery a technická analýza

**Aktivity**
- Inventura workloadů, prostředí a vlastníků.
- Sběr metrik CPU, RAM, disk performance, síťové komunikace.
- Analýza závislostí aplikace ↔ databáze ↔ integrační služby.
- Identifikace workloadů s latencí-citlivým nebo regulatorním omezením.

**Výstupy**
- Asset katalog.
- Dependency matice.
- Technický profil workloadů.
- Seznam kandidátů pro Retain/Retire.

### 6.2 Stream B — Finanční a licenční assessment

**Aktivity**
- Definice TCO scénářů (on-prem / rehost / hybrid / selected replatform).
- Right-sizing na základě měřených dat.
- Ověření AHB, RI, Savings Plans, ELP vstupů.
- Vyčíslení nákladů na síť, egress, monitoring, backup a DR.

**Výstupy**
- TCO model variant.
- Licenční posouzení a omezení.
- Doporučení commitment strategie dle typu workloadu.

### 6.3 Stream C — Strategie a governance

**Aktivity**
- Klasifikace všech workloadů podle 6R.
- Návrh cílového provozního modelu (role, odpovědnosti, provozní procesy).
- Návrh migračních vln podle kritičnosti a proveditelnosti.
- Definice rizik, mitigací a rozhodovacích checkpointů.

**Výstupy**
- 6R rozhodovací matice.
- Migrační roadmapa (vlny 1..n).
- Risk register + mitigation plan.
- Management summary pro schvalovací fórum.

## 7. Řídicí model (governance)

### 7.1 Role

- **Executive Sponsor:** schvalování směru a budgetu.
- **IT Lead:** koordinace technických vstupů a priorit.
- **Cloud/Infra Architect:** cílový návrh a technická validace.
- **Finance Controller:** validace nákladových modelů a předpokladů.
- **Security/Compliance Lead:** posouzení regulatorních omezení.
- **OT Representative:** validace dopadů na výrobní prostředí.

### 7.2 Cadence

- Týdenní pracovní status (operativa).
- Dvoutýdenní steering checkpoint (řízení rizik a rozhodnutí).
- Závěrečný decision workshop (schválení doporučené varianty).

## 8. Časový plán (8 týdnů)

| Fáze | Týdny | Hlavní výstup |
|---|---:|---|
| Mobilizace a setup | 1–2 | Potvrzený scope, přístupy, aktivní sběr |
| Discovery běh | 3–5 | Metriky, dependency mapping, předběžná segmentace |
| Assessment a návrh | 6–7 | TCO model, licenční posouzení, 6R návrh |
| Finalizace | 8 | Schvalovací balíček a roadmapa |

## 9. Kritická rizika a mitigace

| Riziko | Dopad | Mitigace |
|---|---|---|
| Krátké měření bez peak období | Chybný right-sizing a budget | Min. 30 dní, preferovaně 6–8 týdnů |
| Neúplná inventura | Nesprávný scope a pořadí migrace | Validace katalogu s business ownery |
| Podceněné integrační vazby | Výpadky nebo latence po přesunu | Dependency mapping + wave planning |
| Neověřené licence | Nadhodnocené úspory / compliance riziko | ELP/licenční review před rozhodnutím |
| Ignorování OT omezení | Provozní riziko ve výrobě | Zapojení OT specialisty do rozhodnutí |
| Podcenění egress a síťových nákladů | Odchylka TCO od reality | Samostatná nákladová kapitola pro network |

## 10. Rozhodovací kritéria pro workloady

Každý workload má mít minimálně tyto atributy:

- business kritičnost,
- technický stav a lifecycle,
- latence a dostupnost,
- integrační závislosti,
- bezpečnost/regulace,
- nákladová efektivita cílového modelu,
- doporučená 6R strategie,
- priorita migrační vlny.

## 11. Konečné deliverables

1. **Workload Inventory Catalogue**
2. **Application & Data Dependency Map**
3. **Right-Sizing and Target Sizing Sheet**
4. **TCO Scenario Model (multi-variant)**
5. **Licensing & Commitment Assessment**
6. **6R Decision Matrix**
7. **Migration Wave Plan**
8. **Risk Register & Mitigation Plan**
9. **Steering Committee Decision Pack**

## 12. Akceptační kritéria fáze

Fáze je považována za uzavřenou, pokud:

- všechny in-scope workloady mají přiřazenou strategii 6R,
- TCO model obsahuje zdrojové předpoklady a citlivostní komentář,
- rizika mají ownera a navrženou mitigaci,
- steering committee schválí doporučený postup další fáze.
