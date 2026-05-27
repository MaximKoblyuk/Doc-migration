# EnterCloud — Azure migrace

**Postup zdarma**  
**Jak za 8 týdnů sestavit plán migrace do Azure a snížit TCO až o 30 %**  
_Autor: EnterCloud · Microsoft Solutions Partner_

## Pro vedoucí IT oddělení

Ve výrobních firmách se opakují stejné situace: rostoucí datové toky z IoT, dražší obnovy on-prem licencí, přetížené interní týmy a tlak na inovace. Cílem není „migrovat za každou cenu“, ale udělat **datově podložené rozhodnutí**:

- migrovat,
- zůstat on-prem,
- nebo zvolit hybrid.

Během 8 týdnů Discovery + Assessment získáte podklady pro rozhodnutí bez zásahu do produkce a bez přetěžování týmu.

## 3 kroky správného rozhodnutí

### 1) Automatizovaný sběr dat a mapování závislostí

- Nasazení nástrojů (typicky Azure Migrate) do stávajícího prostředí.
- Sběr reálných metrik: CPU, RAM, IOPS, síťové vazby.
- Pro spolehlivý right-sizing doporučeno min. 30 dní, ve výrobě typicky 6–8 týdnů.
- Důraz na mapu závislostí aplikace ↔ databáze (prevence latence a egress nákladů).

**Časté slepé skvrny:**
- Agentless vs. agent-based discovery (hloubka analýzy).
- OT/IoT (SCADA, MES, PLC) mimo standardní rozsah — vyžadují specializované nástroje.

### 2) Finanční TCO analýza a licenční optimalizace

- Right-sizing podle reálného zatížení (ne podle historického overprovisioningu).
- Azure Hybrid Benefit (AHB) pro Windows/SQL licence se Software Assurance.
- Reserved Instances / Savings Plans pro 24/7 workloady.
- ELP audit před aktivací licenčních benefitů.

**Klíčové ekonomické body:**
- 1Y/3Y závazky významně snižují compute náklady.
- Pozor na refund cap, podmínky storna a exchange politiku.
- U CSP modelu vždy prověřit konkrétní podmínky poskytovatele.
- Nezapomenout na **egress** (odchozí data) jako častý skrytý náklad.

### 3) Volba migrační strategie (6R)

- **Rehost** (rychlost)
- **Replatform** (úleva provozu)
- **Refactor** (strategická inovace, vyšší riziko a náklady)
- **Repurchase** (SaaS náhrada)
- **Retire** (vypnutí nepotřebných systémů)
- **Retain** (vědomé nemigrování)

Ve výrobě jsou často kritické právě **Retire** a **Retain**: ne vše patří do public cloudu.

## Co získáte jako výstup

1. **Objektivní rozhodovací rámec** podložený daty.  
2. **Přehled o kritických rizicích** (technických i finančních).  
3. **Strukturovaný proces** Discovery/Assessment navázaný na CAF (Plan → Ready → Adopt → Govern → Manage).

## Doporučení pro business case

Použijte vrstvený model závazků podle typu workloadu:

- Predikovatelné workloady (ERP, DB, AD): 3Y RI + AHB
- Stabilní compute s potřebou flexibility: Savings Plans
- Variabilní/dev-test: 1Y RI nebo PAYG s auto-shutdown
- Batch/přerušitelné workloady: Spot VMs
- Edge/MES/SCADA: Azure Local / Azure IoT Edge (latence a regulace mají prioritu)

## Konzultace zdarma (30 minut)

Získáte:

- druhý názor na vaši migrační úvahu,
- orientaci v licenční pozici (Windows/SQL + Azure),
- odhad, zda má 8týdenní Discovery pro vaši situaci nejvyšší přínos.

**EnterCloud — Microsoft Solutions Partner (Infrastructure/Azure, Data & AI)**
