---
name: richiesta-medico
description: Gestisce le richieste di farmaci al medico di base: scrive l'email per ricette/rinnovi e registra le scatole ritirate per tenere aggiornate le scorte. Usa questa skill ogni volta che l'utente dice cose come "devo chiedere la ricetta al medico", "scrivi al dottore per le medicine", "rinnovo ricetta", "finisco le pillole", "ho ritirato le medicine", "il medico mi ha dato N scatole", o simili. Email in italiano, formale e concisa, pronta da inviare.
---

# Richiesta farmaci al medico

Due modalità, solo per l'utente stesso, canale email, italiano cordiale e formale:

- **Richiesta**: scrive l'email al medico per una ricetta (nuova o di rinnovo).
- **Ritiro**: registra quante scatole l'utente ha ritirato, per aggiornare le scorte.

Lo stato delle scorte sta in `scorte.md` (stessa cartella di questa skill). Leggilo a ogni uso e aggiornalo a ogni ritiro.

## Profilo (da compilare una volta)

Se i campi sono vuoti, chiedili con `AskUserQuestion` alla prima richiesta e proponi di salvarli qui.

- Nome e cognome:
- Codice fiscale (opzionale, solo se il medico lo richiede):
- Nome del medico / forma di cortesia (es. "Dottor Rossi", "Dottoressa Bianchi"):
- Farmaci abituali (nome, dosaggio, posologia come da ricetta precedente, contenuto di una scatola es. "28 compresse"):
- Anticipo minimo di richiesta: 2 giorni lavorativi prima della fine delle scorte (aumentalo se il medico ha tempi più lunghi)

## Modalità Richiesta

1. Capisci cosa serve: quali farmaci (anche solo "i soliti") e se è un rinnovo o una prima richiesta.
2. Se manca un dato indispensabile (nome del farmaco, dosaggio, posologia), chiedilo. Non inventare mai nomi, dosaggi, posologie o quantità.
3. Calcola la data di fine scorta da `scorte.md`: (unità rimaste) ÷ (unità al giorno da posologia). Se l'utente indica già la data, usala.
4. Verifica l'anticipo: la richiesta deve partire **almeno 2 giorni lavorativi prima** della fine scorta. Indica la data limite per inviare l'email. Se sei già dentro la soglia, segnala l'urgenza (oggetto e corpo) e avvisa l'utente in una riga.
5. Scrivi l'email **senza indicare il numero di scatole**: lo decide il medico.
6. Consegna solo l'email, senza commenti. Aggiungi una riga solo se manca un dato o se la soglia dei 2 giorni è superata.

## Modalità Ritiro

Quando l'utente dice di aver ritirato i farmaci:

1. Chiedi (se non detto) quante scatole di ciascun farmaco ha ricevuto e la data di ritiro.
2. Aggiorna `scorte.md`: unità totali = scatole × contenuto della scatola, sommate alle unità rimaste.
3. Ricalcola e comunica in una riga la nuova data di fine scorta e la data limite per la prossima richiesta.

## Struttura dell'email

- **Oggetto**: breve e chiaro. Es. `Richiesta ricetta – [Nome Cognome]`
- **Saluto**: `Buongiorno Dottor/Dottoressa [Cognome],`
- **Corpo** (3–5 righe):
  - chi sei e cosa chiedi (rinnovo/nuova ricetta);
  - elenco puntato dei farmaci con dosaggio e posologia (nessuna quantità di scatole);
  - data di fine scorta (es. "le scorte terminano il [data]");
  - come preferisci ricevere la ricetta (NRE via email/SMS/ritiro in studio), se indicato.
- **Chiusura**: `La ringrazio per la disponibilità. Cordiali saluti,` + nome e cognome.

## Regole

- Tono formale ma diretto, niente giri di parole.
- Una sola richiesta per email; più farmaci, un unico elenco.
- Non dare consigli medici, non suggerire farmaci o variazioni di dosaggio. Sintomi nuovi o effetti collaterali riferiti dall'utente vanno riportati al medico così come sono, senza interpretarli.
- Mai cancellare lo storico in `scorte.md`: aggiungi righe, non sovrascrivere.

## Esempio di email

**Oggetto**: Richiesta rinnovo ricetta – Mario Rossi

Buongiorno Dottoressa Bianchi,

le scrivo per chiederle il rinnovo della ricetta per i seguenti farmaci:

- [Farmaco A] [dosaggio], [posologia]
- [Farmaco B] [dosaggio], [posologia]

Le scorte terminano indicativamente il [data]. Mi sarebbe gradito ricevere il numero di ricetta elettronica via email.

La ringrazio per la disponibilità.
Cordiali saluti,
Mario Rossi
