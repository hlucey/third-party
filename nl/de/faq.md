---

copyright:

  years: 2015, 2019

lastupdated: "2019-02-25"

keywords: IBM Cloud, different metering options, new IBM Cloud Identity, faqs 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# Häufig gestellte Fragen (FAQs)
{: #3p-faqs}

## Welche unterschiedlichen Messungsoptionen stehen für Pläne zur Verfügung?
{: #metering}
{: faq}

{{site.data.keyword.Bluemix}} unterstützt mehrere Modelle zur Aggregation der Angebotsnutzung. Die Angebotsprovider erfassen verschiedene Metriken für die bereitgestellten Instanzen und übermitteln diese Messdaten an den Messservice. Der Bewertungsservice aggregiert die übermittelten Nutzungsdaten auf Basis des Modells, das von den Angebotsprovidern ausgewählt wurde, in verschiedenen Buckets (Instanz, Ressourcengruppe und Konto). Die Aggregations- und Bewertungsmodelle für alle Metriken eines Plans sind in den Dokumenten für die Messungs- und Bewertungsdefinition des jeweiligen Plans enthalten.

Sie müssen die stündliche Übermittlung von Nutzungsdaten mithilfe der Messservice-API automatisieren, wenn Sie einen Plan mit Nutzungsmessung anbieten.
{: note}

Weitere Informationen zu Messungen finden Sie in [Messungsintegration](/docs/third-party?topic=third-party-meteringintera#meteringintera). Weitere Informationen zur Übermittlung der gemessenen Nutzungsdaten finden Sie in [Nutzungsdaten für Pläne mit Nutzungsmessung übermitteln](/docs/third-party?topic=third-party-submitusage#submitusage).

## Wie kann ich einen neuen API-Schlüssel für {{site.data.keyword.Bluemix_notm}} Identity and Access Management generieren?
{: #iam-creds}
{: faq}

Sie erhalten den API-Schlüssel bei der Aktivierung von IAM. Es ist wichtig, dass Sie den API-Schlüssel speichern. Der Wert wird nicht erneut angezeigt. Wenn Sie den API-Schlüssel verlieren, können Sie den Schlüssel löschen und einen neuen erstellen. Weitere Informationen finden Sie in [API-Schlüssel für Service-ID verwalten](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys). 


