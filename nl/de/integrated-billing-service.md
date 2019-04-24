---


copyright:
  years: 2018, 2019
lastupdated: "2019-01-30"


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

Als nächsten Schritt führen Sie außerhalb der Ressourcenmanagementkonsole die Codeentwicklung durch, um einen neuen Open Service Broker zu erstellen und zu hosten. Broker-Beispiele für den Einstieg und API-Docs werden bereitgestellt und Sie verwenden IAM, um einen Authentifizierungsablauf zu entwickeln. Rufen Sie anschließend die Ressourcenmanagementkonsole erneut auf, um den Service im Katalog im Modus für eingeschränkte Sichtbarkeit bereitzustellen. In diesem Modus können Sie die Erfüllung von Bereitstellungsanforderungen testen und überprüfen. Wenn Sie dies erledigt haben und Ihr Angebot alle Anforderungen erfüllt, wird Ihr Service im {{site.data.keyword.Bluemix_notm}}-Katalog vollständig sichtbar!


## Ablauf des Prozesses
{: #process}

Zur Bereitstellung eines integrierten Abrechnungsservice arbeiten Sie mit der Provider-Workbench (PWB), der Ressourcenmanagementkonsole und Ihrer bevorzugten Entwicklungsumgebung. Verwenden Sie die [Prüfliste](/docs/third-party?topic=third-party-checklist#checklist), um diese Schritte zu überwachen.

Bei diesen Schritten wird davon ausgegangen, dass Sie bereits über die Genehmigung zum Bereitstellen eines integrierten Abrechnungsservice verfügen. Sollten Sie die Erstregistrierung und die Genehmigung in der Provider-Workbench noch nicht abgeschlossen haben, sollten Sie sich mit den Informationen im Abschnitt mit der [Einführung zum Veröffentlichen Ihres Drittanbieterangebots in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md?topic=third-party-get-started#get-started) vertraut machen.
{: tip}

1. [Dokumentation und Vertriebsfreigabe erstellen](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [Angebot in der Konsole für das Ressourcenmanagement definieren{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define).
3. [Eigene Service-Broker entwickeln und hosten](/docs/third-party?topic=third-party-step3-osb#step3-osb).
4. [Authentifizierungsablauf entwickeln](/docs/third-party?topic=third-party-step4-iam#step4-iam).
5. [Service testen](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest).
6. [Service öffentlich freigeben](/docs/third-party?topic=third-party-public-releasing#public-releasing).

## Unterstützung
{: #support}

Für integrierte Abrechnungsservices ist es erforderlich, dass die Drittanbieter des Angebots ein eigenes Unterstützungsmodell bereitstellen. Der zuständige IBM Ansprechpartner kann bei der Aktivierung des Unterstützungsmodells helfen und sicherstellen, dass beim Öffnen eines {{site.data.keyword.Bluemix_notm}}-Support-Tickets durch einen Benutzer das betreffende Ticket an die Unterstützungssite des Drittanbieters weitergeleitet wird.

## Fortlaufende Aktualisierungen
{: #maintain}

Nach Freigabe Ihres Service können Sie fortlaufend Aktualisierungen durchführen, indem Sie direkt mit dem zuständigen {{site.data.keyword.Bluemix_notm}}-Ansprechpartner zusammenarbeiten.



