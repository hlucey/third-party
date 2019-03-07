---

copyright:

  years: 2017, 2019

lastupdated: "2019-02-25"

keywords: Q P, offering usage, metering service, configuration, metering model, daily proration 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Messungsintegration
{: #meteringintera}

{{site.data.keyword.Bluemix}} unterstützt mehrere Modelle für die Aggregation der Angebotsnutzung. Angebotsprovider messen verschiedene Metriken zu den bereitgestellten Instanzen und übermitteln die entsprechenden Messwerte an den Messservice. Der Bewertungsservice aggregiert die übermittelten Nutzungsdaten auf Basis des Modells, das von den Angebotsprovidern ausgewählt wurde, in verschiedenen Buckets (Instanz, Ressourcengruppe und Konto). Die Aggregations- und Bewertungsmodelle für alle Metriken eines Plans sind in den Dokumenten für die Messungs- und Bewertungsdefinition des jeweiligen Plans enthalten.
{:shortdesc}

In der folgenden Liste finden Sie eine Beschreibung der Erwartungen, die bei der Überwachung und Übermittlung der Nutzungsdaten gelten:

*	Provider von Drittanbieterangeboten müssen für kostenfreie Pläne keine Nutzungsdaten übermitteln.
*	Provider von Drittanbieterangeboten müssen für monatliche Abonnementpläne keine Nutzungsdaten übermitteln.
*	Für Pläne mit Nutzungsmessung müssen alle Angebotsprovider stündliche Nutzungsdaten übermitteln (Lite-Pläne müssen Daten in Intervallen zwischen 15 Minuten und 1 Stunde übermitteln).
*	Der Angebotsprovider ist für die Automatisierung der Übermittlung der Nutzungsdaten verantwortlich. Hierzu zählt auch die Automatisierung von erneuten Versuchen nach einer fehlgeschlagenen Antwort. {{site.data.keyword.Bluemix_notm}} stellt keine Wiederholungsfunktion für fehlgeschlagene Übermittlungen bereit. Weitere Informationen finden Sie in der Tabelle für die Statuscodes und Aktionen im Abschnitt [Nutzungsdatensätze übermitteln](/docs/third-party?topic=third-party-submitusage#usage-records).
*	Die Nutzungsdatensätze für den aktuellen Monat müssen spätestens zum 2. des Folgemonats übermittelt werden.
*	{{site.data.keyword.Bluemix_notm}} ist für einen monatlichen Abrechnungszyklus konfiguriert. Die Zeit wird als Angabe in koordinierter Weltzeit (UTC; Coordinated Universal Time) dargestellt.
*  Angebotsprovider müssen die Übermittlung von Nutzungsdaten testen und die entsprechenden Ergebnisse überprüfen, um Informationen zur Berechnung des monatlichen Abrechnungszyklus bereitzustellen.

Allgemeine Informationen zur Preisstruktur finden Sie in [Vorgehensweise zur Kostenberechnung](/docs/billing-usage?topic=billing-usage-cost#cost). 

## Konfigurationseigenschaften
{: #configure}

Die folgenden Eigenschaften definieren die Vorgehensweise zur Messung und Bewertung der Übermittlung von Nutzungsdaten für Angebotspläne:

<dl>
<dt>Einheit</dt>
<dd>Zu messende Metrik, z. B. ApiCall, Byte, Stunden, Instanzen und Knoten.</dd>
<dt>Aggregation</dt>
<dd>Die Vorgehensweise zum Kompilieren der gemessenen Daten zur Einheit, z. B. INSTANCES_BY_MONTH oder ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Messungsmodell</dt>
<dd>Die Vorgehensweise zur Verarbeitung der übermittelten Nutzungsdaten (siehe folgende Tabelle).</dd>
<dt>Ressourcenname</dt>
<dd>Der Name der Ressource, für die Messungen durchgeführt werden, z. B. Speicher, Instanz, virtueller Server oder übertragene Byte.</dd>
<dt>Einheitenname</dt>
<dd>Der beschreibende Name der Einheit, wenn der Standardname für das Angebot nicht relevant ist.</dd>
</dl>

## Typen von Messungsmodellen
{: #metermodel}

In der folgenden Tabelle werden die verfügbaren Messungsmodelle dargestellt.

|  Typ | Beschreibung  |
|-----|-----|
| standard_add | Addieren der Menge aus allen übermittelten Nutzungsdatensätzen eines Monats. | 
| standard_max  | Maximale Menge aus allen übermittelten Nutzungsdatensätzen eines Monats. | 
| standard_avg | Durchschnittliche Menge aus allen übermittelten Nutzungsdatensätzen eines Monats. |
| dailyproration_max | Berechneter Tageshöchstwert. Summe aller Tage eines Monats. | 
| dailyproration_avg | Berechneter Tagesdurchschnittswert. Summe aller Tage eines Monats. |
| monthlyproration | Berechnung ähnlich wie bei der täglichen anteilmäßigen Verrechnung, aber der verwendete Preis ist der Planpreis geteilt durch die Gesamtzahl der Tage des Monats (Tagespreis). |
{: caption="Tabelle 1. Messungsmodell" caption-side="top"}

### Beispiele
{: #examples}

Beachten Sie, dass die im Dashboard vorhandene Menge in den folgenden Beispielen sich auf den Wert vor der Übermittlung der nächsten Nutzung, jedoch nach der Verarbeitung der aktuellen Nutzung bezieht.

#### Standardmäßige Hinzufügung
{: #standard-add}

Berechnen Sie die Nutzungsdaten für den gesamten Monat.

Formel: ADD(usages)

| Zeit            | Eingesendete Nutzungsdaten | Berechnung | Menge im Dashboard |
|-----------------|:-------------:| ----------- |:---------------------:|
| Tag 1 (Morgen) | 5             | 5           | 5                     |
| Tag 1 (Nacht)   | 5             | 5 + 5       | 10                    |
| Tag 2 (Morgen) | 5             | 10 + 5      | 15                    |
| Tag 3 (Morgen) | 5             | 15 + 5      | 20                    |
| Tag 4 (Nacht)   | 5             | 20 + 5      | 25                    |
{: caption="Tabelle 2. Monatliche Nutzungsberechnungen" caption-side="top"}

#### Standardmäßiger Durchschnitt
{: #standard-average}

Berechnen Sie den Durchschnitt der Nutzungsdaten für den gesamten Monat. Beachten Sie hierbei, dass die Übermittlung von Nullnutzungsdaten ebenfalls bei der Berechnung des Durchschnitts berücksichtigt wird.

Formel: AVG(usages)

| Zeit            | Eingesendete Nutzungsdaten | Berechnung             | Menge im Dashboard |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Tag 1 (Morgen) | 4             | 4 / 1                   | 4                     |
| Tag 1 (Nacht)   | 0             | (4 + 0) / 2             | 2                     |
| Tag 2 (Morgen) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Tag 3 (Morgen) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Tag 4 (Nacht)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |
{: caption="Tabelle 3. Monatliche Nutzungsberechnungen - Durchschnitt" caption-side="top"}

#### Standardmäßiges Maximum
{: #standard-max}

Berechnen Sie das Maximum der Nutzungsdaten für den gesamten Monat.

Formel: MAX(usages)

| Zeit            | Eingesendete Nutzungsdaten  | Berechnung  | Menge im Dashboard |
|-----------------|:--------------:| ------------ |:---------------------:|
| Tag 1 (Morgen) | 5              | MAX(5)       | 5                     |
| Tag 1 (Nacht)   | 10             | MAX(5, 10)   | 10                    |
| Tag 2 (Morgen) | 0              | MAX(10, 0)   | 10                    |
| Tag 3 (Morgen) | 15             | MAX(10, 15)  | 15                    |
| Tag 4 (Nacht)   | 1              | MAX(15, 1)   | 15                    |
{: caption="Tabelle 4. Monatliche Nutzungsberechnungen - Maximum" caption-side="top"}

#### Durchschnittliche anteilmäßige Verrechnung pro Tag
{: #proration-average}

Berechnen Sie die durchschnittlichen Nutzungsdaten für jeden Tag und den Durchschnitt für den Monat. Der Durchschnitt für jeden Tag wird addiert und durch die Anzahl der bereits verstrichenen Tage (in koordinierter Weltzeit) dividiert.

Formel: Summation(daily average) / Anzahl der verstrichenen Tage im Abrechnungszeitraum

Beachten Sie, dass die Menge sich innerhalb des Monats ändern kann. Bewertet wird jedoch die durchschnittliche Nutzung pro Tag.

Beispiel für einen Monat mit 30 Tagen:

| Zeit               | Eingesendete Nutzungsdaten    | Täglicher Durchschnitt | Berechnung                            | Menge im Dashboard*                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Tag 1 (Morgen)    | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Tag 1 (Nacht)      | 3                | (8 + 3) / 2   | 5,5 / 1                                | 5,5 (am Ende des ersten Tages)                               |
| Tag 2 (Morgen)    | 2                | 2 / 1         | (5,5 + 2) / 2                          | 3,75                                             |
| Tag 2 (Nacht)      | 5                | (2 + 5) / 2   | (5,5 + 3,5) / 2                        | 4,5 (am Ende des zweiten Tages)                               |
| Tag 3 bis Tag 15    | 1                | 1 / 1         | (5,5 + 3,5 + (1 + 13)  / 15            | 1,4666  (am Ende des 15. Tages)                          |
| Tag 15 bis Tag 30   | 0                | 0 / 1         | (5,5 + 3,5 + (1 \* 12) + (0  \* 15) / 30 | 0,7333  (am Ende des 30. Tages)                          |
{: caption="Tabelle 5. Berechnung der durchschnittlichen Nutzung pro Tag und Monat" caption-side="top"}

\* Wie für denselben Tag angezeigt, an dem die Nutzungsdaten übermittelt wurden.

#### Maximale anteilmäßige Verrechnung pro Tag
{: #daily-proration}

Berechnen Sie den Maximalwert der Nutzungsdaten pro Tag und den Durchschnitt für den Monat. Der Maximalwert der einzelnen Tage wird addiert und durch die Anzahl der bereits verstrichenen Tage (in koordinierter Weltzeit) dividiert.

Formel: Summation(daily max) / Anzahl der verstrichenen Tage im Abrechnungszeitraum

Beachten Sie, dass die Menge sich innerhalb des Monats ändern kann. Bewertet wird jedoch die maximale Nutzung pro Tag.

Beispiel für einen Monat mit 30 Tagen:

| Zeit             | Eingesendete Nutzungsdaten  | Tageshöchstwert | Berechnung                    | Menge im Dashboard* |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Tag 1 (Morgen)  | 0              | MAX(0)    | 0 / 1                          | 0                      |
| Tag 1 (Nacht)    | 1              | MAX(0, 1) | 1 / 1                          | 1                      |
| Tag 2 bis Tag 15  | 1              | MAX(1)    | (1 + 1 + ...) / Tag            | 1                      |
| Tag 15 bis Tag 30 | 0              | MAX(0)    | (1 + (1 * 14) + 0 + ...) / Tag | < 1                    |
{: caption="Tabelle 6. Berechnung der maximalen Nutzung pro Tag und des monatlichen Durchschnitts" caption-side="top"}

\* Wie für denselben Tag angezeigt, an dem die Nutzungsdaten übermittelt wurden.

## Beispiele für Messungs- und Bewertungsskala
{: #scale-examples}

Sie können die Skalierungskonfiguration verwenden, um die Einheitenmenge anders als bei der Übermittlung von Nutzungsdaten, bei der Anzeige im Nutzungsdashboard und anders als die verwendeten Daten für die Bewertung und Kostenberechnungen zu kompilieren. In den folgenden Beispielen werden diese Szenarios dargestellt:

### Sie möchten einen höheren Detaillierungsgrad als in der Benutzeranzeige verwenden
{: #users}

Sie möchten Nutzungsdaten mit einem höheren Detaillierungsgrad senden, für Kunden jedoch einen einfacher lesbaren numerischen Wert darstellen.

Beispiel: Sie möchten den Datenverkehr einer Instanz in Byte messen und den aggregierten Wert in Megabyte anzeigen. Hierzu fügen Sie eine `Skalierung` von 1024 zur Konfiguration für die **Messung** hinzu.

### Sie möchten einen höheren Detaillierungsgrad als bei der Preisstrukturkonfiguration verwenden
{: #pricing-configuration}

Sie legen für Ihre Metriken einen Preis nach der Formel EuroX / Gigabyte fest, möchten die Übermittlung jedoch in Megabyte durchführen. Wenn der Preis für Ihre Metrik nach der Formel Euro1 / Gigabyte festgelegt wird, der Benutzer jedoch 0,5 Megabyte verwendet, dann wird 1 Euro berechnet, da Ihre Preisstruktur auf einer Abrechnung pro Gigabyte basiert. Sie fügen eine `Skalierung` von 1024 zur Konfiguration für die **Bewertung** hinzu und geben für `clip` den Wert `true` an.

Diese Einstellung gilt, wenn der Preis für Ihre Metrik auch nach der Formel EuroX pro 100 API-Aufrufe (oder einer anderen Paketgröße) berechnet wird.

### Sie möchten die Skalierung sowohl auf Messungs- als auch auf Bewertungsebene durchführen
{: #metering-rating}

Sie können eine Skalierung sowohl zur Messungs- als auch zur Bewertungskonfiguration hinzufügen. Wenn die Übermittlung in Byte erfolgen soll, die Werte für den Benutzer jedoch in Megabyte angezeigt werden sollen, dann konfigurieren Sie die Messungsskalierung mit 1024. Wird der Preis für die Metrik in Gigabyte angegeben, dann müssen Sie auch die Bewertungsskalierung mit 1024 konfigurieren.

## Preisstaffelungsmodelle
{: #pricing}

Die folgende Tabelle enthält ausführliche Informationen zu den Preisstaffelungsmodellen, die zur Verfügung stehen. Für viele der verfügbaren Metriken können Sie ein zugeordnetes Preisstaffelungsmodell auswählen.

| Modell          | Beschreibung | Berechnung | Beispiel (Menge 5000) |
|:-----------------|:-------------|:----------- |:---------------------|
| Linear         | Multiplikation des Einzelpreises pro Ressource (P) mit der Nutzungsmenge (Q) zur Ermittlung des Gesamtbetrags (T)  | P*Q    | P=$1 T=1*5000 =$5000        |
| Anteilmäßige Verrechnung      | Multiplikation des täglichen Einzelpreises pro Ressource (P) mit der täglichen Nutzungsmenge (Q) zur Ermittlung des täglichen Gesamtbetrags. Die Gesamtgebühr umfasst die Kumulierung der Gebühren für alle Tage innerhalb des Monats.         | T= (pd * Q1) + ...+(Pd *Qn)     | <ul><li>P= $30</li><li>Pd (Tagespreis) =$30/30=$1 (bei 30 Tagen pro Monat)</li><li>T1= $1 * 1 =$1</li><li>T2 = $1 * 0 =$0</li><li>Tn = 1 * 1 =$1</li><li>T = $1 + $0 +...+$1 = $5000</li></ul>     |
| Einfache Preisstufe (differenzierte Preisstufe)  | Ein P*Q-Modell, in dem der Einzelpreis für die gesamte Nutzung anhand der Preisstufe für die Menge ermittelt wird.           | <ul><li>Wenn Q gleich <=Q1, T=P1*Q ist</li><li>Wenn Q1 < Q <=Q2, T=P2*Q</li><li>Wenn Q2 < Q <=Q3, T=P3*Q</li></ul>     |   <ul><li>Q1=1000, P1=$1</li><li>Q2=2500, P2=$0.9</li><li>Q3=10000, P3=$0.75</li><li>T=$0.75*5000=$3750</li></ul>              |
| Gestaffelte Preisstufe (schrittweise Preisstufe)   | Der Stückpreis variiert, wenn die genutzte Menge in verschiedene vordefinierte Preisstufen verschoben wird. Die Gesamtgebühr umfasst die Kumulierung der Gebühren aus den vorherigen Preisstufen           | <ul><li>T1=P1*Q (0 < Q</li><li>Wenn Q1 < Q <=Q2, T=T2</li><li>Wenn Q2 < Q <=Q3, T=T3</li></ul>     | <ul><li>Q1=1000, P1=$1, T1=1*1000</li><li>Q2=1500, P2=$0.9, T2=0.9*1500</li><li>Q3=10000, P3=$0.75, T3=0.75*2500</li><li>T=1000 +1350+1875=$4225</li></ul>          |
| Blockpreisstufe (bis zu)           | Der belastete Gesamtbetrag wird anhand einer Maximalmenge festgelegt, die innerhalb des Blocks nicht variiert     | <ul><li>Wenn Q gleich <=Q1, T=T1</li><li>Wenn Q1 < Q <=Q2, T=T2</li><li>Wenn Q2 < Q <=Q3, T=T3</li></ul>    |  <ul><li>Q1=1000, T1=$0</li><li>Q2=2500, T2=2500</li><li>Q3=10000, T3=$4500</li><li>T=$4500</li></ul>            |
{: caption="Tabelle 7. Preismodelle" caption-side="top"}

