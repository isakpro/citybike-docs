# GDPR-avvikelser i CityBike

## Personuppgiftsinventering
- Users: Name, Personnummer, Email, Phone, PasswordHash, Status, CreatedAt. Namn, personnummer, eposrt och telefon är direkta identifierade och resten hör till en känd person
- PaymentMethods: UserId, ProviderToken, CardLast4, ExpiryMonth, ExpiryYear. kortuppgifter som är kopplade till en personn via UserId
- Bikes: inga personuppgifter. tabellen beskriver endast cykeln och inga kopplingar till en person
- Stations: inga personuppgifter. i tabellen finns det endast platser och kapacitet
- Trips: UserId, StartStationId, EndStationId, StartedAt, EndedAt, PriceSek. det visar vart och när en person har rest
- GpsPoints: TripId, Latitude, Longitude, RecordedAt. de kopplas till en person via TripId och visar exakta position varje 15 sekund.

## A1
Rutin: R1
Vad: Personnummer krävs vid registrering trots att syftet kan nås på annat sätt.
Artikel: Art. 5.1 c, dataskyddslagen 3 kap. 10 §
Risk: Hög
Åtgärd: Ta bort kravet. Kontrollera ålder på annat sätt eller ta bara emot födelsedatum.
Testfall: Registrering utan personnummer ska fungera (systemtest).

## A2
Rutin: R2
Vad: resor och position sparas utan något slut datum vilket kommer ge ca 44 miljoner positioner per säsong som inte behövs efter att resan blivit betaltd
Artikel: Art. 5.1 e
Risk: Hög
Åtgärd: rensa GpsPoints automatiskt efter 30 dagar och spara istället Trips den tid bokföringslagen gäller och skippa position
Testfall: efter automatiska rensningen så ska inga positioner äldre än 30 dagar finnas kvar

## A3
Rutin: R3
Vad: Om en kund vill stänga sitt konto så blir det bara inactive vilket betyder att alla personuppgifter fortfarande finns kvar
Artikel: Art. 17, Art 5.1 e
Risk: Medel
Åtgärd: Radera personuppgifter och behåll endast det som bokföringen kräver
Testfall: när ett konto stängs av så ska personuppgifterna försvinna

## A4
Rutin: R4
Vad: alla i kundtjänst delar ett konto och lösenordet ligger i chatten och man ser allt så det går ej att avgöra vem som gjort vad
Artikel: Art. 32, Art 5.1 f, Art. 25
Risk: Hög
Åtgärd: Gör personliga konton med mer säkerthet som två faktorisering och roller så man bara ser de uppgifter som behövs och inte allt.
Testfall: gör test med en ny kundtjänstroll som inte ser all information och endast det som rör den personen och deras ärenden

## A5
Rutin: R5
Vad: API loggar hela innehållet i varje anrop 12 månader och då hamnar personnummer och lösenord i loggfiler
Artikel: Art. 5.1 c, Art. 5.1 e, Art. 32
Risk: Hög
Åtgärd: Logga inget innehåll i anropen och korta även lagringsperioden till 30 dagar
Testfall: efter registeranrop så ska inte personuppgifterna hamna i loggfiler

## A6
Rutin: R6
Vad: alla kunder får nyhetsbrev och har ej fått frågan om de vill eller ej, ingen rättslig grund
Artikel: Art. 6.1, Art. 21, marknadsföringslagen 19 §
Risk: Låg
Åtgärd: Gör så det kommer en ruta när man skapar konto så kunden får välja om hen vill få nyhetsbrev eller ej
Testfall: Ett test där en kund kryssar i att de ej vill ha och då ska ej nyhetsbreve komma upp

## A7
Rutin: R7
Vad: analysverktyget får id, epost och resor utan avalt och det lagras i USA även så behövs ej eposten får statistik
Artikel: Art. 28, Art. 44-46, Art. 5.1 c
Risk: Hög
Åtgärd: Tecka personppgiftsbitrödesavatl och kontrollera så att leverantören har certifikat enlig eu-us data privacy framework och att det skickas anonymt id istället för epost
Testfall: all data som skickas till analysverktyget ska ej innehålla epost längre

## A8
Rutin: R8
Vad: ingen förteckning över behandlingar och ingen konsekvensbedöming, även fast platsdata behandlas
Artikel: Art. 30, Art. 35
Risk: Medel
Åtgärd: skaffa en förteckning äver behandlingarna och en konsekvensbedöming för gps data
Testfall: granska att det finns en förteckning och bedömning, ett såkallat acceptanstest

## A9
Rutin: R8
Vad: Inget står om hur personuppgifter behandlas för kunden
Artikel: Art. 12, Art. 13
Risk: Medel
Åtgärd: Skapa en intergritetspolicy och den måste visas vid skapandet av konto
Testfall: när man skapar konto ska det finnas länk till integritetspolicy

## A10
Rutin: R11
Vad: Lösenord hash utan salt med SHA-256
Artikel: Art. 32
Risk: Hög
Åtgärd: byt till en hashfunktion med salt som Argon2
Testfall: två users med samma lösenord får olika i PasswordHash

## R9
Rutin: R9
Bedöming: det är i ordning, säkerhetskopior används för att återställa lösenord och även 90 dagar ör en rimlig tid. det borde dock framgå till kunderna att raderade uppgifter stannar kvar ett tag.

## Incident R10
Tidpunkt för kännedom: tisdag 3 mars 2026 14:20
Frist för anmälan (datum och klockslag): Fredag 6 mars 14:20 
Anmäla till IMY: Ja
Informera berörda kunder: Nej
Motivering: namn, epost och telefonnummer för 2100 kunder har skickats till ett externt företag och vi kan inte vara säkra på att filen raderas så det ör oklart om risken är osannolik eftersom dessa uppgifter kan användas för phising så det ska anmälas enligt Art. 33. Men eftersom inga personnummer, lösn eller kortuppgifter är läckta så är det bara medel alvarlighetsgrad.
Åtgärder för att förhindra upprepning: be mottagaren radera filen och bekräfta det, exporter behöver inte innehålla telefonnummer de ska bara innehålla det som krävs. personuppgifter ska ej skickas via epost utan i ett system som kräver behörighet. epost ska varana när det skickas till en extern adress.
