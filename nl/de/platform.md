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
{:note: .note}
{:download: .download}

# Vorgehensweise zur Verwendung der {{site.data.keyword.Bluemix_notm}}-Plattform durch integrierte Abrechnungsservices
{: #how-it-works}

Integrierte Abrechnungsservices unterscheiden sich von Empfehlungsservices. Ein integrierter Abrechnungsservice verwendet die {{site.data.keyword.Bluemix_notm}}-Plattform zur Authentifizierung, für den Zugriff, die Bereitstellung, die Messung und die Abrechnung. Im vorliegenden Abschnitt wird ein allgemeiner Überblick über die Plattformkomponenten gegeben, die von Ihrem integrierten Abrechnungsservice verwendet werden.

## {{site.data.keyword.Bluemix_notm}}-Bereitstellungsebene
{: #provisioning-layer}

Die Bereitstellungsebene verwaltet den Lebenszyklus von {{site.data.keyword.Bluemix_notm}}-Ressourcen. Die Bereitstellungsebene ist für die Steuerung und Überwachung des Lebenszyklus von Ressourcen in einem Kundenkonto verantwortlich. Bei *Ressourcen* handelt es sich um physische und logische Komponenten, die für eine Anwendung oder eine Serviceinstanz bereitgestellt oder reserviert werden können. Zu den Beispielen für Ressourcen gehören Datenbanken und Konten, Prozessoren, Speicher und Speichergrenzwerte. Im Allgemeinen dienen Ressourcen, die in der Bereitstellungsebene überwacht werden, der Zuordnung von Nutzungsmetriken und Abrechnungen, dies ist jedoch nicht zwingend erforderlich. In bestimmten Fällen kann die Ressource der Bereitstellungsebene zugeordnet werden, um sicherzustellen, dass der Lebenszyklus der Ressource zusammen mit dem Lebenszyklus des Kontos verwaltet werden kann.

### Verwaltung des Lebenszyklus von Ressourcen
{: #lifecycle}

Die Bereitstellungsebene stellt allgemeine APIs zur Verfügung, mit denen der Lebenszyklus von Ressourcen von der Bereitstellung (Instanzerstellung) über die Bindung (Erstellung der Zugriffsberechtigungsnachweise) und die Aufhebung der Bindung (Entfernung des Zugriffs) bis hin zur Aufhebung der Bereitstellung (Instanzlöschung) gesteuert werden kann. Darüber hinaus stellt die {{site.data.keyword.Bluemix_notm}}-Plattform CLIs und eine Benutzerschnittstelle zur Verwaltung des Lebenszyklus dieser Ressourcen bereit, sodass Sie keine eigenen Verwaltungsfunktionen erstellen müssen.

Die Bereitstellungsebene stellt APIs zur Verfügung, mit denen Sie die folgenden Elemente im Lebenszyklus von Ressourcen verwalten können:
* Bereitstellung
* Aktualisierung einer Ressourceninstanz
* Bindung
* Ressourcenschlüssel
* Aufhebung der Bindung
* Aufhebung der Bereitstellung

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)
{: #iam}

Identity Access Management (IAM) ermöglicht Ihnen die sichere Authentifizierung von Benutzern und die einheitliche Steuerung des Zugriffs auf alle Cloudressourcen in {{site.data.keyword.Bluemix_notm}}. Die {{site.data.keyword.Bluemix_notm}}-Bereitstellungsebene hat IAM für die Authentifizierung und Berechtigung von Aktionen ausgewählt, die für die Bereitstellungsebene ausgeführt werden. Provider von Drittanbieterangeboten verwenden IAM zur Erstellung eines Authentifizierungsablaufs (OAuth). Weitere Informationen hierzu finden Sie in [Was ist IAM?](/docs/iam?topic=iam-iamoverview#iamoverview).

Wenn Ihr Angebot OIDC-Bibliotheken (OpenID Connect) verwendet, dann unterstützt IAM die OIDC-Integration. Bei OIDC handelt es sich um eine Authentifizierungsebene, die auf dem Berechtigungsframework OAuth 2.0 basiert und zur Vereinfachung des Onboarding-Prozesses beitragen kann. Weitere Informationen zu OIDC finden Sie in [OpenID Connect](http://openid.net/connect/){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

## {{site.data.keyword.Bluemix_notm}}-Katalog
{: #catalog}

Der {{site.data.keyword.Bluemix_notm}}-Katalog dient zur Speicherung der Angebotsdefinitionen (Beschreibung, Funktionen, Bilder, URLs usw.) der Ressourcen, die an der {{site.data.keyword.Bluemix_notm}}-Konsole angezeigt werden. Die Konsole für das Ressourcenmanagement wird zum Definieren aller Aspekte der erforderlichen Metadaten Ihres Service verwendet. Diese Metadaten werden im Katalog veröffentlicht und für die Anzeige im Katalog verwendet. Ausführliche Informationen zu den erforderlichen und optionalen Metadatenfeldern finden Sie auf den Seiten **Angebot** und **Plan** der Konsole für das Ressourcenmanagement. Hier werden jedoch die wichtigsten Elemente aufgeführt, um Ihnen einen raschen Einstieg zu ermöglichen.

   * Servicename: Technischer Name Ihres Service. Der Servicename ist wichtig und muss korrekt definiert werden. Sie müssen sowohl einen Servicenamen angeben, der zur Identifikation des Service durch die {{site.data.keyword.Bluemix_notm}}-Plattform dient, als auch einen Anzeigenamen, der Ihren Kunden im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt wird. Der Servicename stimmt nicht mit dem Anzeigenamen überein.
   * Anzeigename des Service: Der benutzerfreundliche Name Ihres Service. Beispiel: "Compose Redis"
   * Service-ID: Die GUID für Ihren Service, die in API-Aufrufen an den Open Service Broker (OSB) verwendet wird. Dieser Wert muss eindeutig sein.
   * Servicesymbol: Ein SVG-Element mit Ihrem Servicelogo.
   * Servicebeschreibung: Die Beschreibung der Ressource, die angezeigt wird, wenn Sie den Mauszeiger über das Ressourcensymbol in der Benutzerschnittstelle des {{site.data.keyword.Bluemix_notm}}-Katalogs bewegen. Sie können für die Beschreibung einen einzelnen Satz oder Ausdruck hinzufügen.
   * Detaillierte Servicebeschreibung: Der erste Abschnitt, der auf der Kataloglistenseite aufgeführt wird. Ziehen Sie als detaillierte Beschreibung mindestens zwei Sätze in Betracht.
   * Dokumentations-URL: Ein Link zu Ihrer {{site.data.keyword.Bluemix_notm}}-Dokumentation. Diese Informationen werden in Provider Workbench (PWB) verfasst und Ihr URL-Wert wird von PWB generiert.
   * Bedingungs-URL: Ein Link zu den Bedingungen für die Nutzung Ihres Service. Beachten Sie dabei, dass für GDPR-Zwecke kein Link zu den vorhandenen Bedingungen für Drittanbieterservices hergestellt werden darf. Stattdessen müssen Sie eine eindeutige Seite für einen integrierten Abrechnungsservice bereitstellen.
   * Anweisungs-URL: Ähnlich wie bei der Dokumentations-URL wird hier auf Ihre {{site.data.keyword.Bluemix_notm}}-Dokumentation verwiesen. Die Anweisungs-URL überführt Ihre Dokumentation jedoch dynamisch auf die Registerkarte 'Einführung' Ihres Service-Dashboards.
   * Kategorie: Die Auswahl der verfügbaren {{site.data.keyword.Bluemix_notm}}-Kategorien, unter denen Ihr Service in den Katalog aufgenommen wird.
   * Listenpunkte: Kurze beschreibende Highlights zu Ihrem Service.
   * Medien: Screenshots und Videos zu Ihrem Service.
   * Name des Serviceplans: Jeder Plan verfügt über einen technischen Namen. Der Name wird vollständig in Kleinschreibung und ohne Leerzeichen eingegeben. Er darf jedoch das Zeichen "-" enthalten. Beispiel: `gold`.
   * Anzeigename des Serviceplans: Der benutzerfreundliche Name des Plans. Beispiel: `Gold`
   * Serviceplan-ID: Die GUID für Ihren Serviceplan, die in API-Aufrufen an den Open Service Broker verwendet wird. Dieser Wert muss eindeutig sein. Die Konsole für das Ressourcenmanagement generiert diesen Wert für Sie.
   * Serviceplanbeschreibung: Die Beschreibung des Ressourcenplans. Die Beschreibung wird angezeigt, nachdem Sie einen Plan auf der Ressourcendetailseite im IBM Cloud-Katalog ausgewählt haben.
   * Listenpunkte für Servicepläne: Kurze beschreibende Highlights zu Ihrem Serviceplan.


## Open Service Broker
{: #open-service}

Service-Broker verwalten den Lebenszyklus von Services. Die {{site.data.keyword.Bluemix_notm}}-Plattform interagiert mit Service-Brokern, um Serviceinstanzen (Instanziierung eines Serviceangebots) und Servicebindungen (Darstellung einer Zuordnung zwischen einer Anwendung und einer Serviceinstanz, die häufig die Berechtigungsnachweise enthält, die von der Anwendung zur Kommunikation mit der Serviceinstanz verwendet werden) bereitzustellen und zu verwalten. Wenn Sie gültige Metadatenwerte angeben, dann können Sie erfolgreich eine REST-API-Antwort erstellen, wenn eine Anforderung ausgeführt wird.

{{site.data.keyword.Bluemix_notm}} verwendet die Spezifikation für die Open Service Broker-API (OSB) `Version 2.12`. Lesen Sie die [Open Broker API-Spezifikation](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") und machen Sie sich mit ihrem Inhalt vertraut. Verwenden Sie die Readme-Datei als Leitfaden für weiterführende Informationen.

Wenn der Resource Controller eine Anforderung zur Bereitstellung einer Ressource empfängt, dann wird der Open Service Broker aufgerufen, um den Servicetyp, das Angebot, die Pläne und die Regionenverfügbarkeit zu überprüfen. Der Resource Controller überprüft außerdem die Sichtbarkeit des Plans, der dem Kundenkonto zugeordnet ist. {{site.data.keyword.Bluemix_notm}} stellt Brokerbeispiele und API-Dokumentation zur Verfügung, mit denen die OSB-Spezifikation erweitert werden kann. Weitere Einzelheiten zur Entwicklung sowie zum Hosting Ihres Brokers erhalten Sie, während Sie die detaillierten Schritte zur Entwicklung des Onboardings für die integrierte Abrechnung ausführen.

## {{site.data.keyword.Bluemix_notm}}-Messservice
{: #metering-service}

Wenn für einen Service ein Plan mit Nutzungsmessung angeboten wird, werden die Gebühren von {{site.data.keyword.Bluemix_notm}}-Benutzern auf Basis des Ressourcenvolumens berechnet, das von den Benutzern genutzt wird. Für {{site.data.keyword.Bluemix_notm}}-Benutzer, die Datenbankservices nutzen, werden die Gebühren beispielsweise auf Basis der Speicherkapazität berechnet, die von den Anwendungen der Benutzer verbraucht wird. Die Übermittlung von Nutzungsdaten ist erforderlich, um die Nutzungsdaten in einen Datensatz umzuwandeln, auf dessen Basis die Belastung erfolgen kann.

Alle integrierten Abrechnungsservices mit einem Plan mit Nutzungsmessung müssen den {{site.data.keyword.Bluemix_notm}}-Messservice verwenden, um die Nutzungsdaten zu melden.

Sie müssen die stündliche Übermittlung von Nutzungsdaten mithilfe der Messservice-API automatisieren, wenn Sie einen Plan mit Nutzungsmessung anbieten. 

Weitere Informationen zu Messungen finden Sie in [Messungsintegration](/docs/third-party?topic=third-party-meteringintera#meteringintera). Weitere Informationen zur Übermittlung der gemessenen Nutzungsdaten finden Sie in [Nutzungsdaten für Pläne mit Nutzungsmessung übermitteln](/docs/third-party?topic=third-party-submitusage#submitusage). 

## Bereitstellungsszenario: Zusammenfassung
{: #provision2}

Im Folgenden werden alle Konzepte zusammengefasst und es wird anhand eines Beispiels betrachtet, wie Serviceinstanzen mithilfe der {{site.data.keyword.Bluemix_notm}}-Plattform erstellt werden können.

![Bereitstellungsszenario](images/flow-am.svg "Abläufe auf der Plattform beim Erstellen von Serviceinstanzen")

Wenn ein Benutzer eine Serviceinstanz erstellen möchte, stehen die folgenden Vorgehensweisen zur Auswahl:
* **CLI**: Verwendung von `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`.
* **{{site.data.keyword.Bluemix_notm}}-Konsole**: Der Benutzer kann den Service und den Plan auswählen und anschließend die Operation **Erstellen** ausführen.

Auf der {{site.data.keyword.Bluemix_notm}}-Plattform wird überprüft, ob der Benutzer über die erforderliche Berechtigung zur Erstellung der Serviceinstanz mithilfe von {{site.data.keyword.Bluemix_notm}} IAM verfügt. Nach Abschluss der Überprüfung wird der Bereitstellungsendpunkt des Service-Brokers (PUT /v2/resource_instances/:resource_instance_id) gestartet. Bei der Bereitstellung müssen die folgenden Regeln beachtet werden:
* Der {{site.data.keyword.Bluemix_notm}}-Kontext ist in der Kontextvariablen enthalten.
* `X-Broker-API-Originating-Identity` ist die IBM IAM-ID des Benutzers zugeordnet, der die Anforderung gestartet hat.
* Der Abschnitt für die Parameter enthält die erforderliche Position (sowie zusätzliche Parameter, die für den Service erforderlich sind).

Beispiel für Bereitstellungsanforderung:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // your service's GUID from onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //your plan's GUID from onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parameter required by your service"
      }
    }
```

### {{site.data.keyword.Bluemix_notm}}-Parameter `context` verstehen
{: #parameter}

Im vorherigen Beispiel wurden die Metadaten dargestellt, die im Parameter `context` zurückgegeben werden. Der Bereitstellungskontext für {{site.data.keyword.Bluemix_notm}} gibt Folgendes zurück:

* **Plattform**: Identifiziert die Plattform als "ibmcloud".

* **"account_id"**: Gibt die ID des Kontos in {{site.data.keyword.Bluemix_notm}} zurück, das die Serviceinstanz bereitstellt.

* **crn**: Wenn ein Kunde Ihren Service in {{site.data.keyword.Bluemix_notm}} bereitstellt, dann wird eine Serviceinstanz erstellt und diese Instanz wird anhand des {{site.data.keyword.Bluemix_notm}}-Ressourcennamens (CRN) identifiziert. Der CRN (Cloud Resource Name) wird für alle Aspekte der Interaktion mit {{site.data.keyword.Bluemix_notm}} einschließlich der Bereitstellung, Bindung (Erstellung von Berechtigungsnachweisen und Endpunkten), der Messung, der Dashboardanzeige sowie der Zugriffssteuerung verwendet. Aus Sicht des Angebotsproviders kann der CRN in der Regel als eine nicht transparente Zeichenfolge behandelt werden, die für die {{site.data.keyword.Bluemix_notm}}-APIs verwendet werden kann. Außerdem kann er mithilfe der folgenden Struktur zerlegt werden:

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   Im Bereitstellungsbeispiel ist ersichtlich, dass der Service-CRN `compose-redis` wie folgt dargestellt wird:

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   Im vorliegenden Beispiel ist diese Instanz von `compose-redis` Teil des {{site.data.keyword.Bluemix_notm}}-Kontos mit ID. Die eindeutige ID für die Instanz lautet `416d769b-682d-4833-8bd7-5ef8778e5b52` und die Instanz wird in der Region `us-south` (Vereinigte Staaten (Süden)) des öffentlichen {{site.data.keyword.Bluemix_notm}}-Systems gehostet.

* **resource_group_crn**: Gibt die Ressourcengruppe zurück, die die Serviceinstanz beinhaltet. Weitere Einzelheiten finden Sie in [Ressourcengruppen verwalten](/docs/resources?topic=resources-rgs#rgs).

   Angebotsprovider müssen von einigen speziellen Ausnahmen abgesehen den Ressourcengruppen-CRN (`resource_group_crn`) nicht berücksichtigen. Wenden Sie sich an den zuständigen IBM Ansprechpartner für Ihren Anwendungsfall, bevor Sie dieses Feld verwenden.
   {: note}

