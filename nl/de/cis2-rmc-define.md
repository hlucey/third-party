---


copyright:
  years: 2018
lastupdated: "2018-07-03"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Schritt 2: Angebot in der Konsole für das Ressourcenmanagement definieren

Die Konsole für das Ressourcenmanagement ist ein webbasiertes Tool, das Sie durch die Bereitstellung Ihres Drittanbieterangebots im {{site.data.keyword.Bluemix_notm}}-Katalog führt.

Nachdem Sie nun über die Genehmigung zur Bereitstellung eines integrierten Abrechnungsservice verfügen, sind Sie bereit, in der Konsole für das Ressourcenmanagement die Registrierung durchzuführen, mit der Entwicklung Ihres Angebots zu beginnen und Ihre Preisstrukturpläne bereitzustellen:
   1. Registrieren Sie Ihren Service bei der Konsole für das Ressourcenmanagement und überprüfen Sie, ob die Daten auf der Seite *Zusammenfassung* korrekt sind.
   2. Geben Sie Ihre Katalogmetadaten auf der Seite *Angebot* ein.
   3. Registrieren Sie Ihr Angebot bei {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Bei der Registrierung werden die Berechtigungsnachweise für die Client- und die Service-ID generiert, die zur Authentifizierung Ihres Service dienen.
   4. Füllen Sie die Seite *Preisstruktur* aus und überprüfen Sie, dass Ihr Serviceangebot in {{site.data.keyword.Bluemix_notm}} den Kunden mit den korrekten Preisstrukturplänen angezeigt wird. Die Pläne, die Sie definieren, umfassen Messungen, in denen wichtige Nutzungsdetails enthalten sind.
   5. Exportieren Sie Ihre Angebotsmetadaten im JSON-Format.


## Vorbereitende Schritte

Bei diesem Schritt wird davon ausgegangen, dass Sie bereits über die Genehmigung zum Bereitstellen eines integrierten Abrechnungsservice verfügen. Sollten Sie die Erstregistrierung und die Genehmigung in Provider Workbench noch nicht durchgeführt haben, dann sollten Sie sich mit den Informationen im [Lernprogramm 'Einführung'](/docs/third-party/index.html) vertraut machen.
{: tip}

1. Vergewissern Sie sich, dass Sie mit dem folgenden Schritt begonnen haben: [Schritt 1: Servicedokumentation und Marketingankündigung verfassen (PWB)](/docs/third-party/cis1-docs-marketing.html).
2. Vergewissern Sie sich, dass Sie die Registrierung bei {{site.data.keyword.Bluemix_notm}} durchgeführt haben. Falls Sie diesen Schritt noch nicht ausgeführt haben, dann führen Sie die [Registrierung](https://console.bluemix.net/registration) durch, bevor Sie fortfahren.
3. Vergewissern Sie sich, dass Sie sich im korrekten Konto befinden, bevor Sie mit dem Arbeiten in der Konsole für das Ressourcenmanagement beginnen.
4. Bereiten Sie Ihren {{site.data.keyword.Bluemix_notm}}-Servicenamen vor.

   Sie müssen sowohl einen Servicenamen angeben, der zur Identifikation des Service durch die {{site.data.keyword.Bluemix_notm}}-Plattform dient, als auch einen Anzeigenamen, der Ihren Kunden im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt wird.

  Wenn Sie die Registrierung für Ihr Angebot bei der Konsole für das Ressourcenmanagement durchführen, dann sollten Sie Ihren {{site.data.keyword.Bluemix_notm}}-Servicenamen bereithalten. Der Servicename stimmt nicht mit dem Anzeigenamen überein. Für die Erstellung des Servicenamens gelten die folgenden Regeln:
   - Es dürfen nur Kleinbuchstaben angegeben werden.
   - Es dürfen keine Leerzeichen im Namen enthalten sein. Bindestriche (`-`) sind hingegen zulässig.
   - Es dürfen nur weniger als 32 Zeichen angegeben werden.

   Ihr Servicename muss den Namen Ihres Unternehmens enthalten. Verfügt Ihr Unternehmen über mehrere Angebote, dann muss der Servicename sowohl das Unternehmen als auch das Angebot enthalten. Beispiel: Das Unternehmen 'Compose' verfügt über Angebote für Redis und Elasticsearch. Die Servicenamen dieser Angebote in {{site.data.keyword.Bluemix_notm}} können `compose-redis` und `compose-elasticsearch` lauten. Beiden Servicenamen sind Anzeigenamen zugeordnet, die im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt werden: *Compose Redis* und *Compose Elasticsearch*. Ein anderes Unternehmen (z. B. FastJetMail) kann über nur ein Angebot mit dem Namen 'JetMail' verfügen. In diesem Fall lautet der Servicename `fastjetmail`.

## Eigenes Angebot registrieren

Melden Sie sich zum Einstieg an und registrieren Sie Ihr Angebot.

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an: [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") und verwenden Sie dazu Ihre {{site.data.keyword.Bluemix_notm}}-ID.
   **Warnung**: Es ist wichtig, dass Sie sich im korrekten {{site.data.keyword.Bluemix_notm}}-Konto befinden. Wenn Sie über mehrere Konten verfügen, dann vergewissern Sie sich, dass Sie das richtige Konto aufrufen.
2. Rufen Sie das Dashboard der Konsole für das Ressourcenmanagement auf: [https://console.bluemix.net/onboarding/dashboard](https://console.bluemix.net/onboarding/dashboard){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
3. Klicken Sie auf **Neue Ressource**, um Ihre Ressource hinzuzufügen.
4. Fügen Sie den Wert für **Ressourcenname** hinzu. Dieser Wert gibt den eindeutigen {{site.data.keyword.Bluemix_notm}}-Servicenamen an, den Sie im vorherigen Abschnitt abgeleitet haben.
5. An diesem Punkt innerhalb des Prozesses ist nicht davon auszugehen, dass Sie bereits über einen gehosteten Service-Broker verfügen. Wählen Sie also im Feld **Ist Ihr Broker bereit für den Import?** die Antwort **Nein** aus. Sie werden in den nachfolgenden Schritten durch die Erstellung eines Brokers geführt und dann wieder zur Konsole für das Ressourcenmanagement zurückkehren, um Ihren Broker zu importieren, nachdem die Entwicklung und das Hosten durchgeführt wurde.
7. Nach der Übergabe wird die Seite **Zusammenfassung** aufgerufen. Geben Sie alle zusätzlich *erforderlichen* Werte ein und klicken Sie dann auf **Speichern**.

Sie können Ihre Arbeitsergebnisse in der Konsole für das Ressourcenmanagement speichern und zu einem späteren Zeitpunkt zu diesen Ergebnissen zurückkehren, um weitere Informationen hinzuzufügen. Die Konsole für das Ressourcenmanagement wurde so konzipiert, dass Sie Unterstützung bei der Verwaltung des Lebenszyklus Ihres Service erhalten. Deswegen ist es unerheblich, wenn Sie zum momentanen Zeitpunkt nicht alle Antworten auf die in den Feldern gestellten Fragen haben.
{: tip}

## Angebotsmetadaten eingeben

Geben Sie auf der Seite **Angebot** die Metadatenwerte an, die im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert sind. Darüber hinaus ist bei einigen dieser Werte ein Export und die Speicherung in Ihrem Service-Broker erforderlich, in dem sie für die Bereitstellung verwendet und als Teil der `Katalog (GET)`-Antwort zurückgegeben werden. Sie verwenden diese Werte in den nachfolgenden Schritten zur raschen Entwicklung eines Service-Brokers.

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Angebot** und dann auf die Registerkarte für die **Listenseite**. Auf der **Listenseite** werden die Metadaten definiert, die im Service-Dashboard Ihres {{site.data.keyword.Bluemix_notm}}-Angebots angezeigt werden. Geben Sie alle erforderlichen Werte an und klicken Sie dann auf **Speichern**. Die Konsole für das Ressourcenmanagement führt eine Erstregistrierung Ihres Service bei {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) durch. Daraufhin wird eine Benachrichtigung angezeigt, in der Sie darüber informiert werden, dass Ihr Service bei IAM registriert wurde. Später werden Sie weitere Aktionen mit IAM ausführen.
2. Klicken Sie auf der Seite 'Angebot' auf die Registerkarte **Einstellungen**.
   1. Geben Sie an, ob für Ihr Angebot die Option **Werden Planänderungen unterstützt?** aktiviert werden soll. Der Standardwert lautet **Nein**. Wenn Sie **Ja** angeben, dann müssen Sie Open Service Broker so erweitern, dass Planänderungen für bereitgestellte Instanzen unterstützt werden. Wenn Ihr Angebot mehrere Pläne unterstützt und wenn Sie möchten, dass Benutzer die Pläne für eine vorhandene bereitgestellte Instanz ändern können, dann müssen Sie die Funktion aktivieren, über die Benutzer ihre Serviceinstanz aktualisieren können. Weitere Details finden Sie unter dem Endpunkt `/v2/service_instances/{instance_id} PATCH` in der [Open Service Broker API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
   2. Geben Sie an, ob für Ihren Service die Option **Bindung möglich** aktiviert werden soll. Der Standardwert ist **Nein**. Wählen Sie **Ja** aus, wenn Ihr Service in {{site.data.keyword.Bluemix_notm}} an Anwendungen gebunden werden kann. Wenn eine Bindung möglich ist, dann muss der Service API-Endpunkte und Berechtigungsnachweise an Ihre Servicekonsumenten zurückgeben können. Bei der Entwicklung eines Service, für den eine Bindung möglich ist, müssen Sie die Informationen im Abschnitt zu den [bindefähigen Operationen in der Open Service Broker-API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") beachten.
   3. Geben Sie die Werte in den zusätzlich erforderlichen Feldern an und klicken Sie dann auf **Speichern**.
3. Auf der Seite 'Angebot' wird nun ein Häkchen in der Navigation angezeigt, das angibt, dass Sie die Mindestanforderungen beim Ausfüllen dieser Seite erfüllt haben. Wird die Seite weiterhin als unvollständig ausgewiesen, dann müssen Sie sie erneut öffnen und auf unvollständig ausgefüllte *erforderliche* Felder überprüfen.

Ihr erstes Anschreiben zu Ihrem Angebot umfasst eine URL für die Servicedokumentation, die von Provider Workbench generiert wurde. Sie müssen diese URL in den Feldern **Dokumentations-URL** und **Anweisungs-URL** eingeben.
{: tip}

## Bei IAM registrieren

IAM ist für das Onboarding aller Services in {{site.data.keyword.Bluemix_notm}} erforderlich. Weitere Informationen hierzu finden Sie im Abschnitt [ Was ist IAM?](/docs/iam/index.html#what-is-cloud-iam-). Dort erfahren Sie mehr über die IAM-Konzepte und -Anforderungen.

Die Konsole für das Ressourcenmanagement generiert die folgenden IAM-Werte:
   - Service-ID (generiert und gespeichert)
   - API-Schlüssel (generiert und nicht gespeichert - wird einmalig angezeigt)
   - Client-ID (generiert und gespeichert)
   - Geheimer Clientschlüssel (generiert und nicht gespeichert)

Der Service-Provider muss folgende Daten angeben:
   - Weiterleitungs-URI (Nach der OSB-Entwicklung kehren Sie zur Konsole für das Ressourcenmanagement zurück. Sie können den Weiterleitungs-URI aus der Position des gehosteten Service-Brokers ableiten.)

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Zugriffsmanagement**.
2. Klicken Sie auf **IAM aktivieren**. Die Konsole für das Ressourcenmanagement registriert Ihren Service bei IAM und erstellt die Service-ID, die Richtlinie und einen API-Schlüssel für Sie. Darüber hinaus wird eine unvollständige Client-ID und ein unvollständiger geheimer Schlüssel erstellt. Die Client-ID muss anhand Ihres Weiterleitungs-URI aktualisiert werden, nachdem dieser zur Verfügung steht.
3. Klicken Sie auf **Status**, um den aktuellen Status Ihrer IAM-Aktivierung anzuzeigen.

**Hinweis**: Sie müssen zu einem späteren Zeitpunkt die IAM-Seite erneut aufrufen, um den `Weiterleitungs-URI` anzugeben. Dieser Wert steht erst dann zur Verfügung, wenn Sie bestimmte zusätzliche Entwicklungsschritte ausgeführt haben, um einen Authentifizierungsablauf zu erstellen. In nachfolgenden Schritten werden Sie durch die Erkennung des Wertes für den Weiterleitungs-URI geführt.

Sie erhalten Ihren API-Schlüssel, wenn Sie **IAM aktivieren**. Es ist wichtig, dass Sie den API-Schlüssel speichern. Der Wert wird nicht erneut angezeigt. Wenn Sie den API-Schlüssel verlieren, dann können Sie ihn löschen und einen neuen API-Schlüssel erstellen: [API-Schlüssel für Service-ID verwalten](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## Preisstrukturplan entwickeln

Wenn Sie das Onboarding Ihres Service in {{site.data.keyword.Bluemix_notm}} durchführen, dann müssen Sie auch einen Preisstrukturplan definieren. Wenn Sie über detailliertes Wissen zur Vorgehensweise bei der Belastung von Benutzern für Ihren Service verfügen, dann können Sie diese Informationen in Ihrem Plan angeben. Wenn Sie sich jedoch noch nicht für einen gebührenpflichtigen Plan entschieden haben, dann können Sie mit der Aktivierung eines kostenlosen Plans beginnen und später einen gebührenpflichtigen Plan einrichten.

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Preisstruktur**.
2. Klicken Sie auf **Plan hinzufügen**, um einen neuen Planeintrag zu erstellen, und klicken Sie dann auf **Plan bearbeiten**, um den Plan zu bearbeiten.
   * **Kostenloser Plan**: Alle Angebote können über einen Lite-Plan verfügen, für den keine Gebühren berechnet werden. Auf diese Weise können Benutzer Ihren Service testen. Kostenlose Pläne verwenden als **Anzeigename** den Wert *Lite* und als **programmorientierten Namen** den Wert *lite*. Geben Sie für **Ist dieser Plan kostenlos?** die Option **Ja** an. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht.
   * **Abonnementplan**: Geben Sie bei diesem Plan für **Ist dieser Plan kostenlos?** die Option **Nein** an. Füllen Sie die erforderlichen Felder aus. Behalten Sie die Standardmetrik **Preisstrukturmetrik** bei. Diese Standardmetrik wird bereitgestellt, damit Sie Benutzern eine einmalige monatliche Gebühr berechnen können. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht. Speichern Sie den curl-Beispielbefehl, um die Nutzungsdaten zu übermitteln.
   * **Nutzungsabhängiger Plan**: Geben Sie bei diesem Plan für **Ist dieser Plan kostenlos?** die Option **Nein** an. Füllen Sie die erforderlichen Felder aus. *Löschen* Sie die standardmäßige Abonnementmetrik **Preisstrukturmetrik**. Klicken Sie auf **Weitere Metrik hinzufügen**, füllen Sie die Seite **Preisstrukturmetrik hinzufügen** aus und klicken Sie auf **Metrik hinzufügen**. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht. Speichern Sie den curl-Beispielbefehl, um die Nutzungsdaten zu übermitteln. Wenn Sie Hilfe bei der Auswahl der richtigen Metriken benötigen, dann lesen Sie die Informationen unter [Messungsintegration](/docs/third-party/metering.html).
3. Die Seite **Preisstruktur** wird nun als vollständig ausgewiesen. Damit wird angegeben, dass Sie die Mindestanforderungen beim Ausfüllen dieser Seite erfüllt haben.

Service-Provider müssen die stündliche Übermittlung der Nutzungsdaten für alle nutzungsabhängigen Pläne automatisieren. Weitere Informationen finden Sie im Abschnitt [Nutzungsdaten für nutzungsabhängige Pläne übermitteln](/docs/third-party/submitusage.html).
{: tip}

## Metadaten im JSON-Format exportieren

 Nachdem Sie Ihren Service nun in der Konsole für das Ressourcenmanagement definiert haben, können Sie die Datei mit dem Namen 'catalog.json' herunterladen und sie verwenden, um die Entwicklung Ihres Open Service Broker zu informieren. Die Datei 'catalog.json' enthält Metadaten, die im Broker gehostet werden müssen. Diese Werte definieren den Vertrag zwischen dem Broker und der {{site.data.keyword.Bluemix_notm}}-Plattform für die Services und Pläne, die vom Broker unterstützt werden. Alle zusätzlichen Katalogmetadaten, die nicht zur Bereitstellung erforderlich sind, werden im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert. Alle Aktualisierungen an den Kataloganzeigewerten, die zur Darstellung Ihres Dashboards verwendet werden (z. B. Links, Symbole und mit i18n umgesetzte Metadaten) müssen in der Konsole für das Ressourcenmanagement aktualisiert werden und dürfen nicht in Ihrem Broker abgelegt werden. Keine der in Ihrem Broker gespeicherten Metadaten werden in der {{site.data.keyword.Bluemix_notm}}-Konsole oder der {{site.data.keyword.Bluemix_notm}}-CLI angezeigt. Die Konsole und die CLI geben die Daten zurück, die in der Konsole für das Ressourcenmanagement festgelegt und im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert wurden.

1. Öffnen Sie in der Konsole für das Ressourcenmanagement die Seite **Bereitstellungen**.
2. Klicken Sie auf **Verwalten**.
3. Klicken Sie auf **Definitionen herunterladen**.

Speichern Sie die Datei `catalog.json`. Sie werden sie bei der Open Service Broker-Entwicklung im nächsten Abschnitt verwenden.

## Nächste Schritte

Gut gemacht! Sie haben Ihr Serviceangebot definiert, indem Sie die Metadaten für die Kataloganzeige hinzugefügt, die Registrierung bei IAM durchgeführt und mindestens einen Preisstrukturplan erstellt haben. Als Nächstes können Sie mithilfe der exportieren JSON-Datei mit der Entwicklung eines Service-Brokers beginnen. Weitere Informationen hierzu finden Sie in [Schritt 3: Service-Broker entwickeln und hosten](/docs/third-party/cis3-broker.html).
