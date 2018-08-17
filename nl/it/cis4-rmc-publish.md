---


copyright:
  years: 2018
lastupdated: "2018-06-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Passo 5: Pubblica e verifica il tuo servizio

Ora che hai il tuo broker o i tuoi broker ospitati che soddisfano la specifica OSB, puoi ritornare alla console di gestione delle risorse per pubblicare il tuo servizio nel catalogo {{site.data.keyword.Bluemix_notm}}. Completa la scheda *Deployments*; pianifica la distribuzione dei tuoi piani di servizio in una o più regioni del catalogo {{site.data.keyword.Bluemix_notm}}, verifica il tuo broker o i tuoi broker e, infine, pubblica nel tuo catalogo in modalità di visibilità limitata. Dopo che hai eseguito correttamente la distribuzione, verifica la tua offerta per assicurarti che soddisfi i criteri obbligatori oppure riesegui il processo di pubblicazione come necessario.


## Prima di iniziare

Questo passo presuppone che tu sia stato approvato per fornire un servizio di fatturazione integrato. Se non hai ancora completato la registrazione e l'approvazione iniziali nel Provider Workbench, consulta l'[Esercitazione introduttiva](/docs/third-party/index.md).
{: tip}

Assicurati di aver avviato il passo 1 e di aver completato i passi 2, 3 e 4:
1. [Crea i documenti e il comunicato di marketing del servizio](/docs/third-party/cis1-docs-marketing.html).
2. [Definisci la tua offerta nella console di gestione delle risorse](/docs/third-party/cis2-rmc-define.html).
3. [Sviluppa e ospita i tuoi broker dei servizi](/docs/third-party/cis3-broker.html).
3. [Sviluppa un flusso di autenticazione](/docs/third-party/cis5-iam.html).

## Pubblica il tuo servizio in {{site.data.keyword.Bluemix_notm}}

1. Dalla console di gestione delle risorse, fai clic sulla pagina **Deployments**.
2. Fai clic sulla scheda **Brokers** e fai clic su **Add broker**
3. Fai clic su **Manage** per aprire la pagina Service Broker Configuration.
4. Aggiungi il tuo broker ospitato e fai clic su **Register broker**.
5. Dopo che hai eseguito correttamente la registrazione, passa alla scheda **Catalog Deployments**.
6. Fai clic su **Add Deployment** e seleziona il piano e il broker che desideri distribuire.
7. Seleziona la regione (Region) e il data center dove vuoi distribuire il tuo servizio e fai clic su **Add**.
8. Dalla pagina **Deployments**, riesamina la tua distribuzione non ancora pubblicata e fai clic su **Publish**.
9. Dalla pagina **Publish to the Catalog**, riesamina i dettagli della tua distribuzione e fai clic su **Publish**.

La pagina Deployments dovrebbe ora essere contrassegnata come completa nella navigazione, a indicare che hai soddisfatto i requisiti minimi.

Sei bloccato su un errore di distribuzione? Contatta il tuo rappresentante IBM per assistenza.
{: tip}

## Verifica la tua offerta distribuita 

Poiché hai eseguito la distribuzione in modalità di visibilità limitata, solo tu puoi vedere la tua offerta nel catalogo {{site.data.keyword.Bluemix_notm}}. Utilizzando l'elenco di controllo qui di seguito, esegui l'accesso {{site.data.keyword.Bluemix_notm}} e procedi con i criteri di verifica.

1. Esegui l'accesso a {{site.data.keyword.Bluemix_notm}}: [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") con il tuo ID IBM.
2. Assicurati di essere nell'account corretto (lo stesso account che hai utilizzato per creare il servizio)
3. Fai clic sul link **Catalog** nell'intestazione e cerca la tua offerta.
4. Utilizza quindi l'elenco di controllo qui di seguito per convalidare il tuo servizio.

### Elenco di controllo - verifica il tuo servizio
1. Convalida l'autenticazione dal dashboard dell'istanza del servizio
2. Il catalogo viene visualizzato correttamente (l'importazione dal broker viene visualizzata correttamente nella console di gestione delle risorse)
3. Il provisioning funziona - puoi creare un'istanza del servizio nel piano che hai scelto
4. L'annullamento del provisioning funziona - puoi eliminare un'istanza del servizio
5. Il bind funziona - puoi fare clic su **Connections** e connettere il tuo servizio a un'altra applicazione
6. L'annullamento del bind funziona - puoi disconnettere il tuo servizio ed eliminare la connessione.
7. Crea una chiave di servizio / Elimina la chiave di servizio - puoi fare clic su **Credentials** e generare una chiave di servizio e quindi eliminarla.
8. Verifica `plan_changeable` se supporti più piani. Se abiliti tale opzione impostando Yes, dovrai estendere il tuo Open Service Broker per supportare le modifiche di piano per le istanze di cui è stato eseguito il provisioning. Se la tua offerta supporta più piani, e desideri che gli utenti possano modificare i piani per un'istanza di cui è stato eseguito il provisioning, dovrai abilitare la capacità degli utenti di aggiornare la loro istanza del servizio. Per ulteriori dettagli, vedi l'endpoint /v2/service_instances/{instance_id} PATCH nella API Open Service Broker v2.12  - Patch - visualizza che l'utente può modificare il piano sull'istanza di cui è stato eseguito il provisioning. Per eseguire la verifica, esegui un passaggio del piano su un'istanza del servizio di cui è stato eseguito il provisioning esistente.
9. La specifica OSB non supporta uno stato di istanza disabilitata ma non ancora eliminata. Perché IBM Cloud supporti i clienti che potrebbero riscontrare un'interruzione della fatturazione o altre situazioni che comportano una sospensione dell'account (ma non ancora l'annullamento), IBM Cloud ha definito degli endpoint API estesi che consentono la disabilitazione e la riabilitazione delle istanze del servizio. Le seguenti estensioni di endpoint sono **OBBLIGATORIE**; coopera con il tuo rappresentante IBM e chiedigli di verificare i tuoi endpoint di abilitazione e disabilitazione:
   - abilitare e disabilitare le istanze (GET): stato - restituisce lo stato della tua istanza del servizio.
   - abilitare e disabilitare le istanze (PUT): ti consente di abilitare o disabilitare un'istanza del servizio.
10. Verifica l'inoltro dell'utilizzo se supporti dei piani a consumo. Per qualsiasi piano con utilizzo a consumo devi convalidare quanto segue:
   - Puoi eseguire il curl dell'API di utilizzo e restituire correttamente un prezzo accurato basato sull'utilizzo.
   - Puoi dimostrare che hai abilitato l'inoltro orario automatizzato per l'utilizzo, supportando tutti gli utenti che eseguono un provisioning di un'istanza del tuo servizio.

Se i tuoi test non vengono eseguiti correttamente, ripeti i passi precedenti per pubblicare il tuo servizio ed esegui nuovamente la verifica, ripetendo la procedura finché non ha esito positivo.


## Passi successivi

Ora che hai un servizio funzionale nel catalogo, puoi creare una Demo e chiedere l'approvazione per rilasciare pubblicamente il tuo servizio. Vedi [Passo 6: Rilascia pubblicamente il tuo servizio](/docs/third-party/cis6-ga.html).
