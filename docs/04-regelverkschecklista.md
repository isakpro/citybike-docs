# Regelverkschecklista för CityBike
 
## GDPR
 
### G1 Radering av kundens uppgifter
Gäller: Ja
Skäl: Art. 17, kunden har rätt att få uppgifterna raderade.
Ansvarig: Backend-utvecklare
Verifieras med: Nivå integration, testtyp funktionell
Bevis: rapport fårn ett test som visar Name, personnummer emial och phone

### G2 Lagringstid för positioner och resor
Gäller: ja
Skäl: Art. 5.1 e, positioner i GpsPoints sparas i dag utan slut datum (R2, A2)
Ansvarig: backend utvecklare
Verifieras med: nivå integration, testtyp funktionell
Bevis: logg från gallringsjobb och även en testrapport som visar att positioner inte är äldre än 30 dagar som finns kvar

### G3 Behörighet i adminpanelen
Gäller: ja
Skäl: Art. 32 och Art. 25. kundtjänst delar på ett konto och ser allt inklusive personnummer
Ansvarig: utvecklare 
Verifieras med: nivå system, testtyp funktionell
Bevis: en testrapport som visar att en kundtjänstroll inte ser personnummer

### G4 Inga personuppifter i loggfiler
Gäller: Ja
Skäl: Art. 5.1 c och Art. 32. API loggar all innehåll i varje anropp i 12 månader
Ansvarig: backend utvecklare
Verifieras med: nivå integration testtyp funktionell
Bevis: en testrapport och utdrag ur loggfil som visar att personnummer och lösenord inte syns

### G5 Samtycke till nyhetsbrev
Gäller: Ja
Skäl: Art 6.1 och Art. 21 även marknadsföringslagen 19§ kunden får nyhetsbrev utan förfrågan
Ansvarig: utvecklaren
Verifieras med: nivå acceptans testtyp funktionell
Bevis: ett test som visar att en någon som ej kryssat i rutan inte får brevet.

### G6 Avtal och överföring till analysverktyget
Gäller: Ja
Skäl: Art. 28 och Art. 44-46 leverantör tar emot och lagrar personuppgifter utan avtal i USA
Ansvarig: Ledningen
Verifieras med: nivå acceptans testtyp funktionell
Bevis: ett personuppgiftsbittädesavtal och utrag som visar att leverantören har certifierade och bevis rapport att ingen epost är skickad.

### G7 Säker lagring av lösenrod
Gäller: ja
Skäl: art. 32 lösenord SHA-256 utan salt
Ansvarig: backend utvecklare
Verifieras med: nivå enhet testtyp icke funktionell
Bevis: en testrapport som visar att kunder med samma lösenord får olika hashningar

## CE och produktkrav

### C1 Maskindirektivet 2006/42/EG och maskinförodringen (EU) 2023/1230
Gäller: Osäkert
Skäl: cykeln har max 250 watt och går 25kmh/h och räknas inte som ett motorfordon och omfattas av maskindirektivet och sen 2027 även maskinförordningen och citybike säljer ej cykel så ansvaret ligger då hos tillverkarna men det kan läggas på citybike eftersomde monterar styreneht och lås
Ansvarig: Ledningen men ta hjälp av jurits
Verifieras med: nivå acceptns testtyp icke funktionell
Bevis: en sortts överrenstämmelse med mellan tillverkarna och juristen.

### C2 EN 15194 för elcyklar
Gäller: ja
Skäl: EN 15194 är standard för elcyklar med 250 watt och max hastighet på 25km/h och det används för att visa att cykeln upfyller maskindirektivet
Ansvarig: ledningen
Verifieras med: nivå system testtyp icke funktionell
Bevis:rapport enlight EN 15194

### C3
Gäller: ja
Skäl: eftersom det är ett modem och en gps mottager i styrenhet så räknas det som radioutrustning och citybike är eget varumärke och krav för cybersäkerhet gäller
Ansvarig: ledning och utvecklare
Verifieras med:nivå system testtyp icke funktioonell
Bevis:rappot för radio, elsäkerthet och cybersäkerhet

### C4
Gäller: ja
Skäl: det ör litiumbatteri för lätt transportmedel och det uppfyller EN 50604-1 och även batteriförodrningen, och styrenheten ser till så att laddning avbyts vid överhättning.
Ansvarig: ledningen och utvecklare
Verifieras med: nivå system testtyp icke funktionell
Bevis: rapport fårn batterileverantören 

### C5
Gäller:ja
Skäl: styrenehten ska inte störa annat och ska själv inte bli stört av annan radioutrustning och liknande.
Ansvarig: ledningen
Verifieras med: nivå system, testtyp icke funktionell
Bevis: rapport för styrenheten

## cyber Resilience Act

### CRA1
Gäller: ja
Skäl:detr ska finnas förteckning för alla komponenter eftrsom styrenhetens firmware är en produkt med digitla element och citybike är tillverkaren
Ansvarig: utvecklare
Verifieras med: nivå enhet, testtyp ickefunktionell
Bevis: automatisk Sbom vid varje bygge

### CRA2
Gäller: ja
Skäl: alla uppdateringar ska vara redo och signerade så det uppdateras under supportperioden
Ansvarig: utveckjlare
Verifieras med: nivå system testtyp funktionell
Bevis: rapport från testrigg som visar att en signerad uppdatering installeras

### CRA3
Gäller: ja
Skäl: ska finnas rutin för att ta emot och åtgärda eventuella sårbarheter och rapportera till ENISA inom 24hr
Ansvarig: ledning och utvecklare
Verifieras med: nivå acceptans testtyp funktionell
Bevis: skriftilg rutin med kontaktperson rapport och protokoll och en test övning

### CRA4
Gäller: osäkert
Skäl: lösenord utan slat med SHA-256 och det går emot krav för skydd av data
Ansvarig: utvecklare
Verifieras med: nivå enhet testtyp ickefunktionell
Bevis: rapport som visar att lösenord hashas med salt

## Spårbarhet

### K1 Batteriet får inte överstiga 60 grader vid laddning
Källa: C4
Testfall: det ska monteras en styreneht med den firmware som ska testas med ett batteri och laddare, starta laddning, höj temperaturen lite i taget tills det blir 61 grader. kontrollera att laddning avbryts inom 5 sekunder och ett larm skickas ut
Nivå och testtyp: system icke funktionell
Resultat som ska sparas: tid och datum, testperson, vilken firmware, styrenehets serienummer, temperatur och när det avbröts, tid tills larm kom in, godkänt eller underkänt resultat
Teknisk dokumentation: rapport som ska sparas i 10 år

### K2 Kundens uppgifter raderas när konto stängs
Källa: G1
Testfall: skapa en kund personnummer namn epost och telefonnummer, gör sedan två testresor sen stäng kontot. kolla i databasen om dessa personuppgifter är borttagna, men Trips och PriceSek ska finnas kvar
Nivå och testtyp: integration testtyp funktionell
Resultat som ska sparas: datum, programverison, testdatabas, reslutat av databasen, godkänt eller underkänt
Teknisk dokumentation: logg från CI 

## Kontrollfrågor
1. citybike räknas som tillverkar då de har eget varumärke och äger firmware
2. ny firmware måste alltid testa speciellt säkerheten och dokumentation måste uppdateras.
3. reslutat som ska spara eftersom det anger firmware verision, datum, testperson och utrustning.