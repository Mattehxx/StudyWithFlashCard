
# StudyWithFlashCard

Questa è una web application minimale ed elegante per studiare con le flash cards, sviluppata in Vue 3 + Vite.

## Funzionalità
- Scegli una flash card tra quelle disponibili (configurate in `src/flashcards.json`)
- Scorri tra le flash cards con i pulsanti Precedente/Successiva
- Clicca sulla flash card per ruotarla e vedere la risposta
- Design minimale con colori neutri

## Configurazione delle flash cards
Le domande e risposte sono definite in `src/flashcards.json`:
```json
[
  { "id": 1, "question": "Qual è la capitale d'Italia?", "answer": "Roma" },
  { "id": 2, "question": "Chi ha scritto 'La Divina Commedia'?", "answer": "Dante Alighieri" },
  { "id": 3, "question": "In che anno è iniziata la Seconda Guerra Mondiale?", "answer": "1939" }
]
```

## Avvio del progetto
1. Assicurati di avere Node.js versione >= 22.12.0
2. Installa le dipendenze:
	```sh
	npm install
	```
3. Avvia il server di sviluppo:
	```sh
	npm run dev
	```

## Note
- Il design è pensato per essere semplice e gradevole.
- Puoi aggiungere nuove flash cards modificando il file `src/flashcards.json`.
