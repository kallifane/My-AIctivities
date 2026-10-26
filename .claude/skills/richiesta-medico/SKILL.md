---
name: richiesta-medico
description: Prepara l'email al medico di base per richiedere ricette, rinnovi o prescrizioni di farmaci. Usa questa skill ogni volta che l'utente dice cose come "devo chiedere la ricetta al medico", "scrivi al dottore per le medicine", "rinnovo ricetta", "mi servono le impegnative/farmaci", "finisco le pillole", o simili. Produce un'email in italiano, formale e concisa, pronta da inviare.
---

# Richiesta farmaci al medico

Genera l'email per chiedere al medico una ricetta (nuova o di rinnovo) per i farmaci dell'utente. Solo per l'utente stesso, canale email, italiano cordiale e formale.

## Profilo (da compilare una volta)

Se i campi sotto sono vuoti, chiedili all'utente con `AskUserQuestion` alla prima richiesta e proponi di salvarli qui.

- Nome e cognome:
- Codice fiscale (opzionale, solo se il medico lo richiede):
- Nome del medico / forma di cortesia (es. "Dottor Rossi", "Dottoressa Bianchi"):
- Farmaci abituali (nome, dosaggio, posologia come da ricetta precedente):

## Flusso

1. Capisci cosa serve: quali farmaci (anche solo "i soliti"), se è un rinnovo o una prima richiesta, e quando finiscono le scorte.
2. Se manca un dato indispensabile (nome del farmaco o dosaggio), chiedilo. Non inventare mai nomi, dosaggi o posologie: usa solo ciò che l'utente o il profilo indicano.
3. Scrivi l'email.
4. Consegna solo l'email, senza commenti. Aggiungi una riga solo se manca un dato da verificare.

## Struttura dell'email

- **Oggetto**: breve e chiaro. Es. `Richiesta ricetta – [Nome Cognome]`
- **Saluto**: `Buongiorno Dottor/Dottoressa [Cognome],`
- **Corpo** (3–5 righe):
  - chi sei e cosa chiedi (rinnovo/nuova ricetta);
  - elenco puntato dei farmaci con dosaggio e posologia;
  - urgenza, se c'è (es. "le scorte terminano il [data]");
  - come preferisci ricevere la ricetta (NRE via email/SMS/ritiro in studio), se indicato.
- **Chiusura**: `La ringrazio per la disponibilità. Cordiali saluti,` + nome e cognome.

## Regole

- Tono formale ma diretto, niente giri di parole.
- Una sola richiesta per email; se i farmaci sono più di uno, elencali tutti insieme.
- Non dare consigli medici, non suggerire farmaci o variazioni di dosaggio. Se l'utente riferisce sintomi nuovi o effetti collaterali, includili come informazione da riportare al medico, senza interpretarli.
- Se l'utente dice che le scorte stanno per finire in pochi giorni, segnala l'urgenza nell'oggetto e nel corpo.

## Esempio

**Oggetto**: Richiesta rinnovo ricetta – Mario Rossi

Buongiorno Dottoressa Bianchi,

le scrivo per chiederle il rinnovo della ricetta per i seguenti farmaci:

- [Farmaco A] [dosaggio], [posologia]
- [Farmaco B] [dosaggio], [posologia]

Le scorte terminano indicativamente il [data]. Mi sarebbe gradito ricevere il numero di ricetta elettronica via email.

La ringrazio per la disponibilità.
Cordiali saluti,
Mario Rossi
