---


copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Tipi di offerta di terze parti
{: #offering-types}

Puoi distribuire un'offerta di terze parti come un servizio di fatturazione integrato o di riferimento in {{site.data.keyword.Bluemix}}.
{:shortdesc}

La distribuzione della tua offerta di terze parti come un servizio di fatturazione integrato indica che gli utenti possono scegliere tra diversi piani dei prezzi IBM elencati nella tua pagina dei dettagli del catalogo nella console {{site.data.keyword.Bluemix_notm}}. Inoltre, gli utenti possono automaticamente creare un'istanza della tua offerta di terze parti.

Quando distribuisci la tua offerta di terze parti come un servizio di riferimento, gli utenti vengono indirizzati al tuo sito web dalla pagina dei dettagli del catalogo nella console {{site.data.keyword.Bluemix_notm}}. Dal tuo sito web, gli utenti creano gli account e ottengono le credenziali appropriate. Queste credenziali sono necessarie per collegare in modo programmatico la tua offerta di terze parti a un'applicazione che stanno creando in {{site.data.keyword.Bluemix_notm}}.

## Confronto dei tipi di offerta
{: #compare}

La seguente tabella fornisce un confronto dettagliato dei tipi di offerta di terze parti.

|  | Servizio di fatturazione integrato  | Servizio di riferimento |
|---|---|---|
| **Onboarding** | L'onboarding viene gestito tramite il workbench IBM Provider e la console di gestione delle risorse. Il provider dell'offerta sviluppa un OSB (Open Service Broker), lo ospita, lo verifica e pubblica la sua offerta tramite una serie di passi self-service. | L'onboarding viene gestito tramite il workbench Provider. Il processo di onboarding self-service richiede circa due settimane. |
| **Distribuzione** | Creato dalla piattaforma {{site.data.keyword.Bluemix_notm}} | Solo servizi basati sull'API |
| **Fatturazione**  |  Nel modello di fatturazione integrato, l'utente riceve una sola fattura per l'offerta IBM e per la loro offerta integrata di terze parti. | Nel modello di riferimento, il provider emette fattura per l'utente e tiene il 100% del ricavo.  |
| **Esempio** | [PowerAI](https://{DomainName}/catalog/services/powerai){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") | [API Accern](https://{DomainName}/catalog/services/accern-api){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") |
{: caption="Tabella 1. Confronto di tipi di offerta di terze parti" caption-side="top"}

