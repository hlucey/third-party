---

 
copyright:

  years: 2017, 2018

lastupdated: "2018-09-05" 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Inoltro dell'utilizzo per i piani a consumo
{: #submitusage}

Devi inoltrare l'utilizzo per tutte le istanze del servizio attivo ogni ora. La mancata notifica dell'utilizzo può portare alla perdita della raccolta di ricavi per IBM, che può causare una perdita della quota di ricavi per i provider di offerte.
{:shortdesc}

## Come funziona il processo
{: #process-flow}

I seguenti passi descrivono il processo per l'inoltro dell'utilizzo:

1. Inoltra una verifica dell'utilizzo iniziale tramite lo strumento API REST Usage Submission per convalidare che i tuoi piani a consumo siano configurati correttamente.
2. Automatizza l'inoltro orario continuo allo strumento API REST Usage Submission per ogni piano a consumo. Puoi ospitare questi inoltri automatizzati dovunque tu voglia, a condizione che sia supportato SSO standard.
2. I record di utilizzo sono aggregati in base al modello di misurazione e la quantità totale viene visualizzata nel Dashboard di utilizzo nella console {{site.data.keyword.Bluemix_notm}}.
3. Viene utilizzata la quantità unitaria aggregata dal processo di misurazione, viene applicato il costo e viene calcolato l'importo dovuto dall'utente per l'istanza del servizio.
4. Alla fine del mese, il costo calcolato finale è l'importo generato per l'utente.

## Prerequisiti
{: #prereqs}

Riesamina i seguenti prerequisiti per abilitare la misurazione per il tuo servizio:

* Il catalogo dei prezzi viene aggiornato con i prezzi per tutte le metriche addebitabili nei piani della risorsa.
* Le definizioni di misurazione e valutazione per tutti i piani nella risorsa vengono verificati e ne viene eseguito l'onboarding.

## Linee guida per l'inoltro dell'utilizzo 
{: #metering_guidelines}

### Linee guida per l'inoltro
{: #submission-guidelines}

Fai riferimento alle seguenti linee guida quando utilizzi il servizio di misurazione {{site.data.keyword.Bluemix_notm}} per inoltrare i dati di utilizzo delle risorse:

* L'ora di inizio e l'ora di fine rappresentano l'intervallo di tempo durante il quale le misure sono state raccolte. Le ore non dipendono dall'ora in cui il record di utilizzo viene inoltrato alle API di misurazione.
* I record di utilizzo sono fatti. Non aggiornare il record di utilizzo dopo averlo creato. Un'ubicazione viene specificata quando crei correttamente un record di utilizzo. Se viene restituito un codice di errore, vedi le [azioni](#actions) che potresti dover eseguire.
* Un record di utilizzo viene identificato in modo univoco dalla firma `account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end`. Quando un record di utilizzo viene elaborato, qualsiasi altro record di utilizzo con la stessa firma viene rifiutato come un duplicato.
* Non combinare l'interazione con il servizio di misurazione con altri servizi. Le richieste devono essere gestite singolarmente anche se la misurazione inizia e termina con il provisioning e l'annullamento del provisioning dell'istanza.
* I dati di utilizzo delle risorse devono essere inoltrati al servizio di misurazione una volta ogni 2 - 24 ore. La frequenza con cui inoltri i dati di utilizzo dipende dalla frequenza con cui vengono modificate le tue metriche di utilizzo.
* I record di utilizzo devono essere inoltrati entro due giorni dall'ora in cui è stata completata la misurazione. I record di utilizzo meno recenti vengono rifiutati.
* Un inoltro eseguito correttamente restituisce un codice di risposta 201. Se viene restituito qualsiasi altro codice di risposta, aggiorna e invia nuovamente i dati finché non ricevi il codice 201.

Di seguito sono riportate le procedure ottimali per l'inoltro dell'utilizzo:

* Si consiglia a tali provider di servizi di inoltrare l'utilizzo ogni ora in modo che l'utente non visualizzi un notevole ritardo dall'ora in cui la risorsa è stata consumata e l'ora in cui il costo viene riflesso nel suo account.
* Ritenta l'inoltro dei record di utilizzo solo se si è verificato un errore effettivo con la richiesta precedente. Non inoltrare nuovamente i record di utilizzo che erano stati accettati correttamente.

### Linee guida per gli ID servizio
{: #id-guidelines}

  Devi attenerti alle seguenti linee guida quando specifichi l'ID servizio utilizzando il campo ID nella definizione della risorsa:
  * Inizia l'ID con un carattere alfanumerico.
  * Utilizza i caratteri A - Z, a - z e 0 - 9. I soli caratteri speciali che puoi usare sono trattini (-) e caratteri di sottolineatura (_).
  * Rispetta la convenzione di caratteri con notazione a cammello se l'ID contiene più di una parola.
  * Assicurati che la lunghezza massima dell'ID sia di 50 caratteri.

### Linee guida per i nomi risorsa
{: #resource-name}

  Devi attenerti alle seguenti linee guida quando specifichi il nome risorsa utilizzando il campo resources.name nella definizione della risorsa:

  * Utilizza solo parole che descrivono le tue risorse. Ad esempio, **Storage** o **ApiCalls**. 
  * Rispetta la convenzione di caratteri con notazione a cammello se il nome contiene più di una parola.
  * Metti in maiuscolo il primo carattere del nome.

### Linee guida per i nomi di unità risorsa
{: #resource-unti}

  Devi attenerti alle seguenti linee guida quando specifichi il nome di unità risorsa utilizzando il campo resources.unit.name nella definizione della risorsa:

  * Utilizza una parola per il nome di unità e utilizza un carattere di sottolineatura (_) invece di uno spazio per separare le parole. Ad esempio, specifica **API_CALL** invece di **API CALL**.  
  * Metti in maiuscole tutte le lettere del nome.
  
### Linee guida per la quantità di unità risorsa
{: #unit-quantity}

  Devi attenerti alle seguenti linee guida quando specifichi il tipo di quantità della risorsa utilizzando il campo resources.unit.quantityType nella definizione della risorsa:
  
  * Utilizza una parola per il tipo di quantità.
  * Metti in maiuscole tutte le lettere del tipo di quantità.
  
### Linee guida per gli ID aggregazione
{: #aggregation}

  Devi attenerti alle seguenti linee guida quando specifichi l'ID aggregazione utilizzando il campo aggregations.id nella definizione della risorsa:

  * Metti in maiuscole tutte le lettere del tipo di quantità.
  * Utilizza un carattere di sottolineatura (_) invece di uno spazio per separare le parole.
  * Assicurati che questo ID inizi con, o corrisponda al, valore di aggregations.unit. Ad esempio, puoi specificare **API_CALLS_PER_MONTH** per aggregations.id e specificare **API_CALLS** per aggregations.unit.

### Linee guida per le unità aggregazione
{: #aggregation-unit}

  Devi attenerti alle seguenti linee guida quando specifichi l'unità aggregazione utilizzando il campo aggregations.unit nella definizione della risorsa:
   
  * Utilizza la forma singolare per il nome unità.
  * Metti in maiuscole tutte le lettere del nome unità.
  * Assicurati che il nome unità da te specificato nel campo aggregations.unit sia un aggregato del nome unità da te specificato nel campo resources.unit.name.
  
### Linee guida per i gruppi aggregazione
{: #aggregation-group}

  Devi utilizzare i caratteri minuscoli per il campo aggregations.aggregationGroup nella definizione della risorsa.
  
### Linee guida per le formule aggregazione
{: #aggregation-formula}

  Per il campo aggregations.formula nella definizione della risorsa, se vuoi utilizzare operazioni aritmetiche nella formula, devi utilizzare l'unità di risorsa come un operando e utilizzare un'espressione aritmetica infissa nella funzione della formula. Ad esempio, puoi utilizzare la seguente formula per convertire i Byte in Megabyte:
  ```
  SUM({BYTE}/1048576)
  ```

## API REST di inoltro dell'utilizzo
{: #RAPIusesubmit}

L'addebito a carico degli utenti {{site.data.keyword.Bluemix_notm}} è basato sulla quantità di risorse che utilizzano. Ad esempio, l'addebito a carico degli utenti che utilizzano i servizi database potrebbe essere basato sulla quantità di archiviazione utilizzata dalle loro applicazioni.

Per utilizzare il servizio di misurazione {{site.data.keyword.Bluemix_notm}} per notificare i dati di utilizzo, implementa l'API del servizio di misurazione per notificare i dati di utilizzo della tua offerta. Per ulteriori dettagli, vedi la [documentazione dell'API pubblica](https://ibm-bluemix-docs.github.io/usage-submission/).  

Devi automatizzare l'inoltro dell'utilizzo orario utilizzando l'API di servizio di misurazione. Puoi ospitare il tuo inoltro automatizzato su qualsiasi endpoint HTTPs valido accessibile su internet pubblica.
{: tip}

## Inoltro dei record di utilizzo
{: #usage-records}

I record di utilizzo sono le entità più piccole che contribuiscono ai valori aggregati delle metriche. Un record di utilizzo viene costruito utilizzando i seguenti campi:

| Nome | Descrizione                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  L'ID dell'istanza della risorsa.  |
| plan_id | Il contratto in base al quale il record di utilizzo viene aggregato e valutato.   |
| start  | L'ora da cui viene misurato l'utilizzo, specificato in millisecondi a partire dall'epoch.  |
| end  | L'ora fino a cui viene misurato l'utilizzo, specificato in millisecondi a partire dall'epoch.  |
| regione  | La regione del provider di offerte in cui viene misurato l'utilizzo.  |
| measured_usage  | Un array di misure con i valori.  |
| consumer_id | Facoltativo. Questo campo è obbligatorio solo se l'aggregazione è richiesta a un livello di consumatore. Solo i provider di offerte conoscono il valore consumer_id. |
{: caption="Tabella 1. Campi di un record di utilizzo" caption-side="top"}

Puoi inoltrare più record di utilizzo servendoti della chiamata API e puoi inoltrare un massimo di 100 record di utilizzo per chiamata. Il corpo della risposta include lo stato di accettazione di ogni record di utilizzo. Qualsiasi stato diverso da 201 è accompagnato da un codice di errore e indica il motivo per cui il record di utilizzo non viene accettato. La seguente tabella elenca i codici di stato e l'azione richiesta.

| Codice di stato | Azione richiesta                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Prova ad inoltrare nuovamente il record di utilizzo. Se il problema persiste, contatta il team di misurazione BSS. |
| 400 |  Il record di utilizzo non è nel formato corretto. La convalida dello schema ha avuto esito negativo, le misure nei record di utilizzo non sono corrette o le ore di inizio e fine non cadono tra le ore di provisioning e di annullamento del provisioning. Aggiorna il record di utilizzo e inoltralo nuovamente.   |
| 424  | I metadati dell'istanza della risorsa presentano alcuni problemi. Aggiorna i dettagli dell'istanza della risorsa e inoltra nuovamente il record di utilizzo.  |
| 404  | Non è stato eseguito l'onboarding della definizione di misurazione. Lavora con il team di misurazione BSS per controllare se viene eseguito l'onboarding della risorsa e inoltra di nuovo il record di utilizzo.  |
| 409  | Il record di utilizzo è un duplicato. Non provare ad inoltrarlo di nuovo. |
{: caption="Tabella 2. Codici di stato e azioni richieste" caption-side="top"}
{: #actions}


  
