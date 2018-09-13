---


copyright:
  years: 2018
lastupdated: "2018-08-23"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Schritt 3. Service-Broker entwickeln und hosten
{: #step3-osb}

Mithilfe der von Ihnen aus der Konsole für das Ressourcenmanagement exportierten Metadaten können Sie nun mindestens einen neuen Service-Broker in der Programmiersprache Ihrer Wahl erstellen.
{:shortdesc}

Service-Broker verwalten den Lebenszyklus von Services. Die {{site.data.keyword.Bluemix_notm}}-Plattform interagiert mit Service-Brokern, um so Serviceinstanzen (Instanziierung eines Serviceangebots) und Servicebindungen (Darstellung einer Zuordnung zwischen einer Anwendung und einer Serviceinstanz, in der häufig die Berechtigungsnachweise enthalten sind, die die Anwendung zur Kommunikation mit der Serviceinstanz verwendet) bereitzustellen und zu verwalten. Wenn Sie gültige Metadatenwerte angeben, dann können Sie erfolgreich eine REST-konforme API-Antwort erstellen, wenn eine Anforderung ausgeführt wird.

Beginnen Sie die Erstellung Ihres Brokers, indem Sie eine Kombination aus den von Ihnen aus der Konsole für das Ressourcenmanagement exportierten Metadaten, den von IBM bereitgestellten öffentlichen {{site.data.keyword.Bluemix_notm}}-Service-Broker-Beispielen und der API-Dokumentation für Ressourcenbroker verwenden.

## Vorbereitende Schritte
{: #pre-reqs}

Vergewissern Sie sich, dass Sie mit Schritt 1 begonnen und Schritt 2 abgeschlossen haben:
1. [Servicedokumentation und Vertriebsfreigabe verfassen](/docs/third-party/cis1-docs-marketing.html).
2. [Angebot in der Konsole für das Ressourcenmanagement definieren](/docs/third-party/cis2-rmc-define.html).


## Szenario für {{site.data.keyword.Bluemix_notm}}-Plattformbereitstellung anzeigen
{: #scenario}

Sie werden einen Open Service Broker entwickeln, der mit der {{site.data.keyword.Bluemix_notm}}-Plattform arbeitet. Anhand des [Bereitstellungsszenarios](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together) können Sie sich mit der Vorgehensweise zur Ressourcenerstellung vertraut machen.

## Einarbeitung in OSB-Spezifikation durchführen
{: #learn-osb}

{{site.data.keyword.Bluemix_notm}} verwendet die Spezifikation für die Open Service Broker-API (OSB) `Version 2.12`. Lesen Sie die [Open Broker API-Spezifikation](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") und machen Sie sich mit ihrem Inhalt vertraut. Verwenden Sie die Readme-Datei als Leitfaden für weiterführende Informationen.

## {{site.data.keyword.Bluemix_notm}}-Brokerbeispiele anzeigen
{: #samples}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")

**Hinweis:** Nicht für alle Sprachen steht ein Beispiel zur Verfügung. Wenn Sie beispielsweise einen Python-Beispielbroker benötigen, sollten Sie über Google ein Cloud Foundry-Beispiel suchen. Sie müssen dieses Beispiel möglicherweise anpassen, um die OSB-Anforderungen zu erfüllen.


## {{site.data.keyword.Bluemix_notm}} Open Service Broker-API-Dokumentation anzeigen
{: #docs}

Zur Entwicklung von Service-Brokern sollten Sie über Kenntnisse zum Thema [{{site.data.keyword.Bluemix_notm}} Open Service Broker-API](https://console.bluemix.net/apidocs/ibm-cloud-osb-api){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") verfügen. Machen Sie sich mit der Broker-API und der Art und Weise vertraut, in der die Interaktion der API mit Ihren Brokern erfolgt.

Der {{site.data.keyword.Bluemix_notm}} Open Service Broker erweitert die Version 2.12 der Open Service Broker-Spezifikation.
{: tip}

### Erforderliche Endpunktlogik für alle Service-Broker

Service-Broker müssen eine Standardgruppe von Metadatenwerten bereitstellen, die von den REST-APIs benutzt werden. Außerdem müssen {{site.data.keyword.Bluemix_notm}}-Broker Logik für die folgenden REST-API-Endpunkte und -Pfade enthalten:

<dl>
  <dt>Katalog (GET)</dt>
  <dd>Gibt die Katalogmetadaten zurück, die in Ihrem Broker enthalten sind. Es stehen zahlreiche zusätzliche Katalogmetadatenwerte zur Verfügung, die nicht zurückgegeben werden. Diese Werte werden ausschließlich in der Konsole für das Ressourcenmanagement hinzugefügt und im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert.</dd>
  <dt>Ressourceninstanzen (PUT)</dt>
  <dd>Bereitstellung Ihrer Serviceinstanz</dd>
  <dt>Ressourceninstanzen (DELETE)</dt>
  <dd>Aufheben der Bereitstellung Ihrer Serviceinstanz</dd>
  <dt>Ressourceninstanzen (PATCH)</dt>
  <dd>Aktualisierung Ihrer Serviceinstanz</dd>
</dl>

**Hinweis zu 'Katalog (GET)'**: Dieser Endpunkt definiert den Vertrag zwischen dem Broker und der {{site.data.keyword.Bluemix_notm}}-Plattform für die Services und Pläne, die vom Broker unterstützt werden. Dieser Endpunkt gibt die Katalogmetadaten zurück, die in Ihrem Broker gespeichert sind. Diese Werte definieren den mindestens erforderlichen Bereitstellungsvertrag zwischen Ihrem Service und der {{site.data.keyword.Bluemix_notm}}-Plattform. Alle zusätzlichen Katalogmetadaten, die nicht zur Bereitstellung erforderlich sind, werden im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert. Alle Aktualisierungen an den Kataloganzeigewerten, die zur Darstellung Ihres Dashboards verwendet werden (z. B. Links, Symbole und mit i18n umgesetzte Metadaten) müssen in der Konsole für das Ressourcenmanagement aktualisiert werden und dürfen nicht in Ihrem Broker abgelegt werden. Keine der in Ihrem Broker gespeicherten Metadaten werden in der {{site.data.keyword.Bluemix_notm}}-Konsole oder der {{site.data.keyword.Bluemix_notm}}-CLI angezeigt. Die Konsole und die CLI geben die Daten zurück, die in der Konsole für das Ressourcenmanagement festgelegt und im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert wurden. Hierbei handelt es sich um die mindestens erforderlichen Werte, die dieser Katalog (GET) zurückgeben sollte:

```
{
       "services":[
   {
           "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### Erforderliche Endpunktlogik für bindefähige Services

Wenn Ihr Service an Anwendungen in {{site.data.keyword.Bluemix_notm}} gebunden werden kann, dann muss er in der Lage sein, API-Endpunkte und Berechtigungsnachweise an Ihre Servicekonsumenten zurückzugeben. Ein bindefähiger Service muss die bindefähigen Operationen in der Open Service Broker-Spezifikation verwenden und die folgenden Endpunkte und Pfade implementieren:

<dl>
  <dt>Bindungen und Berechtigungsnachweise (PUT)</dt>
  <dd>Bindung Ihrer Serviceinstanz an eine Anwendung.</dd>
  <dt>Bindungen und Berechtigungsnachweise (DEL)</dt>
  <dd>Aufheben der Bindung Ihrer Serviceinstanz an eine Anwendung.</dd>
</dl>

### Erforderliche {{site.data.keyword.Bluemix_notm}}-Erweiterungsendpunkte

Die OSB-Spezifikation bietet *keine* Unterstützung für einen inaktivierten Instanzstatus, der jedoch noch nicht gelöscht wurde. Damit {{site.data.keyword.Bluemix_notm}} Kunden unterstützen kann, bei denen es möglicherweise zu Zahlungsverzögerungen oder zu anderen Situationen kommt, die zu einer Aussetzung des Kontos (jedoch nicht zum Abbruch) führen können, hat {{site.data.keyword.Bluemix_notm}} erweiterte API-Endpunkte definiert, die es Ihnen ermöglichen, Serviceinstanzen zu inaktivieren und erneut zu aktivieren. Die folgenden Endpunkterweiterungen sind **erforderlich**:

<dl>
  <dt>Instanzen aktivieren und inaktivieren (GET)</dt>
  <dd>Status - Gibt den Status Ihrer Serviceinstanz zurück.</dd>
  <dt>Instanzen aktivieren und inaktivieren (PUT)</dt>
  <dd>Ermöglicht das Aktivieren oder Inaktivieren einer Serviceinstanz.</dd>
</dl>

**Hinweis**: Die Inaktivierung des Zugriffs auf die Serviceinstanz bei Aufruf des Inaktivierungsendpunkts und die erneute Aktivierung des Zugriffs bei Aufruf des Aktivierungsendpunkts liegt im Verantwortungsbereich des Service-Providers.

## Informationen zur Verwendung der exportierten Metadaten als Leitfaden für die Brokerentwicklung
{: #use-metadata}

Die von Ihnen aus der Konsole für das Ressourcenmanagement exportierten Metadaten können als Leitfaden für die Entwicklung eines eigenen Brokers verwendet werden. Nicht alle von Ihnen an der Konsole für das Ressourcenmanagement eingegebenen Werte sind zur Bereitstellung eines Service erforderlich. Die Metadaten, die Sie aus der Konsole für das Ressourcenmanagement exportiert haben, definieren den mindestens erforderlichen Bereitstellungsvertrag zwischen Ihrem Service und der {{site.data.keyword.Bluemix_notm}}-Plattform. Ihre exportierte JSON-Datei muss die folgenden Werte enthalten:

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - GUID generated by http://www.guidgenerator.com
                    // TODO - This service id must be unique within an IBM Cloud environment's set of service offerings
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - Ensure this value is accurate for your service. Requires PATCH of /v2/service_instances/:instance_id below if true
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - GUID generated by http://www.guidgenerator.com
                            // TODO - This service plan id must be unique within an IBM Cloud environment's set of service plans
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - This service plan name must be unique within the containing service definition
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


Ihr OSB-Servicearray muss exakt mit den Angebotsmetadaten übereinstimmen, die Sie zur Konsole für das Ressourcenmanagement hinzugefügt haben. Um sicherzustellen, dass zwischen OSB und der Konsole für das Ressourcenmanagement eine Eins-zu-eins-Parität besteht, müssen Sie unbedingt den Servicearray in der Datei `catalog.json`, die Sie aus der Konsole für das Ressourcenmanagement heruntergeladen haben, mit dem tatsächlichen Servicearray im Broker vergleichen. Alle Service- und Plan-IDs und -Namen müssen übereinstimmen.
{: tip}

## Von der {{site.data.keyword.Bluemix_notm}}-Plattform bereitgestellte Brokerinformationen
{: #broker info}

Ihre Service-Broker oder Broker empfangen die folgenden Informationen von der {{site.data.keyword.Bluemix_notm}}-Plattform:

### X-Broker-API-Originating-Identity

Der **Benutzeridentitätsheader** wird über einen Identitätsheader der API bereitgestellt. Dieser Anforderungsheader enthält die  {{site.data.keyword.Bluemix_notm}}-IAM-Identität des Benutzers. Die IAM-Identität verfügt über eine Base64-Codierung. {{site.data.keyword.Bluemix_notm}} unterstützt einen einzelnen Authentifizierungsrealm: `IBMid`. Der Realm `IBMid` verwendet eine eindeutige IBMid-ID (IUI = IBMid Unique ID)), um die Identität des Benutzers in {{site.data.keyword.Bluemix_notm}} zu ermitteln. Diese IUI stellt für den Service-Provider eine nicht transparente Zeichenfolge dar.

Beispiel:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### Version des API-Headers

Der **Header der API-Version** lautet [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link"). Beispiel: `X-Broker-Api-Version: 2.12`.

### Ressourceninstanz (PUT) body.context und Ressourceninstanz (PATCH) body.context

`PUT /v2/service_instances/:resource_instance_id` und `PATCH /v2/service_instances/:resource_instance_id` empfangen den folgenden Wert in **body.context**: `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`.

## Zusätzliche Brokerempfehlungen
{: #more-info}

### Empfehlungen zur Verwendung asynchroner oder synchroner Operationen

Die OSB-API unterstützt sowohl den synchronen als auch den asynchronen Betriebsmodus. Wenn die Operationen weniger als 10 Sekunden in Anspruch nehmen, dann werden synchrone Antworten empfohlen.  Andernfalls sollte der asynchrone Betriebsmodus verwendet werden.  Weitere Informationen zu diesem Thema sind in der OSB-Spezifikation enthalten.

Wenn die asynchrone Operation für den Versuch, eine Instanz bereitzustellen, weniger als 10 Sekunden dauert, dann tritt auf der Plattform eine Zeitlimitüberschreitung auf.
{: tip}

### Empfehlungen für die positionsübergreifende Verwaltung von Brokern

Für Benutzer ist es wichtig, die Gegebenheiten der Position für ihre Cloud-Services in Bezug auf die Latenzzeiten, die Verfügbarkeit und den Datenspeicherort zu kennen.

Bei der Bereitstellung von Serviceinstanzen in {{site.data.keyword.Bluemix_notm}} stellt einer der erforderlichen Parameter, die von den Benutzern angegeben werden müssen, die Position dar, an der die betreffende Serviceinstanz bereitgestellt werden soll. Bestimmte Services unterstützen die Bereitstellung an mehreren Positionen. Ein Datenbankservice kann z. B. die Bereitstellung in allen {{site.data.keyword.Bluemix_notm}}-Regionen oder in einer bestimmten Untergruppe unterstützen.

Wenn Ihr API-basierter Drittanbieterservice in einer anderen Cloud implementiert wurde und in {{site.data.keyword.Bluemix_notm}} zugänglich gemacht wurde, dann muss die Position die Position des Service in der anderen Cloud angeben.

Beim Onboarding in {{site.data.keyword.Bluemix_notm}} müssen Sie mindestens einen OSB-Broker implementieren. Sie haben jedoch die Option, abhängig von Ihrer Bereitstellungsstrategie und den Positionen, die Sie für Ihren Service unterstützen wollen, mit mehreren Brokern zu arbeiten.  Im Tool der Konsole für das Ressourcenmanagement haben Sie die Zuordnung zwischen Ihrem Service, dem Plan und dem Positionstupel und dem Broker eingerichtet, der die Operationen für diesen Tupel bedient. Die typischen Optionen bestehen im Definieren eines einzelnen Brokers, der alle Positionen für Ihren Service bedient, oder in der Definition eines Brokers pro Position. Die gewählte Option wird vom jeweiligen Service-Provider festgelegt.

Eine Liste der verfügbaren Positionen finden Sie unter den [IBM Global Catalog Locations](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link"). Wenn für Ihren Service zusätzliche Positionen im globalen Katalog definiert werden müssen, dann wenden Sie sich an das {{site.data.keyword.Bluemix_notm}}-Onboarding-Team.


## Eigene Broker hosten
{: #host}

Ihr Broker muss als Bestandteil einer Anwendung gehostet werden, die auf REST-API-Aufrufe reagieren kann. Ihre gehostete Position muss den {{site.data.keyword.Bluemix_notm}}-Sicherheitsrichtlinien entsprechen. Sie können das Hosting in {{site.data.keyword.Bluemix_notm}} oder extern durchführen, solange öffentlicher Zugriff über {{site.data.keyword.Bluemix_notm}} besteht.

Zum IBM externen Hosten des Brokers müssen Sie sicherstellen, dass die folgenden Sicherheitsrichtlinien erfüllt sind:
- Einhaltung des TLS-Protokolls (Transport Layer Security) Version 1.2
- Hosting auf einem gültigen HTTPS-Endpunkt, auf den über das öffentliche Internet zugegriffen werden kann

Wenn das Hosting in {{site.data.keyword.Bluemix_notm}} durchgeführt werden soll, dann sollten Sie die Informationen zum Erstellen einer App mithilfe von Containern (Kubernetes) lesen: [Interne Adopter - Nutzungsinformationen](/docs/containers/cs_internal.html#cs_internal).

Sie benötigen die gehostete Position Ihres Service-Brokers, um den nächsten Schritt ausführen zu können. Halten Sie die URL und die Berechtigungsnachweise Ihrer App bereit, bevor Sie mit dem nächsten Schritt fortfahren.
{: tip}

## Vorgehensweise zum Testen des Service-Brokers
{: #test}

Sie müssen Ihren Broker überprüfen, indem Sie die curl-Befehle für die unterschiedlichen Endpunkte ausführen, die Sie aktivieren wollen. Die Beispiel-Readme-Datei enthält hervorragende Anweisungen zur Verarbeitung Ihrer OSB-Endpunkte mit curl: https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### Vorgehensweise zur Bearbeitung des Service-Brokers mit curl

Verwenden Sie das folgende Beispiel, um die curl-Antwort Ihrer Broker zu testen:

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## Nächste Schritte

Sie verfügen nun über fundierte Kenntnisse! Sie haben soeben einen Service-Broker erstellt und gehostet, der der OSB-Spezifikation entspricht. Weitere Informationen finden Sie in [Schritt 4: Authentifizierungsablauf entwickeln](/docs/third-party/cis5-iam.html).
