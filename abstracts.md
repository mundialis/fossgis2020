### FOSS in der Cloud (Talk)


Mit den täglich wachsenden Geodatenpools, z.B. angereichert durch das Copernicus oder Landsat Programm, steigen die Anforderungen an Hard- und Software für die Geodatenprozessierung (nicht nur) im Bereich der Fernerkundung stetig an. Lokale Installationen können dabei die Datenmengen und Anforderungen an Echtzeit-Analysten kaum stemmen und sind daher in den letzten Jahren vermehrt durch verteilte Systeme in der Cloud abgelöst worden. Dieser Trend macht auch vor dem Bereich der FOSS keinen Halt und hat sich seither etabliert.
Dieser Vortrag soll einen Überblick über die Konzepte des Cloud Computings, der verfügbaren Tools und Voraussetzungen der serviceorientierten Architektur für eine erfolgreiche Skalierbarkeit geben. Anschließend wird anhand eines konkreten Beispiels basierend auf den Komponenten actinia, GRASS GIS, GeoServer und SHOGun demonstriert wie diese für einen reibungslosen Betrieb in der Cloud angepasst werden müssen. Abgerundet wird der Vortrag durch Erfahrungen und daraus abgeleiteten Empfehlungen, die während der Vorbereitung und zur Laufzeit der Architektur gesammelt wurden.


Mit den täglich wachsenden Geodatenpools steigen Anforderungen an Hard- und Software. Lokale Installationen sind in den letzten Jahren vermehrt durch verteilte Systeme in der Cloud abgelöst worden, welche sich auch im Bereich der FOSS etabliert haben.
Dieser Vortrag gibt einen Überblick über Konzepte des Cloud Computings, der verfügbaren Tools und Voraussetzungen für eine erfolgreiche Skalierbarkeit, sowie Erfahrungen und Empfehlungen am Beispiel von actinia, GRASS GIS, GeoServer und SHOGun.


https://github.com/mundialis/actinia_core, https://github.com/OSGeo/grass, https://github.com/geoserver, https://github.com/terrestris/shogun-core
actinia, GRASS GIS, GeoServer und SHOGun.



### GRASS GIS in der Cloud: actinia Geoprozessierung (Talk)


Ursprünglich GRaaS (GRASS as a Service) genannt, wurde actinia entwickelt, um GRASS GIS Funktionalität über eine HTTP REST API bereitzustellen. GRASS GIS Locations, Mapsets und Geodaten werden zu Ressourcen, die per REST verwaltet und visualisiert werden können. Actinia folgt dem Paradigma, Algorithmen zu Clouddaten zu bringen und unterstützt u.a. persistente und flüchtige Berechnung, Benutzerverwaltung zur Begrenzung von Pixeln, Prozessen und Berechnungsdauer.


Ursprünglich GRaaS (GRASS as a Service) genannt, wurde actinia (https://actinia.mundialis.de) entwickelt, um die GRASS GIS Funktionalität über eine HTTPS REST API bereitzustellen. GRASS GIS Locations, Mapsets, Vektor- und Rasterdaten sowie raum-zeitliche Daten werden zu Ressourcen, die per REST verwaltet und visualisiert werden können. Mit den bestehenden (z.B. Landsat) und in den letzten Jahren neu entstehenden (Copernicus Sentinel) großen Geodatenpools, die Tag für Tag wachsen, soll actinia dem Paradigma folgen, Algorithmen zu den Clouddaten zu bringen. Actinia ermöglicht es, eine große Menge an Geoinformationen aufzubereiten, zu analysieren und bereitzustellen, ohne dass Kenntnisse der Daten, der Analyse, der geeigneten Software zur Automatisierung oder skalierbarer Hardware-Ressourcen erforderlich sind.
Einige der Funktionalitäten sind persistente und flüchtige Berechnung, Benutzerverwaltung zur Begrenzung von z.B. Pixeln, Prozessen und Berechnungsdauer sowie das Loggen von API-Aufrufen und verwendeten Ressourcen durch jeden Benutzer. Ein weiterer Vorteil ist die einfache Installation mit Docker. Bei der Installation in einer Cloud Umgebung mit OpenShift oder Kubernetes verwaltet der integrierte Loadbalancer das Cluster automatisch.
Dem Geist von FOSS folgend sind wir stolz, ein OSGeo-Community-Projekt geworden zu sein und freuen uns auf die Erweiterung der actinia-Community.

Der Vortrag gibt eine Übersicht über Konzepte und grundlegende Funktionalitäten von actinia.



### GRASS GIS per HTTP: actinia Geoprozessierung (Workshop)


Actinia ist eine Open-Source-REST-API für die skalierbare, verteilte, leistungsstarke Verarbeitung von Geodaten, die intern hauptsächlich GRASS GIS für Rechenaufgaben verwendet. Die Kernfunktionalität umfasst die Verarbeitung von Einzel- und Zeitreihen von Satellitenbildern, von Raster- und Vektordaten. In diesem Kurs werden wir grundlegende GRASS GIS Konzepte vorstellen, eine kurze Einführung in HTTP REST und Cloud-Verarbeitungskonzepte geben und in die Prozessierung mit actinia einführen.


Actinia (https://actinia.mundialis.de) ist eine Open-Source-REST-API für die skalierbare, verteilte, leistungsstarke Verarbeitung von Geodaten, die intern hauptsächlich GRASS GIS für Rechenaufgaben verwendet. Die Kernfunktionalität umfasst die Verarbeitung von Einzel- und Zeitreihen von Satellitenbildern, von Raster- und Vektordaten. Mit den bestehenden (z.B. Landsat) und in den letzten Jahren neu entstehenden (Copernicus Sentinel) großen Geodatenpools, die Tag für Tag wachsen, soll actinia dem Paradigma folgen, Algorithmen zu den Clouddaten zu bringen. Actinia ist seit 2019 ein OSGeo Community Projekt.

In diesem Kurs werden wir kurz grundlegende GRASS GIS Konzepte vorstellen und eine kurze Einführung in HTTP REST und Cloud-Verarbeitungskonzepte geben. Es folgt eine Einführung in die Prozessierung mit actinia sowie praktische Übungen, um das Thema besser kennenzulernen.

https://actinia.mundialis.de/, https://github.com/mundialis/actinia_core
