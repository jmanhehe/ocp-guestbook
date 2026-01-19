# Log — 15 Jan 2026 to 31 Jan 2026 (150126–310126)

## Table of contents
- [2026-01-15 (150126)](#2026-01-15-150126)
- [2026-01-16 (160126)](#2026-01-16-160126)
- [2026-01-17 (170126)](#2026-01-17-170126)
- [2026-01-18 (180126)](#2026-01-18-180126)
- [2026-01-19 (190126)](#2026-01-19-190126)
- [2026-01-20 (200126)](#2026-01-20-200126)
- [2026-01-21 (210126)](#2026-01-21-210126)
- [2026-01-22 (220126)](#2026-01-22-220126)
- [2026-01-23 (230126)](#2026-01-23-230126)
- [2026-01-24 (240126)](#2026-01-24-240126)
- [2026-01-25 (250126)](#2026-01-25-250126)
- [2026-01-26 (260126)](#2026-01-26-260126)
- [2026-01-27 (270126)](#2026-01-27-270126)
- [2026-01-28 (280126)](#2026-01-28-280126)
- [2026-01-29 (290126)](#2026-01-29-290126)
- [2026-01-30 (300126)](#2026-01-30-300126)
- [2026-01-31 (310126)](#2026-01-31-310126)

---

## 2026-01-15 (150126)
- Summary: Frontend Container
- Tasks:
    - [ ] Sätta upp frontend container och se så det funkar.
- Notes: Det tog lite tid då jag försökte kopiera in config filen vi fick via nginx, eftersom den resolvade en dns på openshift gick det inte i lokal miljö. Att köra med orginal conf från nginx med port 80 gick.

## 2026-01-16 (160126)
- Summary: Backend containers(backend, psql, redis)
- Tasks:
    - [ ] Sätta upp backend container
    - [ ] Sätta upp databas container (psql, postgres)
    - [ ] Sätta upp cache container (redis)
- Notes: Detta var lättare då det inte va något specifikt som blockerade mig - länkar till postgres och redis fick vi av lärare, samt hela backend applikationen. Det som tog tid var att förstå hur man skulle kompilera go för körning i container.

## 2026-01-17 (170126)
- Summary: Se till att kunna köra backend containers (se ovan) och att dom pratar med varann.
- Tasks:
    - [ ] Få healthy när vi kör ```curl localhost:8080/health```
- Notes: Detta fungerade på lite olika sätt. När jag gjorde en compose fil så funkade det som vanligt, men när jag ville starta alla 3 containers separat gick det inte, då var jag tvungen att ändra host från localhost till postgres/redis (namnet på containern) i backend applikationen. Antar att det har något att göra med pods och hur dom fungerar? (compose skapade en pod? och la in alla 4 containers i den, fortfarande oklart hur det funkar). Efter detta fanns det lite mer tid så vi fortsatte att arbeta med frontend kopplingen till våran backend.
- Tasks:
    - [ ] Se till att frontend applikationen kan prata och använda backend.
- Notes: Detta var lite struligare än väntat. Frontend funkade, backend funkade, men inte ihop. Detta tackvare att jag försökte få in nginx.conf vi blev tilldelade av läraren. Detta löste vi med att ändra resolver från openshift till 127.0.0.1, samt expose 8080 på våran frontend containerfile. Efter detta så fungerar allt som det ska. Vi hämtar, postar och läser in stats och posts från våran backend, cachen ger också en checkmark (svårt att veta hur vi ska testa den så antar att det är rätt)

## 2026-01-18 (180126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-19 (190126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-20 (200126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-21 (210126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-22 (220126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-23 (230126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-24 (240126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-25 (250126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-26 (260126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-27 (270126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-28 (280126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-29 (290126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-30 (300126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent:

## 2026-01-31 (310126)
- Summary:  
- Tasks:
    - [ ] 
    - [ ] 
- Notes:  
- Blockers:  
- Time spent: