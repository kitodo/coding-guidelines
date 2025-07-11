# Leitfaden für Kitodo-Entwickler:innen

> [!NOTE]
> Dieses Dokument ist gemäß § 11 der [Vereinssatzung](https://www.kitodo.org/fileadmin/groups/kitodo/Verein/2025-06-20_Satzung_Kitodo_eV.pdf) auf Beschluss der Mitgliederversammlung des Vereins [Kitodo. Key to digital objects e. V.](https://www.kitodo.org/verein/ueber-den-verein) am 25.06.2025 in Kraft getreten und ersetzt mit diesem Stichtag die bisher gültige, von der Mitgliederversammlung beschlossene Fassung vom 24.11.2021.

Dieses Dokument beschreibt die Grundsätze der gemeinsamen Software-Entwicklung für Kitodo. Dazu werden die generelle Entwicklungsmethodik, verbindliche Standards wie zum Beispiel Coding Guidelines sowie die zu verwendenden Werkzeuge und Kommunikationsmittel vorgestellt. Der Leitfaden richtet sich sowohl an individuelle Software-Entwickler:innen, die am Kitodo-Quellcode arbeiten möchten, als auch an Entscheider:innen, die Entwicklungsaufträge erteilen möchten und dabei die Kompatibilität der beauftragten Arbeiten zum quelloffenen Community-Produkt Kitodo gewährleisten wollen. Die Einhaltung der hier beschriebenen Regularien ist zwingende Voraussetzung für jede Teilhabe an der Kitodo-Entwicklung.

> [!IMPORTANT]
> Gemäß § 3.5 der Satzung haben sich Mitglieder des Vereins *Kitodo. Key to digital objects e. V.* insbesondere zur Einhaltung der in diesem Dokument beschriebenen Regeln verpflichtet. Dies gilt auch bei der Vergabe von Entwicklungsaufträgen an Dritte.

Die Festlegungen gelten für alle im Umfeld von Kitodo gemeinschaftlich entwickelten Komponenten ([Kitodo.Production](https://github.com/kitodo/kitodo-production), [Kitodo.Presentation](https://github.com/kitodo/kitodo-presentation), etc.) soweit sie für das jeweilige Produkt anwendbar sind. Nicht aus der gemeinschaftlichen Entwicklung hervorgegangener Quellcode, der zu einem Kitodo-Produkt beigesteuert wird, muss mindestens die beschriebenen Standards und Bedingungen zur Übernahme von Quellcode erfüllen.

## Werkzeuge und Kommunikation

**Die zentrale Entwicklungsplattform bildet [GitHub](https://github.com/kitodo).** Dort befinden sich das öffentliche Quellcode-Repository, ein Bug- und Featuretracker sowie ein Wiki zur Diskussion und Erarbeitung neuer Konzepte. **Dem zugrunde liegt das Versionsverwaltungswerkzeug [Git](https://git-scm.com/).** Zusätzlich ist es möglich, über GitHub das Release Management zu kontaktieren. Zur Nutzung von GitHub ist ein kostenloser Account notwendig.

**Generell sind alle Programmfehler im Bugtracker von GitHub zu melden. Sicherheitskritische Bugs können auch nur vertraulich dem Release Management bekannt gemacht werden, um erst nach ihrer Behebung veröffentlicht zu werden.** Auch Entwicklungsvorhaben sind nach Möglichkeit immer im GitHub-Bugtracker zu dokumentieren, mindestens aber vertraulich dem zuständigen Release Management mitzuteilen, um unwissentliche Doppelarbeit zu vermeiden.

**Zur Übernahme in den Hauptentwicklungszweig freigegebener Quellcode ist zwingend in Form eines auf dem Hauptentwicklungszweig basierenden Git-Branchs auf GitHub bereitzustellen und mittels der dort verfügbaren Funktion als Pull Request an die Release Manager zu melden.** Quellcode-Lieferungen auf anderem Weg können nicht berücksichtigt werden. Die eigentliche Entwicklung kann auch unter Beachtung der Anforderungen an eine dezentrale, funktionsgetriebene Entwicklung in einem privat angelegten lokalen Zweig stattfinden, der erst nach Abschluss der Programmierung zur Übernahme in den Hauptentwicklungszweig in GitHub eingestellt wird.

## Dezentrale, funktionsgetriebene Entwicklung

**Die Software-Entwicklung erfolgt im Kitodo-Kontext generell dezentral und funktionsgetrieben.** Nur das jeweils für das Produkt verantwortliche Release Management erhält schreibenden Zugriff auf den zentralen Hauptentwicklungszweig. Alle Weiterentwicklungen und Fehlerbehebungen finden in separaten Quellcode-Zweigen ([Branch](https://docs.github.com/articles/creating-and-deleting-branches-within-your-repository)) in eigenen Kopien des Repositories ([Fork](https://docs.github.com/articles/fork-a-repo)) statt, die jeweils aus dem aktuellen Hauptentwicklungszweig erzeugt werden müssen. **Entwicklungszweige, die nicht aus dem Hauptentwicklungszweig erzeugt wurden, können nicht wieder in diesen übernommen werden!** Ein Entwicklungszweig darf immer nur zur Erledigung eines einzigen, in sich abgeschlossenen Arbeitspakets dienen (also der Behebung genau eines Fehlers oder der Realisierung einer Funktionalität).

Nach Abschluss der Programmierung und erfolgreichem Test der Änderungen wird der Zweig zur Übernahme in den Hauptentwicklungszweig freigegeben ([Pull Request](https://docs.github.com/articles/creating-a-pull-request)). **Der Entwicklungszweig, von dem aus der Pull Request gestellt wurde, ist bis zur Übernahme in den Hauptentwicklungszweig aktuell zu halten, d.h. in der Zwischenzeit im Hauptentwicklungszweig vorgenommene Änderungen sind in den Entwicklungszweig des Pull Requests zu übernehmen.** Das Release Management unterzieht den Quellcode einer abschließenden Revision, wobei die Einhaltung formaler Kriterien sowie der Maßnahmen zur Qualitätssicherung (siehe unten) geprüft wird. **Die Revision ersetzt keine ordentlichen Funktions- und Leistungstests, diese liegen in der Verantwortung der Entwickler:innen!** Verläuft die Revision positiv, übernimmt das Release Management den Quellcode in den Hauptentwicklungszweig, verläuft sie negativ, gibt es den Entwicklungszweig zur Nachbearbeitung an die Entwickler:innen zurück.

Treten nach erfolgter Übernahme in den Hauptentwicklungszweig trotz Qualitätssicherung, Tests und Code-Revision Fehler auf, die eindeutig auf einen Pull Request zurückgeführt werden können, so müssen diese durch die für den Pull Request verantwortlichen Entwickler:innen binnen kurzer Frist behoben werden. Andernfalls kann das Release Management abhängig von der Signifikanz der Fehler zur Sicherstellung der Stabilität und Sicherheit von Kitodo den Pull Request rückabwickeln. Den Entwickler:innen steht es frei, den Pull Request erneut einzureichen.

Über den Zeitpunkt der Freigabe zur Quellcode-Übernahme entscheiden generell die Entwickler:innen, so dass zum Beispiel kommerzielle Entwicklungen durchaus eine gewisse Zeit zurückgehalten werden können. Da mit zunehmendem zeitlichem Abstand die Quellcode-Übernahme aufwändiger wird, sollte eine Freigabe jedoch spätestens 3 Monate nach Fertigstellung der Entwicklung erfolgen. **Eine Ausnahme stellen reine Fehlerbehebungen dar, die stets sofort nach Fertigstellung freigegeben werden müssen, sofern sie einen Fehler in einem öffentlichen Entwicklungszweig betreffen!**

> [!IMPORTANT]
> Siehe auch § 3.5 der Vereinssatzung, wonach diese Frist insbesondere für Vereinsmitglieder gilt.

## Maßnahmen zur Qualitätssicherung

Zur Verbesserung und Erhaltung der Software-Qualität von Kitodo wurden eine Reihe von Maßnahmen implementiert. Teilweise handelt es sich dabei um automatisierte, passive Prozesse, teilweise erfordern sie aber auch aktive Mitwirkung der Entwickler:innen.

Die passiven Prozesse sind in Form von GitHub Workflows implementiert, die verschiedene *Static Code Analyzer* und *Functional/Unit Tests* ausführen. Diese Prozesse starten automatisch, sobald ein Pull Request gestellt wird und ihr Ergebnis wird auf GitHub angezeigt. **Die Code-Revision durch das Release Management beginnt erst, wenn alle Prozesse erfolgreich durchlaufen wurden.** Die Repositorien enthalten alle Konfigurationen der Prüfwerkzeuge, so dass diese auch in lokalen Entwicklungsumgebungen ausgeführt werden können.

Kitodo verfügt in zunehmendem Maße über automatisierbare Software-Tests in Form von *Functional/Unit Tests*. **Diese Tests zu erstellen und zu pflegen ist essentieller Bestandteil der Software-Entwicklung und für jede:n Entwickler:in verpflichtend.** Das bedeutet, dass jede veränderte oder neu implementierte Funktionalität vollumfänglich durch entsprechende Tests abgedeckt werden muss. Diese müssen in einer Weise umgesetzt werden, die eine automatisierte Ausführung im Rahmen des bestehenden GitHub-Workflows ermöglicht. Darüber hinaus soll bei jeder Fehlerbehebung geprüft werden, ob ein erneutes Auftreten desselben Fehlers durch einen entsprechenden Test effektiv erkannt und damit vermieden werden kann.

Automatisierte Tests und passive Code-Analysen entbinden Entwickler:innen nicht von der Pflicht, vollumfängliche manuelle Tests durchzuführen, die sicherstellen, dass die entwickelte Funktionalität fehlerfrei funktioniert und keine ungewollten Nebeneffekte in anderen Funktionalitäten auftreten.

**Eine Übernahme von Pull Requests in den Hauptentwicklungszweig kann nur erfolgen, wenn alle Maßnahmen zur Qualitätssicherung erfolgreich angewendet wurden.** Dies liegt in der Verantwortung der Entwickler:innen, so dass entsprechende Mehraufwände bei Projektkalkulationen und Beauftragungen zu berücksichtigen sind.

## Coding Guidelines

**Entwicklungszweige dürfen nur die zur Erreichung des Entwicklungsziels notwendigen Änderungen beinhalten.** Rein kosmetische Anpassungen (z. B. der Formatierung) oder nicht-funktionale Ergänzungen (z. B. der Dokumentation) von ansonsten unveränderten Quellcode-Bereichen müssen daher in einem eigenen Entwicklungszweig vorgenommen werden und nicht mit funktionalen Änderungen einhergehen, um bei der Code-Übernahme in den Hauptentwicklungszweig die in ihrer Funktionalität veränderten Code-Bereiche schnell identifizieren zu können. Auch dürfen nicht mehrere Entwicklungsziele innerhalb desselben Entwicklungszweigs realisiert werden. Dies vereinfacht Funktions- und Leistungstests, verbessert die Transparenz des Entwicklungsprozesses und erleichtert die Revision durch das Release Management.

**Je nach verwendeter Technologie und Produkt sind zudem die folgenden Coding Guidelines einzuhalten.** Diese Standardisierung soll es den Entwickler:innen erleichtern, sich in fremdem Quellcode zurechtzufinden, und eine gleichbleibend hohe Code-Qualität gewährleisten.

### Allgemeingültige Standards

Diese Vereinbarungen gelten unabhängig von der verwendeten Programmiersprache und für alle Komponenten der Kitodo Suite gleichermaßen.

- Generell ist die Arbeitssprache Englisch, was insbesondere bei der Wahl von Variablen-, Klassen- und Methodennamen sowie der Quellcode-Dokumentation zu berücksichtigen ist. Die Kommunikation auf GitHub und den Mailinglisten kann dagegen auch auf Deutsch erfolgen.
- Die einschlägigen Regeln zur Wahl von sprechenden Bezeichnern und deren Schreibweise (`camelCase` oder `CamelCase`) sind zu beachten. Eine Ausnahme stellen Konstanten dar, die immer in Großbuchstaben geschrieben werden.
- Es ist objektorientiert zu entwickeln. Große Klassen und Methoden sind zu vermeiden. Jede Datei darf nur eine Klasse beinhalten und muss entsprechend der Klasse benannt sein.
- Die Zeichenkodierung ist UTF8, Zeilenumbrüche werden im Unix-Format (`\n`) kodiert, Einrückungen erfolgen mit Leerzeichen (4 Leerzeichen pro Einrückung). Jede Datei ist mit einem Zeilenumbruch abzuschließen.
- Jede Klasse, jede öffentliche Methode und jede Klassenvariable ist im phpDoc- bzw. JavaDoc-Standard zu dokumentieren. Der Quellcode sollte durch sprechende Bezeichnungen und kleine Methoden weitestgehend selbsterklärend sein. Zur Erläuterung von Funktionalität sollte im Quellcode von Zeilenkommentaren Gebrauch gemacht werden. Nicht-öffentliche Methoden müssen ebenfalls dokumentiert werden, wenn sie nicht trivial sind.
- Statt öffentlicher Klassen-Variablen sollten immer Getter- und Setter-Methoden verwendet werden. Setter sind immer `void`-Methoden, Getter haben keine Parameter. Innerhalb einer Klasse sollte der Zugriff auf private Variablen immer direkt erfolgen.
- Schleifen (`for`, `while`), Bedingungen (`if`, `else`) und vergleichbare Codeblöcke müssen immer in geschweiften Klammern eingeschlossen werden.
- Exceptions (`error`) müssen immer geeignet behandelt werden und gegebenenfalls bis zu der Stelle durchgereicht werden, an der dies möglich ist. Sie müssen abhängig vom konfigurierten Loglevel immer im Log registriert werden. Letzteres gilt auch für unkritische Programmfehler (`warning`) und Hinweise (`notice`).
- Alle Änderungen werden in den Commit Messages kurz, aber aussagekräftig dokumentiert. Ein Changelog innerhalb der Quellcodedateien wird dagegen nicht geführt.

### Kitodo.Presentation

Die Präsentationskomponente der Kitodo Digitalisierungssuite bildet eine Erweiterung (*Extension*) für das freie CMS [TYPO3](https://typo3.org/). Diese Extension enthält selbst alle wesentlichen Funktionsmodule einer modernen Digitalen Bibliothek, stellt zugleich aber auch eine umfangreiche API zur Entwicklung ergänzender Module (in Form eigener Extensions) bereit. **Für die Entwicklung sind die [Coding Guidelines des TYPO3-Projekts](https://docs.typo3.org/m/typo3/reference-coreapi/main/en-us/CodingGuidelines/Index.html) bindend.**

Zusätzlich gelten folgende, eventuell abweichende Vereinbarungen:

- Neue Frontend-Plugins und Backend-Module sollten in der Regel in Form eigener Extensions umgesetzt werden, um eine modulare Zusammenstellung der benötigten Komponenten zu ermöglichen. Nur Basisfunktionalitäten sollen Bestandteil der Extension `dlf` sein. Wann immer möglich, sind die APIs von TYPO3 und Kitodo zu nutzen.
- Die Extension `dlf` stellt den Kern der Präsentationsschicht dar und muss bei eigenen Extensions deshalb stets als Abhängigkeit deklariert genannt werden. Dazu muss die Paketverwaltung [Composer](https://getcomposer.org/) verwendet werden, über die die Extension unter dem Namen [`kitodo/presentation`](https://packagist.org/packages/kitodo/presentation) verfügbar ist.
- Frontend-Plugins und Backend-Module müssen immer von der Klasse `\Kitodo\Dlf\Common\AbstractController` abgeleitet werden, die wiederum von der entsprechenden Standardklasse von TYPO3 abgeleitet ist.
- Alle Klassen müssen den gemeinsamen Namensraum `\Kitodo\Dlf` bzw. der Verzeichnisstruktur entsprechende Unter-Namensräume verwenden. Verwendete Fremdklassen in abweichenden Namensräumen sind am Beginn der Datei mittels `use` zu deklarieren und im Quellcode ohne Angabe des Namensraums zu referenzieren.
- Alle URL-Parameter müssen den gemeinsamen Namensraum `tx_dlf` verwenden. Dadurch kann jedes Plugin bei Bedarf auf die Eingaben jedes anderen Kitodo-Plugins zugreifen.
- Bei der Dokumentation der Klassen, Methoden und Klassenvariablen sind mindestens die folgenden phpDoc-Schlüsselwörter in der angegebenen Reihenfolge zu verwenden (sofern zutreffend):
  - `@property[-read|-write]` für Klassen
  - `@param` und `@return` für Methoden
  - `@var` für Klassenvariablen
- Methoden müssen die Datentypen aller Parameter und des Rückgabewerts deklarieren. Mittels `declare(strict_types=1);` muss für jede PHP-Datei eine strikte Typisierung erzwungen werden.

### Kitodo.Production

Die Produktionskomponente der Kitodo Digitalisierungssuite bildet eine Webapplikation für einen Applikationsserver wie Tomcat oder Jetty. Generell werden hier die [Coding Standards von Scott Ambler](https://www.ambysoft.com/downloads/javaCodingStandards.pdf) als bindend betrachtet.

Zusätzlich gelten folgende, eventuell abweichende Vereinbarungen:

- Klassendateien sind entsprechend ihrer Package-Zugehörigkeit in der Verzeichnisstruktur abzulegen (z. B. Klasse `Foo`, Package `org.Kitodo.bar`: `src/org/Kitodo/bar/Foo.java`).
- Bezeichnungen für Datenbanken, Tabellen und Spalten sind durchgängig klein zu schreiben.
- Es müssen immer typsichere Listen verwendet werden (`ArrayList<Element> list;` bzw. `HashMap<Integer, String> map;`).
- Methoden, die Listen als Rückgabewert haben, sollen (z.B. im Fall von leeren Ergebnismengen) nie `null` zurückgeben. Stattdessen soll eine leere Liste zurückgegeben werden, um `NullPointerException` in den aufrufenden Methoden zu vermeiden.
- Öffentliche Methoden mit komplexen Datentypen als Parametern müssen auf diesen Null-Checks durchführen, um `NullPointerException` zu vermeiden.
- Klassen sollen immer einzeln importiert werden. Wildcard-Importe (`*`) sollen vermieden werden.
- Variablen sollen immer möglichst kleine Geltungsbereiche haben. Lokale Variablen sind in der Regel gegenüber Instanz- oder Klassenvariablen zu bevorzugen.
- Variablen, denen nach der Initialisierung im Programmcode keine neuen Werte zugewiesen werden, sollen immer mit dem Modifier `final` versehen werden.
- Jedes Frontend-Template bzw. jede Seite in der Applikation muss seine eigene Backing Bean haben. Diese Backing Beans sollen in der Regel im `ViewScope` des in Kitodo.Production eingesetzten Web-Frameworks JSF liegen. Abweichungen von dieser Regel müssen begründet werden.
- Der Quellcode muss mit dem mitgelieferten Codeformatter formatiert sein.
- Lesbarkeit und Wartbarkeit haben prinzipiell eine höhere Priorität als Kompaktheit. Verkettungen von Ausdrücken in einer Zeile oder Anweisung sollen vermieden werden, wenn sie die Lesbarkeit des Codes negativ beeinträchtigen.

## Versionierung und Releasezyklen

Kitodo verwendet [Semantic Versioning](https://semver.org/), d. h. das stets dreiteilige Versionsschema unterscheidet zwischen reinen Fehlerbehebungen und nicht-funktionalen Änderungen (*Patch Version*), funktionalen Erweiterungen und Aktualisierungen von Abhängigkeiten (*Minor Version*) sowie tiefergreifenden Änderungen etwa der Architektur, des Datenmodells oder grundlegender Basiskomponenten (*Major Version*). Für jede Major Version wird auf GitHub ein eigener Code-Branch gepflegt, so dass mehrere Major Versionen parallel entwickelt und gepflegt werden können. Minor und Patch Versionen werden innerhalb dieser Branches mit Tags gekennzeichnet. In Ausnahmefällen können auch für Minor Versionen eigene Branches angelegt werden.

Das Release Management pflegt und betreut neben der Weiterentwicklung im Main Branch die Branches der jeweils aktuellsten Major Version (Stable). Entsprechend sind die Entwickler:innen aufgefordert, Bugfixes für beide Branches zur Verfügung zu stellen, sofern ein Fehler in beiden Versionsständen auftritt. Im Falle von sicherheitskritischen Fehlern wird darüber hinaus die vorherige Major Version (Old Stable) mit dem passenden Bugfixing versorgt. Die jeweils unterstützten Major Versionen können dem Dokument `SECURITY.md` im Quellcode-Repository entnommen werden.

Funktionale Weiterentwicklungen müssen stets für das aktuelle oder zukünftige Stable Release erfolgen und können optional in einem separaten Pull Request zusätzlich auch in das Old Stable Release eingebracht werden. Fehlerbehebungen müssen immer in allen noch unterstützten und betroffenen Major Versionen erfolgen.

Es wird ein kontinuierlicher Entwicklungszyklus mit zwei funktionalen Releases pro Jahr angestrebt. Abhängig vom Umfang der Änderungen können dies Minor oder Major Versionen sein. Dazwischen werden bedarfsgerecht Patch Versionen veröffentlicht. Zur Vorbereitung von funktionalen Releases entscheidet das Release Management ca. 3 Monate vor dem angestrebten Release-Datum über den sogenannten *Feature Freeze*. Ab diesem Zeitpunkt werden keine weiteren funktionalen Änderungen mehr für das kommende Release akzeptiert, sondern nur noch Fehlerbehebungen, Detailverbesserungen sowie allgemeine Wartungs- und Pflegemaßnahmen. Zwischenzeitlich eingehende Feature-Entwicklungen werden erst in das übernächste Release aufgenommen.

Einem funktionalen Release kann ein *Release Candidate* vorausgehen. Dabei handelt es sich um eine vollständige Vorab-Version der anstehenden Veröffentlichung, die jedoch noch nicht unter Produktivbedingungen getestet wurde. Ein Release Candidate dient dem intensiven Testen durch die Community, um vor dem tatsächlichen Release mögliche Fehler zu identifizieren und zu beheben.

## Koordinierung der Entwicklungsvorhaben

**Sämtliche Entwicklungsvorhaben sollten öffentlich dokumentiert und müssen dem zuständigen Release Management mitgeteilt werden.** Das Release Management behandelt diese Mitteilungen auf Wunsch vertraulich. Dies dient der Vermeidung von Parallelentwicklungen und somit einer stärkeren Bündelung von Entwicklungsressourcen der Community sowie einer verlässlichen Release-Planung.

**Da für die Revision von Code-Freigaben und die Übernahme in den Hauptentwicklungszweig Ressourcen des Release Managements benötigt werden, diese aber in der Regel zeitnah erfolgen müssen, sollte der Entwicklungsplan größerer Vorhaben frühzeitig mit dem Release Management abgestimmt werden.** Nur dann kann das Release Management entsprechende Ressourcen zur jeweils benötigten Zeit widmen und dadurch zu einem verzögerungsfreien Projektverlauf beitragen.
