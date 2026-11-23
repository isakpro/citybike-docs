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
 
1. security: kunder kan andras resor (k5) detta kan leda till dataläckor.
2. 
3. 
4. 
 
## 3. Mätbara krav
 
## 4. Skillnad mot ett annat par
 
