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

# Schritt 2. Angebot in der Konsole für das Ressourcenmanagement definieren
{: #step2-define}

Die Konsole für das Ressourcenmanagement ist ein Tool, das Sie durch die Bereitstellung Ihres Drittanbieterangebots im {{site.data.keyword.Bluemix_notm}}-Katalog führt.
Nachdem Sie nun über die Genehmigung zur Bereitstellung eines integrierten Abrechnungsservice verfügen, sind Sie bereit, in der Konsole für das Ressourcenmanagement die Registrierung Ihres Service durchzuführen, mit der Entwicklung zu beginnen und Ihre Preisstrukturpläne zu definieren. Die Konsole für das Ressourcenmanagement ist ein webbasiertes Tool, das Sie durch die Bereitstellung Ihres integrierten Abrechnungsservice im {{site.data.keyword.Bluemix_notm}}-Katalog führt.
{:shortdesc}

## Vorbereitende Schritte
{: #rmc-pre-reqs}

1. Vergewissern Sie sich, dass Sie mit dem folgenden Schritt beginnen: [Schritt 1. Servicedokumentation und Vertriebsfreigabe verfassen (PWB)](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. Vergewissern Sie sich, dass Sie die Registrierung bei {{site.data.keyword.Bluemix_notm}} durchgeführt haben. Führen Sie die [Registrierung](https://cloud.ibm.com/registration){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") andernfalls durch, bevor Sie fortfahren.
3. Vergewissern Sie sich, dass Sie sich im richtigen Konto befinden, bevor Sie mit dem Arbeiten in der Konsole für das Ressourcenmanagement beginnen.
4. Bereiten Sie Ihren {{site.data.keyword.Bluemix_notm}}-Servicenamen vor. Sie müssen sowohl einen Servicenamen angeben, der zur Identifikation des Service durch die {{site.data.keyword.Bluemix_notm}}-Plattform dient, als auch einen Anzeigenamen, der Ihren Kunden im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt wird.

  Wenn Sie die Registrierung für Ihr Angebot bei der Konsole für das Ressourcenmanagement durchführen, dann sollten Sie Ihren {{site.data.keyword.Bluemix_notm}}-Servicenamen bereithalten. Der Servicename stimmt nicht mit dem Anzeigenamen überein. Für die Erstellung des Servicenamens gelten die folgenden Regeln:
   - Es dürfen nur Kleinbuchstaben angegeben werden.
   - Es dürfen keine Leerzeichen im Namen enthalten sein. Bindestriche (`-`) sind hingegen zulässig.
   - Es dürfen nur weniger als 32 Zeichen angegeben werden.

   Ihr Servicename muss den Namen Ihres Unternehmens enthalten. Verfügt Ihr Unternehmen über mehrere Angebote, dann muss der Servicename sowohl das Unternehmen als auch das Angebot enthalten. Beispiel: Das Unternehmen 'Compose' verfügt über Angebote für Redis und Elasticsearch. Die Servicenamen dieser Angebote in {{site.data.keyword.Bluemix_notm}} können `compose-redis` und `compose-elasticsearch` lauten. Beide Servicenamen enthalten zugeordnete Anzeigenamen, die im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt werden: *Compose Redis* und *Compose Elasticsearch*. Ein anderes Unternehmen (z. B. FastJetMail) kann über nur das einzelne Angebot mit dem Namen 'JetMail' verfügen. In diesem Fall lautet der Servicename `fastjetmail`.

## Eigenes Angebot registrieren
{: #register}

Melden Sie sich zum Einstieg an und registrieren Sie Ihr Angebot.

1. Melden Sie sich bei [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") mit Ihrer {{site.data.keyword.Bluemix_notm}}-ID an.
   **Warnung**: Es ist wichtig, dass Sie sich im richtigen {{site.data.keyword.Bluemix_notm}}-Konto befinden. Wenn Sie über mehrere Konten verfügen, dann vergewissern Sie sich, dass Sie das richtige Konto aufrufen.
2. Rufen Sie das [Dashboard der Konsole für das Ressourcenmanagement](https://cloud.ibm.com/onboarding/dashboard){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") auf.
3. Klicken Sie auf **Neue Ressource**, um Ihre Ressource hinzuzufügen.
4. Fügen Sie den Wert für **Ressourcenname** hinzu. Dieser Wert gibt den eindeutigen {{site.data.keyword.Bluemix_notm}}-Servicenamen an, den Sie im vorherigen Abschnitt abgeleitet haben.
5. Es ist nicht davon auszugehen, dass Sie bereits über einen gehosteten Service-Broker verfügen. Wählen Sie also im Feld **Ist Ihr Broker bereit für den Import?** die Antwort **Nein** aus. Sie werden in den nachfolgenden Schritten durch die Erstellung eines Brokers geführt und dann wieder zur Konsole für das Ressourcenmanagement zurückkehren, um Ihren Broker zu importieren, nachdem die Entwicklung und das Hosten durchgeführt wurde.
7. Nach der Übergabe wird die Seite **Zusammenfassung** aufgerufen. Geben Sie alle zusätzlich *erforderlichen* Werte ein und klicken Sie dann auf **Speichern**.

Sie können Ihre Arbeitsergebnisse in der Konsole für das Ressourcenmanagement speichern und zu einem späteren Zeitpunkt zu diesen Ergebnissen zurückkehren, um weitere Informationen hinzuzufügen. Die Konsole für das Ressourcenmanagement wurde so konzipiert, dass Sie Unterstützung bei der Verwaltung des Lebenszyklus Ihres Service erhalten. Deshalb ist es in Ordnung, wenn Sie noch nicht alle Antworten auf die in den Feldern gestellten Fragen haben.
{: tip}

## Angebotsmetadaten eingeben
{: #offering-metadata}

Geben Sie auf der Seite **Angebot** die Metadatenwerte an, die im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert sind. Darüber hinaus ist bei einigen dieser Werte ein Export und die Speicherung in Ihrem Service-Broker erforderlich, in dem sie für die Bereitstellung verwendet und als Teil der `Katalog (GET)`-Antwort zurückgegeben werden. Verwenden Sie diese Werte in den nachfolgenden Schritten, um rasch einen Service-Broker zu entwickeln.

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Angebot** und dann auf die Registerkarte für die **Listenseite**. Auf der **Listenseite** werden die Metadaten definiert, die im Service-Dashboard Ihres {{site.data.keyword.Bluemix_notm}}-Angebots angezeigt werden. Geben Sie alle erforderlichen Werte an und klicken Sie dann auf **Speichern**. Die Konsole für das Ressourcenmanagement führt eine Erstregistrierung Ihres Service bei {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) durch. Daraufhin wird eine Benachrichtigung angezeigt, in der Sie darüber informiert werden, dass Ihr Service bei IAM registriert wurde. Später können Sie weitere Aktionen mit IAM ausführen.
2. Klicken Sie auf der Seite 'Angebot' auf die Registerkarte **Einstellungen**.
   1. Geben Sie an, ob für Ihr Angebot die Option **Werden Planänderungen unterstützt?** zulässig sein soll. Der Standardwert lautet **Nein**. Wenn Sie **Ja** angeben, dann müssen Sie Open Service Broker so erweitern, dass Planänderungen für bereitgestellte Instanzen unterstützt werden. Wenn Ihr Angebot mehrere Pläne unterstützt und wenn Sie möchten, dass Benutzer die Pläne für eine vorhandene bereitgestellte Instanz ändern können, müssen Sie die Funktion aktivieren, über die Benutzer ihre Serviceinstanz aktualisieren können. Weitere Details finden Sie unter dem Endpunkt `/v2/service_instances/{instance_id} PATCH` in der [Open Service Broker API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
   2. Geben Sie an, ob für Ihren Service die Option **Bindable** gelten soll. Der Standardwert ist **Nein**. Wählen Sie **Ja** aus, wenn Ihr Service in {{site.data.keyword.Bluemix_notm}} an Anwendungen gebunden werden kann. Wenn eine Bindung möglich sein soll, muss der Service API-Endpunkte und Berechtigungsnachweise an Ihre Servicekonsumenten zurückgeben können. Bei der Entwicklung eines Service, für den eine Bindung möglich ist, müssen Sie die Informationen im Abschnitt zu den [bindefähigen Operationen in der Open Service Broker-API v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") beachten.
   3. Geben Sie die Werte in den zusätzlich erforderlichen Feldern an und klicken Sie dann auf **Speichern**.
3. Auf der Seite 'Angebot' wird nun ein Häkchen in der Navigation angezeigt, das angibt, dass Sie die Mindestanforderungen beim Ausfüllen dieser Seite erfüllt haben. Wird die Seite weiterhin als unvollständig ausgewiesen, müssen Sie sie erneut öffnen und auf unvollständig ausgefüllte *erforderliche* Felder überprüfen.

Ihr erstes Anschreiben zu Ihrem Angebot umfasst eine URL für die Servicedokumentation, die von der Provider-Workbench generiert wurde. Sie müssen diese URL in den Feldern **Dokumentations-URL** und **Anweisungs-URL** eingeben.
{: tip}

## Bei IAM registrieren
{: #reg-iam}

IAM ist für das Onboarding aller Services in {{site.data.keyword.Bluemix_notm}} erforderlich. Weitere Informationen hierzu finden Sie im Abschnitt [ Was ist IAM?](/docs/iam?topic=iam-iamoverview#iamoverview). Dort erfahren Sie mehr über die IAM-Konzepte und -Anforderungen.

Die Konsole für das Ressourcenmanagement generiert die folgenden IAM-Werte:
   - Service-ID (generiert und gespeichert)
   - API-Schlüssel (generiert und nicht gespeichert - wird einmalig angezeigt)
   - Client-ID (generiert und gespeichert)
   - Geheimer Clientschlüssel (generiert und nicht gespeichert)

Der Service-Provider muss folgende Daten angeben:
   - Weiterleitungs-URI (Nach der OSB-Entwicklung kehren Sie zur Konsole für das Ressourcenmanagement zurück. Sie leiten den Weiterleitungs-URI aus der Position des gehosteten Service-Brokers ab.)

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Zugriffsmanagement**.
2. Klicken Sie auf **IAM aktivieren**. Die Konsole für das Ressourcenmanagement registriert Ihren Service bei IAM und erstellt die Service-ID, die Richtlinie und einen API-Schlüssel für Sie. Darüber hinaus wird eine unvollständige Client-ID und ein unvollständiger geheimer Schlüssel erstellt. Die Client-ID muss anhand Ihres Weiterleitungs-URI aktualisiert werden, nachdem dieser zur Verfügung steht.
3. Klicken Sie auf **Status**, um den aktuellen Status Ihrer IAM-Aktivierung anzuzeigen.

Sie müssen zu einem späteren Zeitpunkt die IAM-Seite erneut aufrufen, um die `Weiterleitungs-URI` anzugeben. Dieser Wert steht erst dann zur Verfügung, wenn Sie bestimmte zusätzliche Entwicklungsschritte ausgeführt haben, um einen Authentifizierungsablauf zu erstellen. In nachfolgenden Schritten werden Sie durch die Erkennung des Wertes für den Weiterleitungs-URI geführt.
{: note}

Sie erhalten Ihren API-Schlüssel, wenn Sie **IAM aktivieren**. Es ist wichtig, dass Sie den API-Schlüssel speichern. Der Wert wird nicht erneut angezeigt. Wenn Sie den API-Schlüssel verlieren, können Sie ihn löschen und einen neuen API-Schlüssel erstellen: [API-Schlüssel für Service-ID verwalten](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys).
{: tip}

## Preisstrukturplan entwickeln
{: #pricing-plan}

Wenn Sie das Onboarding Ihres Service in {{site.data.keyword.Bluemix_notm}} durchführen, dann müssen Sie auch einen Preisstrukturplan definieren. Wenn Sie über detailliertes Wissen zur Vorgehensweise bei der Belastung von Benutzern für Ihren Service verfügen, dann können Sie diese Informationen in Ihrem Plan angeben. Wenn Sie sich jedoch noch nicht für einen gebührenpflichtigen Plan entschieden haben, können Sie mit der Aktivierung eines kostenlosen Plans beginnen und später einen gebührenpflichtigen Plan einrichten.

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Preisstruktur**.
2. Klicken Sie auf **Plan hinzufügen**, um einen neuen Planeintrag zu erstellen, und klicken Sie dann auf **Plan bearbeiten**, um den Plan zu bearbeiten.
   * **Kostenfreier Plan**: Alle Angebote können über einen Lite-Plan verfügen, für den keine Gebühren berechnet werden. Auf diese Weise können Benutzer Ihren Service testen. Kostenfreie Pläne verwenden als **Anzeigename** den Wert *Lite* und als **programmorientierten Namen** den Wert *lite*. Geben Sie für **Ist dieser Plan kostenfrei?** die Option **Ja** an. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht.
   * **Abonnementplan**: Geben Sie bei diesem Plan für **Ist dieser Plan kostenfrei?** die Option **Nein** an. Füllen Sie die erforderlichen Felder aus. Behalten Sie die Standardmetrik **Preisstrukturmetrik** bei. Diese Standardmetrik wird bereitgestellt, damit Sie Benutzern eine einmalige monatliche Gebühr berechnen können. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht. Speichern Sie den curl-Beispielbefehl, um die Nutzungsdaten zu übermitteln.
   * **Plan mit Nutzungsmessung**: Geben Sie bei diesem Plan für **Ist dieser Plan kostenfrei?** die Option **Nein** an. Füllen Sie die erforderlichen Felder aus. *Löschen* Sie die standardmäßige Abonnementmetrik **Preisstrukturmetrik**. Klicken Sie auf **Weitere Metrik hinzufügen**, füllen Sie die Seite **Preisstrukturmetrik hinzufügen** aus und klicken Sie auf **Metrik hinzufügen**. Klicken Sie auf **Speichern**. Ihr Plan wird im {{site.data.keyword.Bluemix_notm}}-Katalog veröffentlicht. Speichern Sie den curl-Beispielbefehl, um die Nutzungsdaten zu übermitteln. Wenn Sie Hilfe bei der Auswahl der richtigen Metriken benötigen, dann lesen Sie die Informationen unter [Messungsintegration](/docs/third-party?topic=third-party-content-tasks#content-tasks).
3. Die Seite **Preisstruktur** wird nun als vollständig ausgewiesen. Damit wird angegeben, dass Sie die Mindestanforderungen beim Ausfüllen dieser Seite erfüllt haben.

Service-Provider müssen die stündliche Übermittlung der Nutzungsdaten für alle Pläne mit Nutzungsmessung automatisieren. Weitere Informationen finden Sie in [Nutzungsdaten für Pläne mit Nutzungsmessung übermitteln](/docs/third-party?topic=third-party-submitusage#submitusage).
{: tip}

## Metadaten im JSON-Format exportieren
{: #export-metadata}

Nachdem Sie Ihren Service nun in der Konsole für das Ressourcenmanagement definiert haben, können Sie die Datei mit dem Namen 'catalog.json' herunterladen und sie verwenden, um Informationen für die Entwicklung Ihres Open Service Broker bereitzustellen. Die Datei 'catalog.json' verfügt über Metadaten, die im Broker gehostet werden müssen. Diese Werte definieren den Vertrag zwischen dem Broker und der {{site.data.keyword.Bluemix_notm}}-Plattform für die Services und Pläne, die vom Broker unterstützt werden. Alle zusätzlichen Katalogmetadaten, die für die Bereitstellung nicht erforderlich sind, werden im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert. Alle Aktualisierungen an den Kataloganzeigewerten, die zur Darstellung Ihres Dashboards verwendet werden (z. B. Links, Symbole und mit i18n umgesetzte Metadaten) werden in der Konsole für das Ressourcenmanagement vorgenommen. Sie werden nicht in den Broker aufgenommen. Keine der in Ihrem Broker gespeicherten Metadaten werden in der {{site.data.keyword.Bluemix_notm}}-Konsole oder der {{site.data.keyword.Bluemix_notm}}-CLI angezeigt. Die Konsole und die CLI geben die Daten zurück, die in der Konsole für das Ressourcenmanagement festgelegt und im {{site.data.keyword.Bluemix_notm}}-Katalog gespeichert wurden.

1. Öffnen Sie in der Konsole für das Ressourcenmanagement die Seite **Bereitstellungen**.
2. Klicken Sie auf **Verwalten**.
3. Klicken Sie auf **Definitionen herunterladen**.

Speichern Sie die Datei `catalog.json`. Sie werden sie bei der Open Service Broker-Entwicklung im nächsten Abschnitt verwenden.

## Nächste Schritte
{: #cis2-next-steps}

Gut gemacht! Sie haben Ihr Serviceangebot definiert, indem Sie die Metadaten für die Kataloganzeige hinzugefügt, die Registrierung bei IAM durchgeführt und mindestens einen Preisstrukturplan erstellt haben. Als Nächstes können Sie mithilfe der exportieren JSON-Datei mit der Entwicklung eines Service-Brokers beginnen. Weitere Informationen hierzu finden Sie in [Schritt 3: Service-Broker entwickeln und hosten](/docs/third-party?topic=third-party-step3-osb#step3-osb).
