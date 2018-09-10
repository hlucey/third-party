---


copyright:

  years: 2017, 2018

lastupdated: "2018-08-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Integrazione della misurazione
{: #meteringintera}

{{site.data.keyword.Bluemix}} supporta molteplici modelli per l'aggregazione dell'utilizzo dell'offerta. I provider di offerte misurano diverse metriche sulle istanze di cui viene eseguito il provisioning e inoltrano tali misure al servizio di misurazione. Il servizio di valutazione aggrega l'utilizzo inoltrato in diversi contenitori (istanza, gruppo di risorse ed account) sulla base del modello scelto dai provider delle offerte. I modelli di aggregazione e valutazione per tutte le metriche in un piano sono contenuti nei documenti di definizione di misurazione e valutazione per il piano.
{:shortdesc}

Il seguente elenco descrive le aspettative per la traccia e l'inoltro dell'utilizzo:

*	I provider di offerte di terze parti non sono tenuti a inoltrare l'utilizzo per i piani gratuiti.
*	I provider di offerte di terze parti non sono tenuti a inoltrare l'utilizzo per i piani di sottoscrizione mensili.
*	Per i piani a consumo, tutti i provider di offerte devono inoltrare l'utilizzo ogni ora (i piani Lite devono eseguire l'inoltro con una frequenza ogni 15 minuti - 1 ora).
*	Il provider di offerte è responsabile dell'automazione dell'inoltro dell'utilizzo, compresa l'automazione che riprova le risposte di errore. {{site.data.keyword.Bluemix_notm}} non fornisce una funzione di nuovo tentativo per gli inoltri non riusciti. Per ulteriori informazioni, vedi la tabella delle azioni e dei codici di stato in [Inoltro dei record di utilizzo](/docs/third-party/submitusage.html#submitting-usage-records).
*	I record di utilizzo per il mese corrente devono essere inoltrati al più tardi entro il secondo giorno del mese successivo.
*	{{site.data.keyword.Bluemix_notm}} è configurato per un ciclo di fatturazione mensile e l'ora è rappresentata in Coordinated Universal Time (UTC).
*  I provider di offerte devono verificare l'inoltro dell'utilizzo e convalidare i loro risultati per informare della modalità di calcolo del ciclo di fatturazione mensile.

Per informazioni generali sui prezzi, consulta [Come calcolare i tuoi costi](https://console.bluemix.net/docs/billing-usage/estimating_costs.html#cost). 

## Proprietà di configurazione
{: #configure}

Le seguenti proprietà definiscono in che modo vengono misurati e valutati gli inoltri dell'utilizzo per i piani di offerta:

<dl>
<dt>Unità</dt>
<dd>Metriche da misurare, ad esempio chiamata ApiCall, Bytes, Hours, Instances e Nodes.</dd>
<dt>Aggregation</dt>
<dd>La modalità di compilazione dei dati unitari, ad esempio INSTANCES_BY_MONTH o ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Metering model</dt>
<dd>La modalità di elaborazione dei dati di inoltro dell'utilizzo, come mostrato nella seguente tabella.</dd>
<dt>Resource name</dt>
<dd>Il nome della risorsa di cui è in corso la misurazione, ad esempio storage, instance, virtual server o byte transmitted.</dd>
<dt>Unit name</dt>
<dd>Il nome descrittivo dell'unità se il nome predefinito non è rilevante per l'offerta.</dd>
</dl>

## Tipo di modello di misurazione
{: #metermodel}

La seguente tabella mostra i modelli di misurazione disponibili:

|  Tipo | Descrizione  |
|-----|-----|
| standard_add | Aggiunge la quantità da tutti i record di utilizzo inoltrati per un mese. | 
| standard_max  | Quantità massima da tutti i record di utilizzo inoltrati per un mese. | 
| standard_avg | Quantità media da tutti i record di utilizzo inoltrati per un mese. |
| dailyproration_max | Massimo giornaliero calcolato. Somma tutti i giorni per il mese. | 
| dailyproration_avg | Media giornaliera calcolata. Somma tutti i giorni per il mese. |
| monthlyproration | Calcolato in modo simile alla quota proporzionale giornaliera ma il prezzo utilizzato è il prezzo del piano diviso per il numero totale di giorni per il mese (prezzo giornaliero). |
{: caption="Tabella 1. Modello di misurazione" caption-side="top"}

### Esempi
Nota che la quantità nel dashboard in ciascuno dei seguenti esempi è antecedente all'inoltro dell'utilizzo successivo ma posteriore all'elaborazione dell'utilizzo corrente.

#### Aggiunta standard
Calcola gli utilizzi per l'intero mese.

Formula: ADD(utilizzi)

| Ora            | Utilizzo inviato | Calcolo | Quantità nel dashboard |
|-----------------|:-------------:| ----------- |:---------------------:|
| Giorno 1 (mattina) | 5             | 5           | 5                     |
| Giorno 1 (notte)   | 5             | 5 + 5       | 10                    |
| Giorno 2 (mattina) | 5             | 10 + 5      | 15                    |
| Giorno 3 (mattina) | 5             | 15 + 5      | 20                    |
| Giorno 4 (notte)   | 5             | 20 + 5      | 25                    |

#### Media standard
Calcola la media degli utilizzi per l'intero mese. Nota che nella media si tiene conto anche dell'inoltro di un utilizzo zero.

Formula: AVG(utilizzi)

| Ora            | Utilizzo inviato | Calcolo             | Quantità nel dashboard |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Giorno 1 (mattina) | 4             | 4 / 1                   | 4                     |
| Giorno 1 (notte)   | 0             | (4 + 0) / 2             | 2                     |
| Giorno 2 (mattina) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Giorno 3 (mattina) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Giorno 4 (notte)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |

#### Massimo standard
Calcola il massimo degli utilizzi per l'intero mese.

Formula: MAX(utilizzi)

| Ora            | Utilizzo inviato  | Calcolo  | Quantità nel dashboard |
|-----------------|:--------------:| ------------ |:---------------------:|
| Giorno 1 (mattina) | 5              | MAX(5)       | 5                     |
| Giorno 1 (notte)   | 10             | MAX(5, 10)   | 10                    |
| Giorno 2 (mattina) | 0              | MAX(10, 0)   | 10                    |
| Giorno 3 (mattina) | 15             | MAX(10, 15)  | 15                    |
| Giorno 4 (notte)   | 1              | MAX(15, 1)   | 15                    |

#### Media proporzionale giornaliera
Calcola l'utilizzo medio per ogni giorno e ne calcola la media per il mese. La media di ogni giorno viene sommata e divisa per il numero di giorni attualmente trascorso (in UTC).

Formula: Summation(media giornaliera) / numero di giorni trascorsi nel periodo di fatturazione

Nota che la quantità potrebbe cambiare nel corso del mese ma ciò che viene valutato è l'utilizzo medio al giorno.

Dato un mese di 30 giorni:

| Ora               | Utilizzo inviato    | Media quotidiana | Calcolo                            | Quantità nel dashboard*                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Giorno 1 (mattina)    | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Giorno 1 (notte)      | 3                | (8 + 3) / 2   | 5,5 / 1                                | 5,5 (il giorno 1 fine giornata)                               |
| Giorno 2 (mattina)    | 2                | 2 / 1         | (5,5 + 2) / 2                          | 3,75                                             |
| Giorno 2 (notte)      | 5                | (2 + 5) / 2   | (5,5 + 3,5) / 2                        | 4,5 (il giorno 2 fine giornata)                               |
| Dal giorno 3 al giorno 15    | 1                | 1 / 1         | (5,5 + 3,5 + (1 + 13)  / 15            | 1,4666  (il giorno 15 fine giornata)                          |
| Dal giorno 15 al giorno 30   | 0                | 0 / 1         | (5.5 + 3.5 + (1 \* 12) + (0  \* 15) / 30 | 0,7333  (il giorno 30 fine giornata)                          |

\* Come visto nello stesso giorno di quando è stato inoltrato l'utilizzo.

#### Massimo proporzionale giornaliero
Calcola l'utilizzo massimo per ogni giorno e ne calcola la media per il mese. Il massimo di ogni giorno viene sommato e diviso per il numero di giorni attualmente trascorso (in UTC).

Formula: Summation(massimo giornaliero) / numero di giorni trascorsi nel periodo di fatturazione

Nota che la quantità potrebbe cambiare nel corso del mese ma ciò che viene valutato è l'utilizzo massimo al giorno.

Dato un mese di 30 giorni:

| Ora             | Utilizzo inviato  | Massimo giornaliero | Calcolo                    | Quantità nel dashboard* |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Giorno 1 (mattina)  | 0              | MAX(0)    | 0 / 1                          | 0                      |
| Giorno 1 (notte)    | 1              | MAX(0, 1) | 1 / 1                          | 1                      |
| Dal giorno 2 al giorno 15  | 1              | MAX(1)    | (1 + 1 + ...) / giorno            | 1                      |
| Dal giorno 15 al giorno 30 | 0              | MAX(0)    | (1 + (1 * 14) + 0 + ...) / giorno | < 1                    |

\* Come visto nello stesso giorno di quando è stato inoltrato l'utilizzo.

## Esempi di scala di misurazione e valutazione
{: #scale-examples}

Puoi utilizzare la configurazione di ridimensionamento per compilare la quantità unitaria differentemente da quello che viene inviato negli inoltri dell'utilizzo a quello che viene visualizzato nel dashboard di utilizzo e quello che viene utilizzato per i calcoli di valutazione e costo. I seguenti esempi illustrano questi scenari:

### Desideri avere una maggiore granularità rispetto a quella che gli utenti vedono
Vuoi inviare gli utilizzi a un livello più granulare ma vuoi mostrare ai clienti un numero più leggibile.

Ad esempio, potresti voler misurare il traffico di un'istanza in byte e volere i valori aggregati in megabyte. Per eseguire tale operazioni, aggiungi una `scale` di 1024 alla configurazione **metering**.

### Desideri avere una maggiore granularità rispetto a quella che ha la tua configurazione dei prezzi
Stabilisci il prezzo delle tue metriche come $X / gigabyte, ma vuoi eseguirne l'invio in megabyte. Se il prezzo della tua metrica è stabilito a $1 / gigabyte ma un utente utilizza 0,5 megabyte, gli viene addebitato $1 poiché il tuo prezzo è per gigabyte. Aggiungi una `scale` di 1024 alla configurazione **rating** e imposti `clip` su `true`.

Questo vale anche se il prezzo della tua metrica viene stabilito come $X per 100 chiamate API (o altra dimensione di pacchetto).

### Vuoi eseguire un ridimensionamento sia al livello di misurazione che a quello di valutazione
Puoi aggiungere un ridimensionamento in entrambe le configurazioni di misurazione e valutazione. Se vuoi eseguire l'invio in byte ma visualizzare i megabyte all'utente, configuri il ridimensionamento della misurazione a 1024. Se il tuo prezzo di metrica è in gigabyte, puoi anche configurare il ridimensionamento della valutazione in modo che sia 1024.

## Modelli di prezzi
{: #pricing}

La seguente tabella fornisce informazioni dettagliate sui modelli di determinazione dei prezzi disponibili. Per molte delle metriche disponibili, selezioni un modello di prezzi associato.

| Modello          | Descrizione | Calcolo | Esempio (quantità 5000) |
|:-----------------|:-------------|:----------- |:---------------------|
| Linear         | Moltiplica il prezzo unitario per risorsa (P) per la quantità di utilizzo (Q) per ottenere l'importo totale (T)  | P*Q    | P=$1 T=1*5000 =$5000        |
| Proration      | Moltiplica il prezzo unitario giornaliero per risorsa (P) per la quantità di utilizzo giornaliero (Q) per ottenere l'importo giornaliero totale. L'addebito totale comporta l'accumulo degli addebiti per tutti i giorni nel mese.         | T= (pd * Q1) + ...+(Pd *Qn)     | <ul><li>P= $30</li><li>Pd (prezzo giornaliero) =$30/30=$1 (presumendo 30 giorni in un mese)</li><li>T1= $1 * 1 =$1</li><li>T2 = $1 * 0 =$0</li><li>Tn = 1 * 1 =$1</li><li>T = $1 + $0 +...+$1 = $5000</li></ul>     |
| Simple tier (granular tier)  | Un modello P*Q in cui il prezzo unitario per tutto il consumo è determinato dal livello in cui rientra la quantità.           | <ul><li>If Q is <=Q1, T=P1*Q</li><li>If Q1 < Q <=Q2, T=P2*Q</li><li>If Q2 < Q <=Q3, T=P3*Q</li></ul>     |   <ul><li>Q1=1000, P1=$1</li><li>Q2=2500, P2=$0.9</li><li>Q3=10000, P3=$0.75</li><li>T=$0.75*5000=$3750</li></ul>              |
| Graduated tier (step tier)   | Il prezzo per unità varia man mano che la quantità consumata si sposta in livelli predefiniti differenti. L'addebito totale comporta l'accumulo degli addebiti dai livelli precedenti           | <ul><li>T1=P1*Q (0 < Q</li><li>If Q1 < Q <=Q2, T=T2</li><li>If Q2 < Q <=Q3, T=T3</li></ul>     | <ul><li>Q1=1000, P1=$1, T1=1*1000</li><li>Q2=1500, P2=$0.9, T2=0.9*1500</li><li>Q3=10000, P3=$0.75, T3=0.75*2500</li><li>T=1000 +1350+1875=$4225</li></ul>          |
| Block tier (up to)           | L'importo totale addebitato è stabilito da una quantità "fino a" che non varia nel blocco     | <ul><li>If Q is <=Q1, T=T1</li><li>If Q1 < Q <=Q2, T=T2</li><li>If Q2 < Q <=Q3, T=T3</li></ul>    |  <ul><li>Q1=1000, T1=$0</li><li>Q2=2500, T2=2500</li><li>Q3=10000, T3=$4500</li><li>T=$4500</li></ul>            |


