#  HMI Bottling & Loading Simulation


Proiectul simulează, într-un mediu **SCADA/HMI (Siemens SIMATIC WinCC Runtime Advanced)**, întregul flux al unui proces industrial de îmbuteliere: de la accesul controlat în fabrică, prin umplerea și ambalarea sticlelor, până la încărcarea lăzilor în TIR și expedierea acestora. Simularea folosește **tag-uri** pentru a controla mișcarea și vizibilitatea obiectelor pe ecran, **butoane** de interacțiune și **bare de progres** pentru vizualizarea umplerii sticlelor, alături de un sistem de **alarme** care marchează începutul fiecărei etape a procesului.

---

##  Autentificare & Niveluri de acces

Accesul la comenzile sistemului este controlat printr-un ecran de **Login**, cu 4 roluri de utilizator, fiecare cu drepturi diferite asupra butoanelor din interfață:

| Rol | Acces |
|---|---|
| **Civil** | Niciun acces la butoane (doar vizualizare) |
| **Practicant** | Acces doar la butonul de intrare în fabrică (ușa fabricii) |
| **Muncitor** | Acces la toate butoanele, **cu excepția** butonului de start al procesului de îmbuteliere |
| **Inginer** | Acces complet la toate butoanele, inclusiv startul procesului de îmbuteliere |

<p align="center">
  <img width="500" alt="Ecran de login SCADA" src="partea de user pentru a accesa comenzile.png" />
</p>

**Butoanele disponibile în interfață:**

- Buton de schimbare a vremii (norul) — element pur vizual, fără rol funcțional în simulare
- Buton de intrare în fabrică (ușa fabricii)
- Buton de închidere a cutiei (lada de ambalare)
- Butoane **START / STOP** — pornesc/opresc procesul de îmbuteliere
- Ușa din centrul stației de îmbuteliere — trimite către zona din spatele fabricii, unde sticlele sunt încărcate în TIR
- TIR-ul — la apăsare, pleacă de la fabrică spre aprovizionare

---

##  Ecranele simulării

### 1 Exteriorul fabricii

Ecranul de intrare, cu fabrica văzută din exterior. Include butonul de schimbare a vremii (element vizual) și butonul de acces (ușa fabricii), controlat de nivelul de acces al utilizatorului logat.

<p align="center">
  <img width="420" alt="Fabrica - vreme insorita" src="Poza afara insorit.png" />
  &nbsp;&nbsp;
  <img width="420" alt="Fabrica - vreme ploioasa" src="poza afara ploios.png" />
</p>

<p align="center">
  <em>Stânga → dreapta: variantă însorită · variantă ploioasă (schimbare vizuală, fără impact asupra procesului)</em>
</p>

### 2 Interiorul fabricii — Stația de îmbuteliere

Ecranul central al simulării. Aici are loc procesul complet de îmbuteliere: sticla goală avansează pe bandă, este umplută prin intermediul unui piston/dozator (simulat printr-o bară de progres a nivelului de lichid), apoi continuă spre zona de ambalare în cutie.

<p align="center">
  <img width="500" alt="Statia de imbuteliere - stare initiala" src="interiorul fabricii.png" />
</p>

**Secvența procesului de umplere:**

<p align="center">
  <img width="300" alt="Banda a pornit" src="banda a pornit.png" />
  &nbsp;&nbsp;
  <img width="300" alt="Sticla se umple" src="sticla se umple.png" />
  &nbsp;&nbsp;
  <img width="300" alt="Sticla umpluta merge in cutie" src="sticla umpluta merge in cutie.png" />
</p>

<p align="center">
  <em>Stânga → dreapta: pornirea benzii transportoare · umplerea sticlei (bară de progres) · sticla umplută avansează către cutie</em>
</p>

###  Panoul de alarme

Sistemul afișează alarme (*Unacknowledged alarms*) care marchează, cu timestamp, momentul declanșării fiecărei etape a procesului (ex. pornirea benzii, umplerea sticlei, plecarea TIR-ului), oferind trasabilitate completă asupra secvenței de evenimente.

<p align="center">
  <img width="500" alt="Panou de alarme" src="alarme.png" />
</p>

### 3 Spatele fabricii — Încărcarea în TIR

Ultimul ecran al fluxului: lăzile cu sticle ambalate sunt preluate cu un stivuitor și încărcate în TIR, care apoi pleacă spre aprovizionare la apăsarea butonului dedicat.

<p align="center">
  <img width="420" alt="Cutia se incarca in tir" src="cutia se incarca in tir.png" />
  &nbsp;&nbsp;
  <img width="420" alt="Tirul a plecat" src="tirul a plecat.png" />
</p>

<p align="center">
  <em>Stânga → dreapta: încărcarea cutiei în TIR · TIR-ul plecat spre aprovizionare</em>
</p>

---

##  Elemente tehnice folosite

- **Tag-uri SCADA** pentru controlul mișcării (*movement*) și vizibilității (*visibility*) obiectelor de pe ecran
- **Butoane** de interacțiune, cu drepturi diferențiate pe roluri de utilizator
- **Bare de progres** pentru simularea vizuală a umplerii sticlelor
- **Sistem de alarme** cu istoric de evenimente și marcaje temporale
- **3 ecrane** interconectate, reprezentând fluxul complet al procesului industrial
