---


copyright:
  years: 2018
lastupdated: "2018-06-28"


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

Dieser Abschnitt führt Sie durch die Schritte zum Entwickeln und Veröffentlichen Ihres integrierten Drittanbieterabrechnungsservice in {{site.data.keyword.Bluemix_notm}}. Nachdem Sie die Genehmigung zur Bereitstellung Ihres Angebots im {{site.data.keyword.Bluemix_notm}}-Katalog erhalten haben, können Sie mit der Entwicklung Ihres Angebots in der Konsole für das Ressourcenmanagement (geführte Benutzerschnittstellenerfahrung) beginnen. In der Konsole für das Ressourcenmanagement werden Sie die Katalogmetadaten entwerfen, die Preisstrukturpläne des Service festlegen und die Integration mit IBM Cloud Access Management (IAM) durchführen. Als Nächstes werden Sie außerhalb der Konsole für das Ressourcenmanagement die Codeentwicklung durchführen, um einen neuen Open Service Broker zu erstellen und zu hosten (Starter-Brokerbeispiele und API-Dokumente werden bereitgestellt). Außerdem werden Sie IAM verwenden, um einen Authentifizierungsablauf zu entwickeln. Nach Abschluss dieser Schritte werden Sie zur Konsole für das Ressourcenmanagement zurückkehren, um Ihren Service im Katalog im Modus für eingeschränkte Sichtbarkeit bereitzustellen. In diesem Modus können Sie verschiedene Anforderungen für die Bereitstellung testen und überprüfen. Nach Abschluss dieser Arbeitsschritte kann Ihr Service, wenn alle Anforderungen erfüllt sind, als vollständig sichtbar im {{site.data.keyword.Bluemix_notm}}-Katalog definiert werden.


## Welche Schritte müssen zur Bereitstellung eines integrierten Abrechnungsservice ausgeführt werden?

Sie arbeiten mit Provider Workbench (PWB), der Konsole für das Ressourcenmanagement und der Entwicklungsumgebung Ihrer Wahl, um diese Zielsetzungen zu erreichen. Verwenden Sie die [Prüfliste](/docs/third-party/checklist.html#checklist), um diese Schritte zu überwachen.

In den folgenden Schritten wird der Onboarding-Prozess allgemein zusammengefasst:

Bei diesen Schritten wird davon ausgegangen, dass Sie bereits über die Genehmigung zum Bereitstellen eines integrierten Abrechnungsservice verfügen. Sollten Sie die Erstregistrierung und die Genehmigung in Provider Workbench (PWB) noch nicht durchgeführt haben, dann sollten Sie sich mit den Informationen im Abschnitt mit der [Einführung zur Veröffentlichung Ihres Drittanbieterangebots in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md) vertraut machen.
{: tip}

1. [Verfassen: Servicedokumentation und Marketingankündigung verfassen (PWB)](/docs/third-party/cis1-docs-marketing.html).
2. [Definieren: Angebot in der Konsole für das Ressourcenmanagement definieren ({{site.data.keyword.Bluemix_notm}})](/docs/third-party/cis2-rmc-define.html).
3. [Entwickeln: Service-Broker mithilfe der Open Service Broker-API-Spezifikation entwickeln und hosten](/docs/third-party/cis3-broker.html).
4. [IAM: Authentifizierungsablauf (OAuth) entwickeln, Benutzerberechtigung überprüfen (v2/authz) und Weiterleitungs-URI ableiten](/docs/third-party/cis5-iam.html).
5. [Veröffentlichen und Testen: OSB mit Konsole für das Ressourcenmanagement verbinden, Service im Modus für eingeschränkte Sichtbarkeit im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlichen und Angebot testen](/docs/third-party/cis4-rmc-publish.html).
6. [Genehmigung zur Vertriebsfreigabe Ihres Service anfordern](/docs/third-party/cis6-ga.html).

## Support

Für integrierte Abrechnungsservices sind Drittanbieter-Service-Provider erforderlich, die ein eigenes Unterstützungsmodell bereitstellen. Der zuständige IBM Ansprechpartner unterstützt Sie bei der Aktivierung Ihres Unterstützungsmodells und stellt sicher, dass bei Öffnung eines Tickets durch einen Benutzer beim {{site.data.keyword.Bluemix_notm}}-Support der {{site.data.keyword.Bluemix_notm}}-Support das Ticket an die Unterstützungssite des Drittanbieters weiterleitet.

## Fortlaufende Aktualisierungen

Nach Freigabe Ihres Service können Sie fortlaufend Aktualisierungen durchführen, indem Sie direkt mit dem zuständigen {{site.data.keyword.Bluemix_notm}}-Ansprechpartner zusammenarbeiten.



