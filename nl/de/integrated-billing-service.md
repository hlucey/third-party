---


copyright:
  years: 2018
lastupdated: "2018-07-20"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Überblick: Integrierten Abrechnungsservice entwickeln
{: #overview}

In diesem Abschnitt werden die Schritte beschrieben, die erforderlich sind, um Ihren integrierten Drittanbieterabrechnungsservice zu entwickeln und in {{site.data.keyword.Bluemix}} zu publizieren.
{:shortdesc}

Nachdem Sie die Genehmigung zur Bereitstellung Ihres Angebots im {{site.data.keyword.Bluemix_notm}}-Katalog erhalten haben, können Sie mit der Entwicklung des Angebots in der Ressourcenmanagementkonsole, einer menügeführten Benutzerschnittstelle, beginnen. Sie können Katalogmetadaten entwerfen, Preisstrukturpläne für den Service festlegen und die Integration mit {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) konfigurieren. 

Als nächsten Schritt führen Sie außerhalb der Ressourcenmanagementkonsole die Codeentwicklung durch, um einen neuen Open Service Broker zu erstellen und zu hosten (Broker-Beispiele für den Einstieg und API-Docs werden bereitgestellt), und Sie verwenden IAM um einen Authentifizierungsablauf zu entwickeln. Nach Abschluss dieser Schritte rufen Sie die Ressourcenmanagementkonsole erneut auf, um den Service im Katalog im Modus für eingeschränkte Sichtbarkeit bereitzustellen. Dieser Modus ermöglicht Ihnen das Testen und Validieren mehrerer Bereitstellungsanforderungen. Nach Abschluss dieser Arbeitsschritte kann Ihr Service, wenn alle Anforderungen erfüllt sind, als vollständig sichtbar im {{site.data.keyword.Bluemix_notm}}-Katalog definiert werden.


## Ablauf des Prozesses
{: #process}

Zur Bereitstellung eines integrierten Abrechnungsservice arbeiten Sie mit der Provider Workbench (PWB), der Ressourcenmanagementkonsole und Ihrer bevorzugten Entwicklungsumgebung. Verwenden Sie die [Prüfliste](/docs/third-party/checklist.html#checklist), um diese Schritte zu überwachen.

1. [Dokumentation und Vertriebsfreigabe erstellen](/docs/third-party/cis1-docs-marketing.html).
2. [Angebot in der Ressourcenmanagementkonsole definieren{{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html).
3. [Eigene Service-Broker entwickeln und hosten](/docs/third-party/cis3-broker.html).
4. [Authentifizierungsablauf entwickeln](/docs/third-party/cis5-iam.html).
5. [Service testen](/docs/third-party/cis4-rmc-publish.html).
6. [Service öffentlich freigeben](/docs/third-party/cis6-ga.html).

Bei diesen Schritten wird davon ausgegangen, dass Sie bereits über die Genehmigung zum Bereitstellen eines integrierten Abrechnungsservice verfügen. Falls Sie den Erstregistrierungs- und Genehmigungsprozess in der Provider Workbench noch nicht durchgeführt haben, sollten Sie sich mit den Informationen im [Lernprogramm zur Einführung](/docs/third-party/index.md) vertraut machen.
{: tip}

## Unterstützung
{: #support}

Für integrierte Abrechnungsservices ist es erforderlich, dass die Drittanbieter des Angebots ein eigenes Unterstützungsmodell bereitstellen. Der zuständige IBM Ansprechpartner kann bei der Aktivierung des Unterstützungsmodells helfen und sicherstellen, dass beim Öffnen eines {{site.data.keyword.Bluemix_notm}}-Support-Tickets durch einen Benutzer dieses Ticket an die Unterstützungssite des Drittanbieters weitergeleitet wird.

## Fortlaufende Aktualisierungen
{: #maintain}

Nach Freigabe Ihres Service können Sie fortlaufend Aktualisierungen durchführen, indem Sie direkt mit dem zuständigen {{site.data.keyword.Bluemix_notm}}-Ansprechpartner zusammenarbeiten.



