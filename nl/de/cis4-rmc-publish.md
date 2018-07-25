---


copyright:
  years: 2018
lastupdated: "2018-06-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Schritt 5: Eigenen Service veröffentlichen und testen

 Nachdem Sie nun über die gehosteten Broker verfügen, die der OSB-Spezifikation entsprechen, können Sie zur Konsole für das Ressourcenmanagement zurückkehren, um Ihren Service im {{site.data.keyword.Bluemix_notm}}-Katalog zu veröffentlichen. Füllen Sie die Registerkarte *Bereitstellungen* aus: Planen Sie die Bereitstellung Ihrer Servicepläne in einer oder auch mehreren Regionen des {{site.data.keyword.Bluemix_notm}}-Katalogs, testen Sie Ihre Broker und führen Sie anschließend die Veröffentlichung im Katalog im Modus für eingeschränkte Sichtbarkeit durch. Nach der erfolgreichen Bereitstellung müssen Sie Ihr Angebot testen, um sicherzustellen, dass es die erforderlichen Kriterien erfüllt, und anschließend den Veröffentlichungsprozess gemäß Ihren Anforderungen durchlaufen.


## Vorbereitende Schritte

Bei diesem Schritt wird davon ausgegangen, dass Sie bereits über die Genehmigung zum Bereitstellen eines integrierten Abrechnungsservice verfügen. Sollten Sie die Erstregistrierung und die Genehmigung in Provider Workbench noch nicht durchgeführt haben, dann sollten Sie sich mit den Informationen im [Lernprogramm 'Einführung'](/docs/third-party/index.md) vertraut machen.
{: tip}

Vergewissern Sie sich, dass Sie mit Schritt 1 begonnen und die Schritte 2, 3 und 4 abgeschlossen haben.
1. [Servicedokumentation und Marketingankündigung verfassen](/docs/third-party/cis1-docs-marketing.html).
2. [Angebot in der Konsole für das Ressourcenmanagement definieren](/docs/third-party/cis2-rmc-define.html).
3. [Eigene Service-Broker entwickeln und hosten](/docs/third-party/cis3-broker.html).
3. [Authentifizierungsablauf entwickeln](/docs/third-party/cis-iam.html).

## Eigenen Service in {{site.data.keyword.Bluemix_notm}} veröffentlichen

1. Klicken Sie in der Konsole für das Ressourcenmanagement auf die Seite **Bereitstellungen**.
2. Klicken Sie auf die Registerkarte **Broker** und anschließend auf **Broker hinzufügen**.
3. Klicken Sie auf **Verwalten**, um die Seite für die Konfiguration des Service-Brokers zu öffnen.
4. Fügen Sie den gehosteten Broker hinzu und klicken Sie dann auf **Broker registrieren**.
5. Rufen Sie nach erfolgreicher Registrierung die Registerkarte **Katalogbereitstellungen** auf.
6. Klicken Sie auf **Bereitstellung hinzufügen** und wählen Sie den Plan und den Broker aus, die bereitgestellt werden sollen.
7. Wählen Sie die Region und das Rechenzentrum aus, in denen Ihr Service bereitgestellt werden soll, und klicken Sie dann auf **Hinzufügen**.
8. Überprüfen Sie auf der Seite **Bereitstellungen** die nicht veröffentlichte Bereitstellung und klicken Sie dann auf **Veröffentlichen**.
9. Überprüfen Sie auf der Seite **Im Katalog veröffentlichen** die Details Ihrer Bereitstellung und klicken Sie dann auf **Veröffentlichen**.

Die Seite 'Bereitstellungen' muss nun in der Navigation als vollständig markiert sein. Dies bedeutet, dass Sie die Mindestanforderungen erfüllt haben.

Tritt bei der Bereitstellung ein Fehler auf, der sich nicht beheben lässt? Wenden Sie sich an den zuständigen IBM Ansprechpartner, um Hilfe anzufordern.
{: tip}

## Bereitgestelltes Angebot testen 

Da Sie die Bereitstellung im Modus für eingeschränkte Sichtbarkeit durchgeführt haben, können nur Sie selbst das Angebot im {{site.data.keyword.Bluemix_notm}}-Katalog anzeigen. Melden Sie sich mithilfe der folgenden Prüfliste bei {{site.data.keyword.Bluemix_notm}} an und arbeiten Sie die Testkriterien ab.

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an: [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") und verwenden Sie dazu Ihre IBMid.
2. Vergewissern Sie sich, dass Sie sich im richtigen Konto befinden (das gleiche Konto, das Sie zur Erstellung des Service verwendet haben).
3. Klicken Sie im Header auf den Link für **Katalog** und suchen Sie nach Ihrem Angebot. Dazu müssen Sie möglicherweise den experimentellen Servicekatalog öffnen.
4. Verwenden Sie als Nächstes die folgende Prüfliste, um Ihren Service zu überprüfen.

### Prüfliste - Eigenen Service testen
1. Überprüfen Sie die Authentifizierung über das Dashboard der Serviceinstanz.
2. Der Katalog wird korrekt angezeigt (Import aus dem Broker wird korrekt in der Konsole für das Ressourcenmanagement angezeigt).
3. Die Bereitstellung funktioniert. Sie können eine Serviceinstanz im Plan Ihrer Wahl erstellen.
4. Die Aufhebung der Bereitstellung funktioniert. Sie können eine Serviceinstanz löschen.
5. Die Bindung funktioniert. Sie können auf **Verbindungen** klicken und eine Verbindung zwischen Ihrem Service und einer anderen Anwendung herstellen.
6. Die Aufhebung der Bindung funktioniert. Sie können die Verbindung Ihres Service beenden und die Verbindung löschen.
7. Erstellung eines Serviceschlüssels / Löschung eines Serviceschlüssels. Sie können auf **Berechtigungsnachweise** klicken und einen Serviceschlüssel generieren und dann diesen Serviceschlüssel wieder löschen.
8. Testen Sie `plan_changeable`, wenn mehrere Pläne unterstützt werden. Wenn Sie diese Funktion aktivieren, indem Sie 'Ja' angeben, dann müssen Sie den Open Service Broker erweitern, sodass Planänderungen für bereitgestellte Instanzen unterstützt werden. Wenn Ihr Angebot mehrere Pläne unterstützt und wenn Sie möchten, dass Benutzer die Pläne für eine bereitgestellte Instanz ändern können, dann müssen Sie die Funktion aktivieren, über die Benutzer ihre Serviceinstanz aktualisieren können. Weitere Einzelheiten hierzu finden Sie unter dem /v2/service_instances/{instance_id} PATCH-Endpunkt in der Open Service Broker-API v2.12  - Patch - Es wird angezeigt, dass der Benutzer den Plan für die bereitgestellte Instanz ändern kann. Um den Test durchzuführen, müssen Sie den Plan einer vorhandenen bereitgestellten Serviceinstanz ändern.
9. Die OSB-Spezifikation bietet keine Unterstützung für einen inaktivierten Instanzstatus, der jedoch noch nicht gelöscht wurde. Damit IBM Cloud Kunden unterstützen kann, bei denen es möglicherweise zu einem Abrechnungsfehler oder zu anderen Situationen kommt, die zu einer Aussetzung des Kontos (jedoch nicht zum Abbruch) führen können, hat IBM Cloud erweiterte API-Endpunkte definiert, die es Ihnen ermöglichen, Serviceinstanzen zu inaktivieren und erneut zu aktivieren. Die folgenden Endpunkterweiterungen sind **ERFORDERLICH**. Arbeiten Sie mit Ihrem IBM Ansprechpartner zusammen und lassen Sie die Aktivierungs- und Inaktivierungsendpunkte testen:
   - Instanzen aktivieren und inaktivieren (GET): Status - Gibt den Status Ihrer Serviceinstanz zurück.
   - Instanzen aktivieren und inaktivieren (PUT): Ermöglicht das Aktivieren oder Inaktivieren einer Serviceinstanz.
10. Testen der Übermittlung von Nutzungsdaten bei Unterstützung von nutzungsabhängigen Plänen. Für alle nutzungsabhängigen Pläne müssen Sie Folgendes überprüfen:
   - Sie können die Nutzungs-API mit curl bearbeiten und es können korrekte Preisstrukturdaten auf Basis der Nutzung zurückgegeben werden.
   - Sie können demonstrieren, dass Sie die automatisierte stündliche Übermittlung von Nutzungsdaten aktiviert haben, sodass alle Benutzer unterstützt werden, die eine Instanz Ihres Service bereitstellen.

Verlaufen die Tests nicht erfolgreich, dann müssen Sie die vorangegangenen Schritte wiederholen, um Ihren Service zu veröffentlichen und erneut zu testen. Dieser Vorgang muss so lange wiederholt werden, bis er erfolgreich abgeschlossen werden kann.


## Nächste Schritte

Nachdem Sie nun über einen funktionsbereiten Service im Katalog verfügen, können Sie eine Demo erstellen und die Genehmigung anfordern, um Ihren Service öffentlich freigeben zu können. Weitere Informationen hierzu finden Sie in [Schritt 6: Eigenen Service öffentlich freigeben](/docs/third-party/cis6-ga.html).
