---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: party offering types, third-party offering, billing service

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Typen von Drittanbieterangeboten
{: #offering-types}

Sie können ein Drittanbieterangebot in {{site.data.keyword.Bluemix}} entweder als integrierten Abrechnungsservice oder als Empfehlungsservice bereitstellen.
{:shortdesc}

Die Bereitstellung Ihres Drittanbieterangebots als integrierter Abrechnungsservice bedeutet, dass Benutzer unter verschiedenen IBM Preisstrukturplänen, die auf der Katalogdetailseite in der {{site.data.keyword.Bluemix_notm}}-Konsole aufgelistet werden, eine Auswahl treffen können. Darüber hinaus können Benutzer automatisch eine Instanz Ihres Drittanbieterangebots erstellen.

Wenn Sie Ihr Drittanbieterangebot als Empfehlungsservice bereitstellen, dann werden Benutzer von der Katalogdetailseite in der {{site.data.keyword.Bluemix_notm}}-Konsole auf Ihre Website weitergeleitet. Auf Ihrer Website können Benutzer Konten erstellen und erhalten die entsprechenden Berechtigungsnachweise. Diese Berechtigungsnachweise werden zum programmgesteuerten Herstellen der Verbindung Ihres Drittanbieterangebots mit einer App benötigt, die in {{site.data.keyword.Bluemix_notm}} erstellt wird.

## Angebotstypen vergleichen
{: #compare}

Die folgende Tabelle enthält eine detaillierte Gegenüberstellung der verschiedenen Typen von Drittanbieterangeboten.

|  | Integrierter Abrechnungsservice  | Empfehlungsservice |
|---|---|---|
| **Onboarding** | Das Onboarding wird über die IBM Provider-Workbench und die Konsole für das Ressourcenmanagement durchgeführt. Der Angebotsprovider entwickelt einen Open Service Broker (OSB), hostet und testet diesen OSB und veröffentlicht das Angebot über eine Reihe von Self-Service-Arbeitsschritten. | Das Onboarding wird über die Provider-Workbench durchgeführt. Der Self-Service-Prozess für das Onboarding nimmt ca. zwei Wochen in Anspruch. |
| **Bereitstellung** | Erstellung über die {{site.data.keyword.Bluemix_notm}}-Plattform | Nur für API-basierte Services |
| **Abrechnung**  |  Im Modell für die integrierte Abrechnung empfängt der Benutzer eine einzige Rechnung, die sowohl für das IBM Angebot als auch das integrierte Drittanbieterangebot gilt. | Im Empfehlungsmodell erhalten Benutzer eine Rechnung des Providers, der 100 % der Einnahmen einbehält.  |
| **Beispiel** | [PowerAI](https://{DomainName}/catalog/services/powerai){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") | [Accern API](https://{DomainName}/catalog/services/accern-api){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") |
{: caption="Tabelle 1. Gegenüberstellung der Typen von Drittanbieterangeboten" caption-side="top"}

