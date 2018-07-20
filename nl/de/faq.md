---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Häufig gestellte Fragen (FAQs)
{: #3p-faqs}

Im Folgenden sind einige häufig gestellte Fragen (FAQs = Frequently Asked Questions) aufgeführt, die zur Beantwortung häufig gestellter Fragen dienen.

## Welche unterschiedlichen Messungsoptionen stehen für Pläne zur Verfügung?
{: #metering}

{{site.data.keyword.Bluemix}} unterstützt mehrere Modelle zur Aggregation der Angebotsnutzung. Die Angebotsprovider erfassen verschiedene Metriken für die bereitgestellten Instanzen und übermitteln diese Messdaten an den Messservice. Der Bewertungsservice aggregiert die übermittelten Nutzungsdaten auf Basis des Modells, das von den Angebotsprovidern ausgewählt wurde, in verschiedenen Buckets (Instanz, Ressourcengruppe und Konto). Die Aggregations- und Bewertungsmodelle für alle Metriken eines Plans sind in den Dokumenten für die Messungs- und Bewertungsdefinition des jeweiligen Plans enthalten.

**Hinweis:** Sie müssen die stündliche Übermittlung von Nutzungsdaten mithilfe der Messservice-API automatisieren, wenn Sie einen nutzungsabhängigen Plan anbieten möchten.

Weitere Informationen zur Messung finden Sie in [Messungsintegration](/docs/third-party/metering.html#meteringintera).

Weitere Informationen zur Übermittlung der gemessenen Nutzung finden Sie im Abschnitt [Nutzungsdaten für nutzungsabhängige Pläne übermitteln](/docs/third-party/submitusage.html#submitusage).

## Ich habe meinen API-Schlüssel für {{site.data.keyword.Bluemix_notm}} Identity and Access Management verloren. Wie kann ich einen neuen Schlüssel generieren?
{: #iam-creds}

Sie erhalten Ihren API-Schlüssel, wenn Sie **IAM aktivieren**. Es ist wichtig, dass Sie den API-Schlüssel speichern. Der Wert wird nicht erneut angezeigt. Wenn Sie den API-Schlüssel verlieren, dann können Sie ihn löschen und einen neuen API-Schlüssel erstellen: [API-Schlüssel für Service-ID verwalten](/docs/iam/serviceid_keys.html#serviceidapikeys)


