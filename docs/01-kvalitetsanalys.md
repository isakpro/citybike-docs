# Kvalitetsanalys CityBike
 
## 1. Observationer och egenskaper
 
### K1
Egenskap: Performance efficiency
Delegenskap: Time behaviour
Motivering: Kartan är för långsam under belastning (9 sekunder för 300 användare).
 
### K2
Egenskap: Functional suitability
Delegenskap: Functional correctness
Motivering: kunden får betala två gånger för en resa och då blir resultatet fel och det berör även Reliability eftersom felet uppstår när det är dålig täckning.

### K3
Egenskap: Reliability
Delegenskap: Fault tolerance
Motivering: resan ska fungera vidare och positionerna ska inte försvinna även om styrenheten tappar uppkoling

### K4
Egenskap: Interaction capability
Delegenskap: Learnability
Motivering: nya kunder hittar inte knappen som avlustar resan vilket ger massa samtal till kundtjänst

### K5
Egenskap: Security
Delegenskap: Confidentiality
Motivering: en kund kommer åt andra kunders resor om hen ändrar id i adressen

### K6
Egenskap: Maintainbility
Delegenskap: Modularity
Motivering: eftersom prisberäkningen sitter ihop med bokningsflödet så gör det att en ändring på ett ställe påverkar båda

### K7
Egenskap: Interaction capability
Delegenskap: Operability
Motivering: tekniker kan inte använda sig av adminpanel på en surfplatta då knapparna är för små och allt innehåll hamnar fel, alltså det anpassar sig inte beroende på skärmstorlek

### K8
Egenskap: Safety
Delegenskap: fail safe
Motivering: om ett batteri blir för varmt är det brandrisk så laddningen måste stängas av och tekniker ska få ett larm när det överstiger 60 grader

### K9 
Egenskap: compatibility
Delegenskap: interoperability
Motivering: API måste kunna ta emot data från två olika modeller av styrenheten med olika dataformat

### K10 
Egenskap: flexiblity
Delegenskap: adaptbilty
Motivering: systemet går inte att anpassa till en ny stad utan att behöva skriv om koden, även nman priser och zoner är hårdkodade
 
## 2. De fyra viktigaste egenskaperna för CityBike
 
1. security: kunder kan se andras resor (k5) och lösenord lagras utan salt (R11) detta kan leda till dataläckor.
2. functional suitability: om pristet blir fel (k2 avsnitt 2) då kommer kunderna betala fel och förtroendet för företaget minskar och även kundtjänst kommer få fler ärenden
3. safety: om laddningen inte avbryts när det blir för varmt (k8 avsnitt7) så kan det leda till att en cykel börjar brinna
4. reliability: om resor och position försvinner vid dålig täckning (k3 avsnitt4) så går det ej att räkna ut rätt pris eller cyklarnas position
 
## 3. Mätbara krav

## Krav 1: Security
Krav: Av 100 anrop där en inloggad kund begär en resa som tillhör en annan kund så ska 0 anrop returnera resans data.
Mått: antal androp mot /trips/{id} med en annan kunds res-id som returnerar resdata
Gränsvärde: 0 av 100 anrop 0%
Mätmetod: automatiska api-tester som loggar in som en kund och anroppar 100 resor som tillhör en anna kund, svaren ska bli 403 eller 404
Hänvisning: K5, avsnitt 3 (s3) och avsnitt 5

## Krav 2: Functional suitability
Krav: När en belaltningsbegäran skickas 2-5 gånger ska kunden bara debiteras för 1 gång, för 1000 av 1000 test resor
Mått: antal debiteringar per resa hos betaltjänst
Gränsvärde:högst 1 debitering per resa, 0 dubbeldebiterngar på 1000 resor
Mätmetod: integrationstest mot betaltjänsten i en testmiljö där en betalningbegäran skickas flera gånger
Hänvisning: K2 avsnitt 2 och 4

## Krav 3: Safety
Krav: när batteriet överstiger 60 grader ska laddningen avbrytas och tekniker larmas inom 5 sekunder i 100 av 100 tester
Mått: tid från att temperaturen överstiger 60 grader till att laddningen avbryts och larmet syns i adminpanelen
Gränsvärde: 5 sekunder i alla 100 tester
Mätmetod: test i testrigg där batteriets sensor hettast upp och tiden loggas
Hänvisning: k8 avsnitt 7

## Krav 4: Reliability
Krav: efter avbrott i mobiltäckningen på upp till 30 minuter ska minst 99% av styrenhetens positioner finnas i Gpspoints inom 2 minuter efter uppkopplingen har kommit tillbaka
Mått: andel mottagna positioner av förväntade positioner, 30minuter/15sekunder = 120st
Gränsvärde:
Mätmetod: test där modemet stängs av i 30 minuter under resan och sedan räkna raderna i Gpspoint för resan
Hänvisning:K3 avsnitt 4 och 7

### Uträkning: tillgänglighet 99,7%
tillåten nedtid ärr 100 - 99.7 = 0.3%
30 dagar = 720 timmar = 43200 minuter
43200 x 0.003 = 129.6 minuter
det får vara 130 minuter nedtid på 30 dagar.



 
## 4. Skillnad mot ett annat par
 --
