# Visualisierung von Konstruktionsbeschreibungen mit JSXGraph

## Die Tools und Beispiele

Im mechanisierten Beweisen geometrischer Theoreme wie auch im Design von
Dynamischer Geometrie-Software (DGS) spielen Konstruktionsbeschreibungen in
Form von linearen Geometrieprogrammen (Geometric straight-line programs) eine
zentrale Rolle, wobei in DGS zusätzliche Layoutinformationen zu den einzelnen
geometrischen Objekten vorgehalten werden müssen.

Mit den [GeoProofSchemes](https://symbolicdata.github.io/Geo) des
[Symbolicdata-Projekts](https://symbolicdata.github.io/) liegen "generische"
Konstruktionsbeschreibungen vor, die als Eingaben für das mechanisierte
Geometriebeweisen dienen und teilweise in ein Format überführt wurden, das
auch für den Import in ein DGS prinzipiell geeignet ist, wenn die freien
Parameter angemessen belegt werden.  Dies lässt sich für verschiedene Typen
der GeoProofSchemes mit den aktuell verfügbaren DGS-Konzepten verschieden
genau realisieren.

Mit der Javascript basierten DGS [JSXGraph](https://jsxgraph.org) liegt
zugleich eine Abspielumgebung vor, die
* quelloffen bei [github](https://github.com/jsxgraph/jsxgraph) gehostet wird
* und behauptet, Konstruktionsbeschreibungen in verschiedenen Formaten einlesen
zu können.

Die hier im Rahmen eines Praktikums (im Jahr 2018) erstellten Lösungen haben
dieses Eingabeformat analysiert und eine Datenbasis mit verschiedenen
Beispielen für JSXGraph aufgebaut (hier ist nur dieser für das Logo-Projekt
wesentliche Teil der im Praktikum erstellten Materialien enthalten).  Dabei
sollten auch GeoProofSchemes für den Upload in JSXGraph aufbereitet werden.

## GeoProofSchemes

138 von 297 Beispielen sind konstruktiv. Alles wird aus Punkten konstruiert.

Dynamische Elemente:
* Point(x,y)  - freier Punkt
* varpoint(A,B,u) - Geradengleiter auf Gerade durch zwei gegebene Punkte
* line_slider(a,u) - Geradengleiter auf Gerade ohne zwei Punkte
* circle_slider(M,A,u) - Gleiter auf Kreis um M mit A auf der Peripherie

Typen:
* Point
* Distance (eigentlich auch Scalar)
* Scalar
* Line
* Circle
* Boolean
* Angle

Die Konstruktionswerkzeuge sind in der Datei GeoCode.ttl im Turtle-Format
beschrieben.

## GeoGebra in JSXGraph verwandeln. Verzeichnis ggb2jsxGraph

Speicherformat und Zusammenhang zu JSXGraph ist in 
- Peter Wilfahrt: Geogebra in JSXGraph. Hausarbeit, Bayreuth 2009
genauer beschrieben. Download unter `Texte/GeogebraInJSXGraph.pdf`.

Siehe auch `examples/ggb/praesentation/ggb-in-jxg.pdf` im jsxgraph Repo und
`GeoGebra-Examples`.

Eine GeoGebra-Datei ist ein gezipptes Archiv, bestehend aus einigen
Hilfsdateien und einer XML-Datei.  Die XML-Datei enthält die Daten, aus denen
die gespeicherten Konstruktionen rekonstruiert werden können.  Die anderen
Dateien spielen eine untergeordnete Rolle.  Ein Element einer Konstruktion
(bspw. ein Punkt) ist mit dem Tag <element> versehen, eine Folge solcher
Elemente beschreibt die Konstruktion.  

Typische Strukturelemente (Elementname, Attribute) sind
* tag "element": Attribute type="point", label - Punkte als elementare Objekte
  * coords x,y,z=1
  * animation -> wenn beweglicher Punkt
* tag "command": Attribute name="Line", label
  * input a0, a1, a2 ...
  * output a0, a1, a2, ...
* Nach jedem tag "command" ein tag "element", welches die Style-Eigenschaften
  weiter beschreibt.
  * coords x,y,z  - Koordinatenattribut
  * eqnstyle="implicit"
* command names: Line, Midpoint, Segment, OrthogonalLine, Intersect, 
* name="Circle" type="conic"
  * eigenvectors x0,y0,z0, x1,y1,z1
  * matrix A0..A5

Mehr zum GeoGebra-XML-Format unter
<https://wiki.geogebra.org/en/Reference:XML>.

Die Applikation parst eine ggb- oder geoProofScheme-Datei und visualisiert
diese mit JSXGraph. Verwendet die Datei `src/reader/geogebra.js` aus dem
jsxgraph Repo zum Parsen der ggb-Datei.

Rufe dazu `ggb2jsxGraph/index.html` auf und lade Beispiele __aus diesem
Verzeichnis__.

## CIPS

CIPS (cips.jar) ist eine Java-Application, um das GeoProofScheme-Format (u.a.)
in JSXGraph zu tramsformieren.

Mehr dazu in der [README-Datei](CIPS/README.md) und auf den [Folien der
Präsentation](CIPS/cips.pdf).

## DisplayWithJSXGraph

Diese Lösung verwendet den im jsxgraph Repo implementierten Workflow zur
Anzeige von Konstruktionen, die im Intergeo-Format in einer Datei in einem der
Verzeichnisse Example-1 oder Example-2 vorliegen:

* Starte einen HTTP-Server auf Port 8000
* Öffne `testcases.html` in einem Webbrowser. Benötigt
  * distrib/jsxgraph.css
  * distrib/prototype.js
  * src/loadjsxgraph.js
  * src/reader/intergeo.js 
  * loadJSXG.js - definiert onchange-Funktion loadJSXG() zur Auswertung der
    Select-Tabelle
* Mit `board = JXG.JSXGraph.loadBoardFromFile('jxgbox', fname , 'Intergeo')`
  wird vom File `fname` die Konstruktion in das JXG.Board `board` geladen.
* Das Board wird in ein div-Element mit id="jxbox" und class="jxbox" geladen
  und dort interaktiv angezeigt. 

Damit existiert eine einfache Möglichkeit, eine Konstruktion im
Intergeo-Format in JSXGraph einzuladen, wenn sie nur die generisch gegebenen
Konstruktionswerkzeuge verwendet.  Es bleibt zu klären, wie man das um weitere
Konstruktionswerkzeuge erweitern kann, die etwa als Macros gegeben sind.
