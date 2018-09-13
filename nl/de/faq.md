---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-28"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Häufig gestellte Fragen (FAQs)
{: #3p-faqs}

## Welche unterschiedlichen Messungsoptionen stehen für Pläne zur Verfügung?
{: #metering}

{{site.data.keyword.Bluemix}} unterstützt mehrere Modelle zur Aggregation der Angebotsnutzung. Die Angebotsprovider erfassen verschiedene Metriken für die bereitgestellten Instanzen und übermitteln diese Messdaten an den Messservice. Der Bewertungsservice aggregiert die übermittelten Nutzungsdaten auf Basis des Modells, das von den Angebotsprovidern ausgewählt wurde, in verschiedenen Buckets (Instanz, Ressourcengruppe und Konto). Die Aggregations- und Bewertungsmodelle für alle Metriken eines Plans sind in den Dokumenten für die Messungs- und Bewertungsdefinition des jeweiligen Plans enthalten.

**Hinweis:** Sie müssen die stündliche Übermittlung von Nutzungsdaten mithilfe der Messservice-API automatisieren, wenn Sie einen Plan mit Nutzungsmessung anbieten möchten.

Weitere Informationen zu Messungen finden Sie in [Messungsintegration](/docs/third-party/metering.html#meteringintera). Weitere Informationen zur Übermittlung der gemessenen Nutzungsdaten finden Sie in [Nutzungsdaten für Pläne mit Nutzungsmessung übermitteln](/docs/third-party/submitusage.html#submitusage).

## Wie kann ich einen neuen API-Schlüssel für {{site.data.keyword.Bluemix_notm}} Identity and Access Management generieren?
{: #iam-creds}

Sie erhalten den API-Schlüssel bei der Aktivierung von IAM. Es ist wichtig, dass Sie den API-Schlüssel speichern. Der Wert wird nicht erneut angezeigt. Wenn Sie den API-Schlüssel verlieren, können Sie den Schlüssel löschen und einen neuen erstellen. Weitere Informationen finden Sie in [API-Schlüssel für Service-ID verwalten](/docs/iam/serviceid_keys.html#serviceidapikeys). 


