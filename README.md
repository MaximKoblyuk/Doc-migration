# Příprava migrace do Azure ve výrobním podniku

## Cíl dokumentu

Tento dokument popisuje technický a rozhodovací postup pro přípravu migrace infrastruktury a vybraných aplikací do Microsoft Azure. Zaměřuje se na fázi **discovery, assessmentu a business case**, tedy na období před samotnou migrací. Cílem není obhajovat cloud jako univerzální řešení, ale vytvořit podklady pro rozhodnutí, které systémy:

- migrovat do Azure,
- ponechat on-premise,
- převést do hybridního režimu,
- nahradit SaaS službou,
- nebo vyřadit.

Výstupem má být technicky obhajitelný plán, odhad nákladů, seznam rizik a prioritizovaná migrační roadmapa.

## Vstupní situace

Ve výrobních firmách se rozhodnutí o migraci typicky otevírá z těchto důvodů:

- končící životní cyklus serverů, storage nebo virtualizační platformy,
- růst nákladů na obnovu licencí (Windows Server, SQL Server, VMware),
- tlak na rychlejší zpracování dat z výroby, IoT a reportingu,
- omezená kapacita interního provozního týmu,
- požadavek na vyšší odolnost, obnovitelnost a bezpečnost.

Tyto faktory samy o sobě ještě neurčují, že je public cloud správná cílová platforma. Je proto nutné rozhodovat podle naměřených dat, provozních závislostí a ekonomiky jednotlivých workloadů.

## Rozsah 8týdenní přípravné fáze

Doporučený rámec je 8 týdnů, protože umožní zachytit běžný i špičkový provoz a současně připravit rozhodnutí bez zásahu do produkčních systémů. Fáze se dělí do tří pracovních bloků:

1. Discovery a technický sběr dat
2. Finanční a licenční assessment
3. Návrh cílového modelu a migrační strategie

## 1. Discovery a technický sběr dat

### 1.1 Cíl discovery

Discovery má odpovědět na čtyři základní otázky:

- Jaké systémy v prostředí skutečně existují?
- Jaké jsou jejich technické parametry a reálné vytížení?
- Jaké jsou vazby mezi aplikační, databázovou a integrační vrstvou?
- Které systémy mají omezení z pohledu latence, regulace, dostupnosti nebo architektury?

### 1.2 Co se sbírá

Pro každý workload je vhodné získat alespoň následující údaje:

- název systému a jeho business vlastník,
- prostředí (produkce / test / dev),
- platforma (VMware, Hyper-V, fyzický server),
- operační systém, verze a lifecycle status,
- počet vCPU, velikost RAM, velikost disků,
- skutečné vytížení CPU/RAM v čase,
- diskové IOPS, throughput a latence,
- síťové toky a závislosti mezi servery,
- databázový engine, verze a licenční model,
- požadavky na RPO/RTO, zálohování a DR,
- bezpečnostní a regulatorní omezení,
- očekávaný horizont životnosti aplikace.

### 1.3 Nástroje a metody

Pro discovery se běžně používají tyto typy nástrojů:

- **Azure Migrate** pro appliance-based discovery, performance profiling a základní dependency mapping,
- **agent-based discovery** tam, kde je potřeba detailnější aplikační a procesní telemetry,
- doplňkové nástroje jako Device42, Lansweeper nebo CMDB exporty pro inventarizaci,
- síťové a bezpečnostní zdroje (firewall logs, NetFlow, Defender, SIEM) pro potvrzení komunikace,
- specializované OT nástroje (např. Defender for IoT, Claroty, Nozomi), pokud je součástí prostředí výrobní síť.

### 1.4 Délka měření

Krátké měření často vede k chybnému right-sizingu. Pro orientační odhad lze pracovat i s kratším intervalem, pro produkční business case je ale vhodné:

- minimálně 30 dní standardního měření,
- ideálně 6 až 8 týdnů v prostředí s měsíčními nebo kvartálními špičkami,
- explicitně zachytit uzávěrky, dávkové běhy, plánovací cykly a reporting.

### 1.5 Technická rizika v discovery

Mezi časté problémy patří:

- neúplná inventura systémů bez určení vlastníka,
- podcenění integračních vazeb mezi aplikací a databází,
- ignorování OT segmentu a průmyslových protokolů,
- absence údajů o licencích a support statusu,
- měření jen ve „slabém“ období bez zachycení peak loadů,
- směšování produkčních a neprodukčních serverů do jednoho odhadu.

## 2. Finanční a licenční assessment

### 2.1 Cíl assessmentu

Finanční část nemá porovnávat jen „dnešní server vs. jedna cloud VM“. Má vytvořit realistický TCO model pro několik variant:

- zachování on-premise,
- rehost do Azure,
- replatforming vybraných služeb,
- hybridní model,
- případně SaaS náhradu.

### 2.2 Základní komponenty TCO

Do srovnání je vhodné zahrnout minimálně:

- compute,
- storage,
- backup a disaster recovery,
- síťovou komunikaci a egress,
- licence OS a databází,
- monitoring a security služby,
- náklady na provozní správu,
- obnovu hardware a virtualizační vrstvy v on-prem variantě,
- externí podporu nebo implementační náklady.

### 2.3 Right-sizing

Cloudový návrh by neměl kopírovat historické on-prem dimenzování. Doporučený postup:

- vycházet z percentilového zatížení, ne jen z maxima,
- oddělit baseline load od krátkodobých peaků,
- zohlednit růst kapacity a sezónnost,
- navrhovat samostatně compute, storage performance a síťové nároky,
- určit, které workloady jsou vhodné pro rezervace a které vyžadují flexibilitu.

### 2.4 Licence a optimalizace

V licenční oblasti je potřeba ověřit:

- zda existují licence vhodné pro **Azure Hybrid Benefit**,
- zda je aktivní Software Assurance nebo ekvivalentní nárok,
- správnost mapování SQL edic a core licencí,
- možnost využití Reserved Instances nebo Savings Plans,
- omezení spojená s refund cap, exchange politikou a podmínkami CSP partnera.

Před započtením úspor je vhodné provést **Effective License Position (ELP)** nebo ekvivalentní licenční ověření.

### 2.5 Náklady, které bývají podceněné

Při přípravě business case bývají nejčastěji opomíjeny:

- odchozí data z Azure do internetu, on-premise nebo jiného regionu,
- náklady na log management a retention,
- síťová konektivita (VPN / ExpressRoute),
- vyšší storage tier pro databázové a IOPS-citlivé systémy,
- provoz zálohování, replikace a testů obnovy,
- náklady na přechodné období, kdy běží paralelně on-prem i cloud.

## 3. Návrh cílového modelu a migrační strategie

### 3.1 Rozhodovací rámec 6R

Každý workload by měl být zařazen do jedné ze strategií:

- **Rehost** – minimální změna aplikace, rychlé opuštění on-prem infrastruktury,
- **Replatform** – omezené technické změny, přesun na řízené služby,
- **Refactor** – architektonická změna aplikace, typicky cloud-native přístup,
- **Repurchase** – nahrazení stávající aplikace SaaS produktem,
- **Retire** – vyřazení nevyužívaného nebo redundantního systému,
- **Retain** – ponechání mimo cloud z technických, regulatorních nebo ekonomických důvodů.

### 3.2 Kritéria pro rozhodnutí

Pro každý systém je vhodné vyhodnotit alespoň tyto oblasti:

- business kritičnost,
- technický dluh a support status,
- latence a citlivost na síťovou komunikaci,
- závislosti na okolních systémech,
- požadavek na vysokou dostupnost,
- provozní náročnost,
- možnosti licenční optimalizace,
- plánovaný konec životnosti nebo náhrada.

### 3.3 Specifika výrobního prostředí

Ve výrobních podnicích je nutné oddělit dvě vrstvy:

- **enterprise IT** – ERP, docházka, souborové služby, databáze, reporting,
- **OT / výrobní IT** – SCADA, MES, PLC integrace, edge sběr dat, real-time řízení.

Právě druhá vrstva často není vhodná pro prostý přesun do public cloudu. Důvodem bývá:

- požadavek na nízkou latenci,
- vazba na lokální průmyslovou síť,
- certifikace nebo validační omezení,
- potřeba lokálního běhu při výpadku konektivity,
- vysoký objem telemetrie s nevhodnou ekonomikou přenosu.

Z toho důvodu bývá vhodný hybridní model: centrální řízení, analytika a governance v Azure, ale část workloadu ponechaná lokálně nebo na edge platformě.

## 4. Business proces rozhodnutí

### 4.1 Role v rozhodování

Do přípravné fáze by měli být zapojeni minimálně:

- IT manažer / Head of Infrastructure,
- architekt nebo senior administrátor,
- vlastník aplikace za business,
- finance / controlling,
- bezpečnost nebo compliance,
- případně výrobní IT / OT specialista.

### 4.2 Doporučený pracovní postup

#### Týden 1–2
- potvrzení rozsahu a cílů,
- určení seznamu systémů a odpovědných osob,
- příprava přístupů a nasazení discovery nástrojů,
- definice způsobu sběru licenčních a finančních vstupů.

#### Týden 3–5
- kontinuální sběr výkonových dat,
- mapování závislostí,
- identifikace kritických workloadů,
- validace inventáře s vlastníky aplikací,
- první rozdělení systémů na kandidáty pro rehost, replatform, retain a retire.

#### Týden 6–7
- zpracování TCO modelu pro více variant,
- licenční posouzení,
- návrh cílového provozního modelu,
- identifikace technických a organizačních rizik,
- návrh pořadí migračních vln.

#### Týden 8
- prezentace závěrů,
- rozhodnutí o cílové variantě,
- schválení roadmapy, rozpočtu a další fáze.

### 4.3 Rozhodovací artefakty

Na konci přípravné fáze by měly existovat tyto výstupy:

- katalog workloadů,
- matice závislostí,
- right-sizing návrh,
- TCO porovnání variant,
- licenční posouzení,
- 6R klasifikace každého systému,
- seznam rizik a předpokladů,
- návrh migračních vln a cílové architektury.

## 5. Praktické zásady

- Nemigrovat vše jedním přístupem.
- Nepřevádět automaticky historické on-prem dimenzování do cloudu.
- Nepodceňovat síťové vazby a egress.
- Oddělit výrobní a kancelářské workloady.
- Vyřadit nevyužívané systémy před výpočtem cílového stavu.
- Zahrnout do business case i provozní model po migraci.
- U systémů s nízkou latencí nebo pevným výrobním vazbám vždy ověřit, zda cloud vůbec řeší skutečný problém.

## Výsledek

Správně provedená přípravná fáze má vést k rozhodnutí, které je současně:

- technicky proveditelné,
- ekonomicky obhajitelné,
- organizačně zvládnutelné,
- a respektuje omezení výrobního provozu.

Hlavním cílem není „mít cloud“, ale vědět, které části prostředí do něj dávají smysl přesunout, v jakém pořadí, za jakých podmínek a s jakým očekávaným dopadem na náklady, provoz a riziko.
