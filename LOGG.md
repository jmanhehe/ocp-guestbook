# Loggbok för DevOps3 med Jonas Björk

## 2026-01-15 (150126)
- Summary: Frontend Container
- Tasks:
    - Sätta upp frontend container och se så det funkar.
- Notes: Det tog lite tid då jag försökte kopiera in config filen vi fick via nginx, eftersom den resolvade en dns på openshift gick det inte i lokal miljö. Att köra med orginal conf från nginx med port 80 gick.

## 2026-01-16 (160126)
- Summary: Backend containers(backend, psql, redis)
- Tasks:
    - Sätta upp backend container
    - Sätta upp databas container (psql, postgres)
    - Sätta upp cache container (redis)
- Notes: Detta var lättare då det inte va något specifikt som blockerade mig - länkar till postgres och redis fick vi av lärare, samt hela backend applikationen. Det som tog tid var att förstå hur man skulle kompilera go för körning i container.

## 2026-01-17 (170126)
- Summary: Se till att kunna köra backend containers (se ovan) och att dom pratar med varann.
- Tasks:
    - Få healthy när vi kör ```curl localhost:8080/health```
- Notes: Detta fungerade på lite olika sätt. När jag gjorde en compose fil så funkade det som vanligt, men när jag ville starta alla 3 containers separat gick det inte, då var jag tvungen att ändra host från localhost till postgres/redis (namnet på containern) i backend applikationen. Antar att det har något att göra med pods och hur dom fungerar? (compose skapade en pod? och la in alla 4 containers i den, fortfarande oklart hur det funkar). Efter detta fanns det lite mer tid så vi fortsatte att arbeta med frontend kopplingen till våran backend.
- Tasks:
    - Se till att frontend applikationen kan prata och använda backend.
- Notes: Detta var lite struligare än väntat. Frontend funkade, backend funkade, men inte ihop. Detta tackvare att jag försökte få in nginx.conf vi blev tilldelade av läraren. Detta löste vi med att ändra resolver från openshift till 127.0.0.1, samt expose 8080 på våran frontend containerfile. Efter detta så fungerar allt som det ska. Vi hämtar, postar och läser in stats och posts från våran backend, cachen ger också en checkmark (svårt att veta hur vi ska testa den så antar att det är rätt)

## 2026-01-18 (180126)
- Summary: Söndag.
- Notes: Detta är kommand vi använt för att starta våra tjänster. Se till att cda in i rätt map där containerfiler ligger.
```
podman run -d -p 3000:8080 --name frontend --network guestbook-net frontend  
podman run -d -p 8080:8080 --name backend --network guestbook-net backend  
podman run -d -p 5432:5432 --name postgres --network guestbook-net postgres  
podman run -d -p 6379:6379 --name redis --network guestbook-net redis
```

## 2026-01-19 (190126)
- Summary: Skrivit loggbok och diskuterat vad vi gjort förra veckan tors,fre samt i helgen när vi arbetat.
- Tasks:
    - Fylla i loggbok för arbetet
- Notes: Vi har även diskuterat hur vi kan ta tillbaka localhost som host för DB_HOST och REDIS_HOST i våran backend. Detta kanske inte går men vi ska testa att se om det funkar, på så sätt spelar det ingen roll vad vi döper våra containers till utan den går på localhost:port om det nu funkar som vi tänker att det ska göra. Jag har också byggt en compose fil för att se om den beter sig annorlunda jämfört med när vi startar alla separat. Detta behövs inte och kommer inte användas men jag är nyfiken på hur det blir. Även läst lite om podman kube play och tänkte kanske testa att använda det för att se hur det funkar.

## 2026-01-20 (200126)
- Summary: Lektion och genomgång med lärare.
- Tasks:
    - Skapa workflow som bygger våran frontend image.
    - Skapa workflow som bygger våran backend image.
- Notes: Idag har jag sett till att få mitt workflow för att bygga min frontend image och generera en länk till ghcr, githubs container registry. Jag valde att använda docker i mitt workflow för att bygga medans Nasir som jag arbetade med valde att testa att utnyttja podman som vi använt lokalt. De flesta på internet föredrog docker då det är inbyggt i github workflow medans podman som Nasir valde att använda måste installeras separat i workflowet för att det ska fungera, båda har för och nackdelar och det var kul att se hur dom olika fungerade i en verklig miljö. Tyvärr hann jag inte bygga färdigt backend delen då jag valde att göra en lite mer "avancerad" workflow så detta arbete fortsatte dagen efter.

## 2026-01-21 (210126)
- Summary: Bygga backend workflow
- Tasks:
    - Skapa workflow för backend image
- Notes: Hann inte med backend på tisdagen så det fick bli onsdagens task, planering och tankar med Nasir i skolan med hjälp av att rita på tavlan det vi trodde vi skulle uppnå. Då jag sitter på MacOS som inte kör amd64 image så valde jag att göra så mitt workflow kan bygga både amd64(linux) och arm64(macos), detta gjorde jag via att ha en specifik del i mitt workflow som kollar om det startade via en dispatch eller inte, om jag vill bygga en ny backend image och testa den lokalt innan jag mergar till main för produktions miljö så startar jag den via en dispatch inne på github, detta genererade en -dev länk/tag till min image och lät mig testa min image lokalt på min mac, var jag nöjd med hur det funkade så mergade jag till main och då startade workflowet fast den byggde för amd64(linux).  
Detta är ett steg jag blev väldigt nöjd med hur jag lyckades lösa då arm64 image tog nästan 6-8min att köra och bygga medans amd64 tog knappt 1 minut, detta är viktig tid i ett riktigt projekt där tid och pengar är en dyr resurs. Med detta nya smidiga workflow så var jag riktigt nöjd med att jag och Nasir lyckats lösa det på ett bra sätt. Tummen upp till både mig och Nasir.

## 2026-01-22 (220126)
- Summary: Lektion med genomgång av openshift och uppsättning av redhat sandbox
- Notes: Generell genomgång med lärare om openshift och hur det ser ut och fungerar i riktig miljö.

## 2026-01-27 (270126)
- Summary: Tisdag, distanslektion med exempel.
- Tasks:
    - Se till att skriva manifest som fungerar med våra images vi byggt via workflow
- Notes: Tisdagen hade vi lektion, lärare gick då igenom hur manifest för openshift ser ut och hur man skriver dom, efter lektion så skrev jag egna manifest med hjälp av det läraren visat och såg till att mina manifest använde rätt images(de jag fått via workflow)

## 2026-01-28 (280126)
- Summary: Openshift sandbox med manifest som lärare visat dagen innan.
- Tasks:
    - Sätta upp deploy struktur i sandbox miljö
- Notes: Under onsdagen så testade jag att deploya mina manifest till min sandbox, detta gick faktiskt utan problem tack vare lärarens genomgång dagen innan som var väldigt bra och nogrann.

## 2026-01-29 (290126)
- Summary: Lektion och genomgång med lärare. Nytt repo för infrastruktur kopplat till ArgoCD
- Tasks:
    - Bygga nytt repo med infrastruktur för ArgoCD
- Notes: Torsdagen så fick vi i uppgift att sätta upp nya repon för infrastruktur. Jag hann inte så mycket mer än att skapa repo och se till att rätt filer fanns där då jag kände mig dålig. Hem efter lunch pga sjukdom.

## 2026-01-30 (300126)
- Summary: Fredag, börjar bli sjuk.
- Tasks:
    - Få upp automatisk synk på ArgoCD via infra repo.
- Notes: Fick inte mycket gjort i mitt eget projekt men hjälpte Nasir en stund med felsökning då hans ArgoCD projekt inte hittade imagen han ville. Detta tog ett tag att felsöka men vi löste problemet när vi insåg att han inte hade rätt image länkat i Infra repot.

## 2026-01-31 (310126)
- Summary: Lördag, fortfarande sjuk 
- Tasks:
    - Hjälpte Alma tillsammans med Nasir över discord
- Notes: Hjälpte så gott jag kunde i någon timme, fortfarande sjuk.

## 2026-02-01 (010226)
- Summary: Sjuk, men ville bli färdig med ArgoCD delen.
- Tasks:
    - Sätta upp ArgoCD för nya repot
- Notes: Fick hjälp med hur systemet skulle funka av Alma och Nasir via discord, satte upp det sista som behövdes för att få ArgoCD att automatiskt uppdatera beroende på image i Infra repo.

## 2026-02-02 (020226)
- Summary: Sjuk hela denna veckan
- Notes: Hjälpte Nasir med sitt backend workflow för att optimisera hur och när den bygger för att spara tid.

## 2026-02-03 (030226)
- Summary: Sjuk resten av kursen tyvärr. Missade både tisdags och torsdags-lektionen.