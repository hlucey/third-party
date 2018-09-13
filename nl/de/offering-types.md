---


copyright:
  years: 2018
lastupdated: "2018-07-20"


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

Die Bereitstellung Ihres Drittanbieterangebots als integrierter Abrechnungsservice bedeutet, dass Benutzer eine Auswahl unter verschiedenen IBM Preisstrukturplänen treffen können, die auf der Katalogdetailseite in der {{site.data.keyword.Bluemix_notm}}-Konsole aufgelistet werden. Darüber hinaus können Benutzer automatisch eine Instanz Ihres Drittanbieterangebots erstellen.

Wenn Sie Ihr Drittanbieterangebot als Empfehlungsservice bereitstellen, dann werden Benutzer von der Katalogdetailseite in der {{site.data.keyword.Bluemix_notm}}-Konsole auf Ihre Website weitergeleitet. Auf Ihrer Website können Benutzer Konten erstellen und die entsprechenden Berechtigungsnachweise anfordern, die zur programmgesteuerten Verbindung Ihres Drittanbieterangebots mit einer App erforderlich sind, die in {{site.data.keyword.Bluemix_notm}} erstellt wird.

## Angebotstypen vergleichen
{: #compare}

Die folgende Tabelle enthält eine detaillierte Gegenüberstellung der verschiedenen Typen von Drittanbieterangeboten.

|  | Integrierter Abrechnungsservice  | Empfehlungsservice |
|---|---|---|
| **Onboarding** | Das Onboarding wird über IBM Provider Workbench und die Konsole für das Ressourcenmanagement durchgeführt. Der Angebotsprovider ist für die Entwicklung eines Open Service Broker (OSB), das Hosten und Testen dieses OSB und die Veröffentlichung des Angebots über eine Reihe von Self-Service-Arbeitsschritten verantwortlich. | Das Onboarding wird über Provider Workbench durchgeführt. Der Self-Service-Prozess für das Onboarding nimmt ca. zwei Wochen in Anspruch. |
| **Bereitstellung** | Bereitstellung durch die {{site.data.keyword.Bluemix_notm}}-Plattform. | Nur für API-basierte Services |
| **Abrechnung**  | Im Modell für die integrierte Abrechnung empfängt der Benutzer eine einzige Rechnung, die sowohl für das IBM Angebot als auch das integrierte Drittanbieterangebot gilt. | Im Empfehlungsmodell erhalten Benutzer eine Rechnung des Providers, der 100 % der Einnahmen einbehält. |
| **Beispiel** | [PowerAI](https://console.bluemix.net/catalog/services/powerai) | [Accern-API](https://console.bluemix.net/catalog/services/accern-api) |
{: caption="Tabelle 1. Gegenüberstellung der Typen von Drittanbieterangeboten" caption-side="top"}

