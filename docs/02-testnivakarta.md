# Testnivåkarta CityBike

## T1
Nivå: enhet
Motivering: PriceCalculator testas ensam med en resetid in och ett pris ut, fråga 4 gäller

## T2
Nivå: enhet
Motivering: det är samma klass om i T1 och taket i P3 kontrollers utan nätverk och databas, fråga 4 gäller

## T3
Nivå: integration
Motivering: API körs i testserver mot en riktig sql databas så flera delar samverkar, men de är inte hela kedja i en driftlik miljö, fråga 3 gäller

## T4
Nivå: enhet
Motivering: upplåsningsklienten är ersatt med testdubbel så bookingservice testas enskilt, fråga 4 gäller

## T5
Nivå: system
Motivering: kedjan går från kundappen via API till en simulerad styrenhet alltså genom flera systemdelar och ingen användare godkänner så fråga 2 gäller

## T6
Nivå: acceptans
Motivering: Projektledaren godkänner resultatet efter kunderna testat så fråga 1 gäller

## T7
Nivå: integration
Motivering: repot skriver och läser mot en rikigt sql databas så fråga 3 gäller

## T8
Nivå: system
Motivering: kartflödet belastas med 500 använder i en driftlik testmiljö och resultatet bedöms möt ett mått inte en användare så fråga 2 gäller

## T9
Nivå: enhet
Motivering: datumet skickas som parameter så agevalidator kan testas utan klocka databas och nätverk, så fråga 4 gäller

## T10
Nivå: acceptans
Motivering: det är den ekonomiansvarige som avgär om kvittot är godkänd, fråga 1 gäller

## T11
Nivå: integration
Motivering: anropet går genom en riktig http-stack i samma process där behörighetskontroll och routing samverkar utan resterande delar, fråga 3 gäller

## T12
Nivå: system
Motivering: resflödet från registrering till betalning körs genom alla systemdelar i testmiljön, fråga 2 gäller

## T13
Nivå: enhet
Motivering: emailvalidator kontrollerar enbart en textsträng utan andra beroende, fråga 4 gäller

## T14
Nivå: acceptans
Motivering: kundtjänst är användare av adminpanelen och skriver protokoll, fråga 1 gäller

## T15
Nivå: integration
Motivering: stationserviuce och databasen testats tillsammans för att kolla antalet lediga cyklar blir korrekt, fråga 3 gäller

## T16
Nivå: system
Motivering: uppdateringen går genom firmware styrenhet mobilnät och API i testtrigg som är lik driftmiljön, resultatet kontrolleras utan godkännande av användare så fråga 2 gäller

## Sammanställning
Enhet: 5
Integration: 4
System: 4
Acceptans: 3

jämnare än pyramiden, i ett riktigt projekt borde vi ha fler enhetstester än tester på högre nivåer.

## Eget testfall
Krav: Krav 3: Safety i docs/01-kvalitetsanalys.md
Givet: en styrenhet i testriggen som laddar, normal temperatur
När:  temperaturen i sensorn höjs över 60 grader
Då:  laddningen ska brytas och larm syns i adminpanel inom 5 sekunder
Nivå: system
Testtyp: icke-funktionellt, svartlåda

## Kontrollfrågor
1. Felet hittas billigast på enhetsnivån då det ligger i prisberäkningen och T1 ligger närmast att fånga det pågrund av att det testar pricecalculator med en vanlig resa. men det behövs ett till fall med 61 sekunder som kontrollerar att påbörjade minuyter avrundas uppåt
2. T11 var svårast att placera eftersom jag tvekade mellan enhet och integration, testet startar inte resten av systemet men går ändå genom en riktig http-stack
