# Projekt Minerva

Dieses Projekt dient zur Einarbeitung in diverse Softwarearchitekturen, Frameworks und Design-Pattern.

## Beschreibung

Um die Einarbeitung in die Themen zu erleichtern, wird ein Projekt aufgesetzt und stetig erweitert. Am Ende soll eine
Architektur entstehen mit einem Backend und mehreren Frontends.

## Konfiguration

Die Konfigurationen für die einzelnen Microservices werden über consul geregelt. Über den Key-Value-Store können die
Konfigurationen nach dem Start der Anwendung abgerufen werden. Die in diesem Projekt vorhandenen Konfigurationen sind
aus den folgenden Dateien zu entnehmen:

* [minerva-gateway](docs/minerva-gateway-consul-configuration.md)
* [docker-compose](docs/docker-consul-configuration.md)

## Disclaimer

Die verwendeten Lösungen in diesem Projekt müssen für die Aufgabenstellung nicht zwingend Sinn ergeben. In erster Linie
dient dieses Projekt dazu gelernte Themen in der Praxis anzuwenden.

## Lizenz

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.