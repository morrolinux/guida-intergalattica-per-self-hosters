# Checklist self-hosting


### Prima di considerarlo "in produzione"

- **Produzione** = il momento in cui qualcun altro dipende da questo servizio.

- Non serve spuntare tutto oggi. Serve sapere **cosa non hai ancora spuntato**

- L'ordine conta: i livelli sono pensati per essere affrontati in sequenza.

> Se qualche voce ti è oscura, [in fondo](#risorse) trovi da dove partire.



## Livello 0 - il minimo indispensabile (con debito tecnico)
- [ ] So **quali dati non posso rigenerare** (foto, documenti, database) e dove stanno fisicamente
- [ ] Ho un **backup automatico** di quei dati, che parte da solo
- [ ] Il backup va su un **disco diverso** da quello dove stanno i dati originali
- [ ] Le password di default sono cambiate **ovunque**, incluso il servizio "tanto è interno"
- [ ] So **come si riaccende tutto** se il server si spegne o si riavvia

---

## Livello 1 - un po' meno debito tecnico
- [ ] **Ho ripristinato un backup per davvero**, almeno una volta.
- [ ] Il backup ha una **copia fuori casa**, cifrata
- [ ] Ricevo un **alert se l'ultimo backup riuscito è più vecchio di N ore**
- [ ] L'accesso da fuori passa da **VPN**, oppure da un reverse proxy con HTTPS e **autenticazione seria** davanti
- [ ] So **chi aggiorna cosa e quando** (anche se la risposta è "io, il primo sabato del mese")
- [ ] Quello che è esposto a Internet (tipicamente solo la VPN) è **sempre aggiornato**
- [ ] Ho scritto da qualche parte **cosa gira dove e come si rimette in piedi**


---

## Livello 2 - Prima di fidarti davvero

- [ ] La configurazione è **in git** (compose file, script; i segreti cifrati o esclusi)
- [ ] **Monitoring attivo e passivo** con notifiche sul telefono (es: Uptime Kuma)
- [ ] **SMART attivo** sui dischi, con alert
- [ ] **Scrub o check periodico** dell'array o del filesystem
- [ ] **Dominio mio + certificati validi**, anche per i servizi raggiungibili solo da VPN (sfida DNS-01)
- [ ] Ho un **UPS**, se vivo in una zona con blackout o ho un array che non ama gli spegnimenti bruschi
- [ ] I servizi più sensibili sono **isolati** dal resto della rete di casa
- [ ] Ho un **ambiente dove rompere le cose** senza toccare quello che usa la famiglia

---

## Manutenzione ricorrente

Da calendarizzare

**Ogni mese**
- [ ] Do un'occhiata agli alert ignorati e allo spazio disco rimasto
- [ ] Applico gli aggiornamenti che ho rimandato

**Ogni tre mesi**
- [ ] **Ripristino un backup a caso** in ambiente temporaneo e controllo che funzioni.
- [ ] Controllo lo stato SMART dei dischi

**Ogni anno**
- [ ] Provo un **restore completo** su hardware diverso, o almeno su una VM
- [ ] Rileggo questa checklist e guardo cosa è scaduto
- [ ] Verifico che la "busta" del bus factor sia ancora aggiornata *(vedi sotto)*

---

## Le tre domande finali

Se rispondi "non lo so" a una di queste, hai trovato il tuo prossimo weekend.

1. Se stanotte il server prende fuoco, cosa perdo **esattamente?**
2. **Se il backup si fosse rotto tre settimane fa, come lo saprei?**
3. **Se domani mi investe un tram, qualcuno recupera le foto di famiglia?**
   Serve una busta - fisica o digitale - con: dove sono i dati, come si decifrano, e la password del password manager. Consegnata a una persona reale.

---

## Anti-pattern comuni da evitare
| Anti-pattern | Perché fa male |
|---|---|
| **"Ho il RAID, sono a posto"** | Il RAID ti protegge da un disco che muore. Non da `rm -rf`, non da un ransomware, non da un errore applicativo, non da te. |
| **"Il backup non dà errori"** | Un backup che non parte non dà errori. Monitora l'età, non i fallimenti. |
| **"Tanto è replicato"** | La ridondanza è anche un anestetico: se il servizio continua a funzionare con un nodo rotto, non c'è urgenza, e i giorni passano. |
| **"Lo ripristino se serve"** | Un backup mai ripristinato non è un backup, è una speranza. Il primo restore non farlo in emergenza. |
| **"È interno, non serve la password"** | Il tuo laptop compromesso e la telecamera IoT sulla stessa LAN sono già oltre il perimetro. |
| **"Aggiorno quando ho tempo"** | Il debito di aggiornamento si paga a interessi: due anni di ritardo e l'upgrade diventa un progetto del weekend. |

---

## Il punto di partenza

Se stai leggendo e non hai ancora fatto niente:

- Un disco esterno. 
- `restic` che ci scrive ogni notte. 
- Un ping a Uptime Kuma quando finisce.

**Un'ora di lavoro, e hai già superato il 90% degli homelab amatoriali.**

Il resto viene dopo.

---

## Risorse

### In cerca di ispirazione?

Dai un'occhiata a [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted).

### Ti manca qualche pezzo?

È normale, dietro ogni spunta c'è una competenza.  
Questi sono i miei corsi per costruirla:

- **[Linux](https://corsolinux.com/linux)**: le fondamenta
- **[Reti](https://corsoreti.it)**: IP, NAT e come parlano le macchine
- **[Docker](https://corsolinux.com/docker)**: servizi e compose
- **[Proxmox](https://corsolinux.com/proxmox)**: virtualizzazione e laboratorio
- **[Kubernetes](https://corsolinux.com/kubernetes)**: quando un server non basta
