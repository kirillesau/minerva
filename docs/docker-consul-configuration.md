# Konfiguration für Anwendungen in einem Docker-Compose

Jede Applikation meldet sich beim Start an dem Discovery Server an. Entscheidet man sich für die Skalierung einer
Anwendung, so wird jede nachfolgende Instanz die vorherige überschreiben, da die Instanz-ID identisch zur vorherigen
ist. Um dies zu umgehen, kann die Instanz-ID beim Start angepasst werden. Mit `${server.port}-${spring.cloud.client.hostname}` wird beim Start der Host und der Port mitgegeben, was die Instanz-ID einzigartig macht.

## File-Struktur

```
<consul>
|
|__config
   |  
   |__defaults,docker
      |  application.yml
```

## config/defaults,docker/application.yml

``` yaml
spring:
  cloud:
    consul:
      discovery:
        instance-id: ${spring.application.name}-${server.port}-${spring.cloud.client.hostname}
```