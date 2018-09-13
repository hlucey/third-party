---

 
copyright:

  years: 2017, 2018

lastupdated: "2018-08-30" 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Nutzungsdaten für Pläne mit Nutzungsmessung übermitteln
{: #submitusage}

Sie müssen die Nutzungsdaten stündlich für alle aktiven Serviceinstanzen übermitteln. Werden die Nutzungsdaten nicht gemeldet, dann kann dies zu Umsatzeinbußen für IBM führen, die ihrerseits Umsatzeinbußen in Bezug auf die Anteile der Angebotsprovider zur Folge haben können.
{:shortdesc}

## Ablauf des Prozesses
{: #process-flow}

In den folgenden Schritten wird der Prozess zur Übermittlung von Nutzungsdaten beschrieben:

1. Übermitteln Sie über das REST-API-Tool für die Nutzungsdatenübermittlung eine Testmeldung für die Nutzungsdaten, um zu überprüfen, ob Ihre Pläne mit Nutzungsmessung korrekt konfiguriert wurden.
2. Automatisieren Sie die fortlaufende stündliche Übermittlung an das REST-API-Tool für die Nutzungsdatenübermittlung für jeden Plan mit Nutzungsmessung. Sie können diese automatisierten Übermittlungen an einer beliebigen Position hosten, solange diese Position die SSO-Standardfunktionen unterstützt.
2. Die Nutzungsdatensätze werden auf Basis des Messungsmodells aggregiert und die Gesamtmenge wird im Nutzungsdashboard an der {{site.data.keyword.Bluemix_notm}}-Konsole angezeigt.
3. Die aggregierte Einheitenmenge aus dem Messungsprozess wird verwendet, die Kosten werden angewendet und der Betrag, den der Benutzer für die Serviceinstanz schuldet, wird berechnet.
4. Am Monatsende wird der für den Benutzer generierte Betrag auf Basis der abschließenden berechneten Kosten ermittelt.

## Voraussetzungen
{: #prereqs}

Überprüfen Sie die folgernden Voraussetzungen für das Aktivieren der Messung für Ihren Service:

* Der Preisstrukturkatalog wird mit den Preisen für alle abrechenbaren Metriken in den Plänen der Ressource aktualisiert.
* Die Messungs- und Bewertungsdefinitionen für alle Pläne in der Ressource werden überprüft und durchlaufen das Onboarding.

## Richtlinien für die Übermittlung der Nutzungsdaten 
{: #metering_guidelines}

### Übermittlungsrichtlinien

Beachten Sie bei Verwendung des {{site.data.keyword.Bluemix_notm}}-Messservice zur Übermittlung der Ressourcennutzungsdaten die folgenden Richtlinien:

* Der Start- und der Endzeitpunkt legen den Zeitbereich fest, innerhalb dessen die Messungen erfasst werden. Die Zeitangaben sind nicht von der Zeit abhängig, zu der der Nutzungsdatensatz an die Messungs-APIs übermittelt wurde.
* Nutzungsdatensätze werden als Fakten eingestuft. Aus diesem Grund dürfen Nutzungsdatensätze nach ihrer Erstellung nicht mehr aktualisiert werden. Eine Position wird angegeben, wenn Sie die Erstellung eines Nutzungsdatensatzes erfolgreich abgeschlossen haben. Wird ein Fehlercode zurückgegeben, dann informieren Sie sich über die [Aktionen](#actions), die möglicherweise ausgeführt werden müssen.
* Ein Nutzungsdatensatz wird durch die Signatur `account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end` eindeutig identifiziert. Wenn ein Nutzungsdatensatz verarbeitet wird, dann werden alle anderen Nutzungsdatensätze mit derselben Signatur als Duplikate zurückgewiesen.
* Die Interaktionen mit dem Messservice dürfen nicht mit anderen Services kombiniert werden. Die Anforderungen müssen auch dann einzeln verarbeitet werden, wenn die Messung mit der Bereitstellung der Instanz beginnt und mit der Aufhebung der Bereitstellung endet.
* Die Ressourcennutzungsdaten müssen in einem Intervall von 2 bis 24 Stunden an den Messservice übermittelt werden. Die Häufigkeit der Übermittlung Ihrer Nutzungsdaten ist davon abhängig, wie oft die Nutzungsmetriken geändert werden.
* Nutzungsdatensätze müssen spätestens zwei Tage nach Abschluss der Messung übermittelt werden. Ältere Nutzungsdatensätze werden zurückgewiesen.
* Eine erfolgreiche Übermittlung gibt den Antwortcode '201' zurück. Wird ein anderer Antwortcode zurückgegeben, dann müssen die Daten so lange aktualisiert und erneut gesendet werden, bis Sie den Code '201' erhalten.

Im Folgenden werden die Best Practices zur Übermittlung der Nutzungsdaten aufgeführt:

* Service-Provider sollten Nutzungsdaten jede Stunde übermitteln, sodass der Endbenutzer keine langen Verzögerungen zwischen dem Zeitpunkt der Ressourcennutzung und dem Zeitpunkt feststellt, zu dem die Kosten in seinem Konto wiedergegeben werden.
* Wiederholen Sie die Übermittlung der Nutzungsdatensätze nur, wenn bei der vorherigen Anforderung ein echter Fehler aufgetreten ist. Nutzungsdatensätze, die erfolgreich akzeptiert wurden, dürfen nicht erneut übermittelt werden.

### Richtlinien für die Service-ID

  Bei der Angabe der Service-ID im Feld 'ID' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:
  * Beginnen Sie die ID mit einem alphanumerischen Zeichen.
  * Verwenden Sie die Zeichen A-Z, a-z und 0-9. Die einzigen Sonderzeichen, die Sie verwenden dürfen, sind Bindestriche (-) und Unterstreichungszeichen (_).
  * Beachten Sie die Konvention für die Kamelschreibweise, wenn die ID mehrere Wörter umfasst.
  * Vergewissern Sie sich, dass die ID maximal 50 Zeichen lang ist.

### Richtlinien für Ressourcennamen

  Bei der Angabe des Ressourcennamens im Feld 'resources.name' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:

  * Verwenden Sie nur Wörter, die Ihre Ressourcen beschreiben. Beispiel: **Storage** oder **ApiCalls**. 
  * Beachten Sie die Konvention für die Kamelschreibweise, wenn der Name mehrere Wörter umfasst.
  * Verwenden Sie als erstes Zeichen im Namen einen Großbuchstaben.

### Richtlinien für Ressourceneinheitennamen

  Bei der Angabe des Ressourceneinheitennamens im Feld 'resources.unit.name' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:

  * Verwenden Sie ein Wort für den Einheitennamen und verwenden Sie ein Unterstreichungszeichen (_) anstelle eines Leerzeichens, um Wörter voneinander zu trennen. Beispiel: Geben Sie **API_CALL** anstelle von **API CALL** an.  
  * Geben Sie alle Buchstaben des Namens in Großschreibung an.
  
### Richtlinien für Ressourceneinheitenquantität

  Bei der Angabe des Ressourcenmengentyps im Feld 'resources.unit.quantityType' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:
  
  * Verwenden Sie ein Wort für den Mengentyp.
  * Geben Sie alle Buchstaben des Mengentyps in Großschreibung an.
  
### Richtlinien für die Aggregations-ID

  Bei der Angabe der Aggregations-ID im Feld 'aggregations.id' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:

  * Geben Sie alle Buchstaben des Mengentyps in Großschreibung an.
  * Verwenden Sie ein Unterstreichungszeichen (_) anstelle eines Leerzeichens, um Wörter voneinander zu trennen.
  * Vergewissern Sie sich, dass diese ID mit dem Wert im Feld 'aggregations.unit' beginnt bzw. mit diesem Wert übereinstimmt. Beispiel: Sie können für 'aggregations.id' den Wert **API_CALLS_PER_MONTH** und für 'aggregations.unit' den Wert **API_CALLS** angeben.

### Richtlinien für Aggregationseinheiten

  Bei der Angabe der Aggregationseinheit im Feld 'aggregations.unit' der Ressourcendefinition müssen Sie die folgenden Richtlinien beachten:
   
  * Verwenden Sie für den Einheitennamen die Singularform.
  * Geben Sie alle Buchstaben des Einheitennamens in Großschreibung an.
  * Vergewissern Sie sich, dass der Einheitenname, den Sie im Feld 'aggregations.unit' angeben, ein Aggregat des Einheitennamens darstellt, den Sie im Feld 'resources.unit.name' angeben.
  
### Richtlinien für Aggregationsgruppen

  Sie müssen im Feld 'aggregations.aggregationGroup' in der Ressourcendefinition Kleinbuchstaben verwenden.
  
### Richtlinien für Aggregationsformeln

  Wenn Sie im Feld 'aggregations.formula' in der Ressourcendefinition Rechenoperationen in der Formel verwenden wollen, dann müssen Sie die Ressourceneinheit als Operanden und einen arithmetischen Infixausdruck in der Funktion der Formel verwenden. Sie können beispielsweise die folgende Formel verwenden, um Byte in Megabyte umzuwandeln:
  ```
  SUM({BYTE}/1048576)
  ```

## REST-API für Übermittlung von Nutzungsdaten
{: #RAPIusesubmit}

Die Gebühren von {{site.data.keyword.Bluemix_notm}}-Benutzer werden auf Basis des Ressourcenvolumens berechnet, das von den Benutzern genutzt wird. Für Benutzer, die Datenbankservices nutzen, werden die Gebühren beispielsweise auf Basis der Speicherkapazität berechnet, die von den Anwendungen der Benutzer verbraucht wird.

Um den {{site.data.keyword.Bluemix_notm}}-Messservice zum Melden von Nutzungsdaten zu verwenden, müssen Sie die API des Messservice zum Melden von Nutzungsdaten Ihres Angebots implementieren. Weitere Einzelheiten hierzu finden Sie im Abschnitt zur [Dokumentation der öffentlichen API](https://ibm-bluemix-docs.github.io/usage-submission/).  

Sie müssen die stündliche Übermittlung von Nutzungsdaten mithilfe der Messservice-API automatisieren. Sie können die automatisierte Übermittlung auf jedem gültigen HTTPS-Endpunkt hosten, auf den über das öffentliche Internet zugegriffen werden kann.
{: tip}

## Nutzungsdatensätze übermitteln
{: #usage-records}

Nutzungsdatensätze sind die kleinsten Entitäten, die zu den aggregierten Werten der Metriken beitragen. Ein Nutzungsdatensatz wird mithilfe der folgenden Felder erstellt:

| Name | Beschreibung                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  Die ID der Ressourceninstanz.  |
| plan_id | Der Vertrag, anhand dessen der Nutzungsdatensatz aggregiert und bewertet wird.   |
| start  | Der Zeitpunkt, ab dem die Nutzung gemessen wird, angegeben in Millisekunden seit der Epoche.  |
| end  | Der Zeitpunkt, bis zu dem die Nutzung gemessen wird, angegeben in Millisekunden seit der Epoche.  |
| region  | Die Region des Angebotsproviders, in der die Nutzung gemessen wird.  |
| measured_usage  | Ein Array von Messpunkten mit Werten.  |
| consumer_id | Optional. Dieses Feld ist nur erforderlich, wenn die Aggregation auf Konsumentenebene erforderlich ist. Nur Angebotsprovider kennen den Wert für 'consumer_id'. |
{: caption="Tabelle 1. Felder des Nutzungsdatensatzes" caption-side="top"}

Sie können mehrere Nutzungsdatensätze übermitteln, indem Sie einen API-Aufruf verwenden. Sie können maximal 100 Nutzungsdatensätze pro Aufruf übermitteln. Der Antworthauptteil umfasst den Annahmestatus der einzelnen Nutzungsdatensätze. Jeder Status ungleich '201' umfasst einen Fehlercode und gibt an, warum der Nutzungsdatensatz nicht akzeptiert wurde. In der folgenden Tabelle werden die Statuscodes und die erforderliche Aktion aufgeführt.

| Statuscode | Erforderliche Aktion                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Wiederholen Sie die Übermittlung des Nutzungsdatensatzes. Wenn das Problem bestehen bleibt, wenden Sie sich an das BSS-Messteam. |
| 400 |  Der Nutzungsdatensatz weist nicht das richtige Format auf. Entweder ist die Schemaprüfung fehlgeschlagen, die Messungen in den Nutzungsdatensätzen sind falsch oder der Start- und der Endzeitpunkt liegen nicht innerhalb des Zeitraums zwischen der Bereitstellung und der Aufhebung der Bereitstellung. Aktualisieren Sie den Nutzungsdatensatz und übermitteln Sie ihn erneut.   |
| 424  | In den Metadaten der Ressourceninstanz sind Fehler aufgetreten. Aktualisieren Sie die Details der Ressourceninstanz und übermitteln Sie den Nutzungsdatensatz erneut.  |
| 404  | Für die Messungsdefinition wurde kein Onboarding durchgeführt. Wenden Sie sich an das BSS-Messteam und lassen Sie überprüfen, ob für die Ressource ein Onboarding durchgeführt wurde. Wiederholen Sie anschließend die Übermittlung des Nutzungsdatensatzes. |
| 409  | Der Nutzungsdatensatz ist ein Duplikat. Versuchen Sie nicht, ihn erneut zu übermitteln. |
{: caption="Tabelle 2. Statuscodes und erforderliche Aktionen" caption-side="top"}
{: #actions}


  
