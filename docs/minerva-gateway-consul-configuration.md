# Konfiguration für das Gateway

## File-Struktur

```
<consul>
|
|__config
   |  
   |__minerva-gateway
      |  application.yml
```

## config/minerva-gateway/application.yml

Folgender Inhalt muss geändert werden:

* service-id: Id des neuen Services z.B. demo-api
* microservice-name: Name des Microservices, mit dem er sich beim Loadbalancer anmeldet.
* host: Host des Keycloack-Servers
* port: Port des Keycloack-Servers
* realms-name: Name des Realms. Default ist "master"
* Authentication-name: Name der Authentifizierungsart. Wird bei der Auswahl im Login-Fenster angezeigt.
* client-id: Client-ID welche unter Keycloack existieren muss.
* client-secret: Wird für den Client generiert.

``` yaml
spring:
  cloud:
    loadbalancer:
      ribbon:
        enabled: false
        
    gateway:
      default-filters:
        - TokenRelay
      routes:
        - id: <service-id>
          uri: lb://<microservice-name>/
          predicates:
            - Path=/**
          filters:
            - RemoveRequestHeader=Cookie
  security:
    oauth2:
      client:
        provider:
          keycloak:
            token-uri: http://<host>:<port>/auth/realms/<realm-name>/protocol/openid-connect/token
            authorization-uri: http://<host>:<port>/auth/realms/<realm-name>/protocol/openid-connect/auth
            userinfo-uri: http://<host>:<port>/auth/realms/<realm-name>/protocol/openid-connect/userinfo
            user-name-attribute: preferred_username
        registration:
          <Authentication-name>:
            provider: keycloak
            client-id: <client-id>
            client-secret: <client-secret>
            authorization-grant-type: authorization_code
            redirect-uri: "{baseUrl}/login/oauth2/code/keycloak"

# Example for Loglevel
logging.level:
  org.springframework.cloud.gateway: DEBUG
  org.springframework.security: DEBUG
  org.springframework.web.reactive.function.client: TRACE
  org.springframework.security.web.server.util.matcher.PathPatternParserServerWebExchangeMatcher: INFO
  org.springframework.security.web.server.context.WebSessionServerSecurityContextRepository: INFO
  org.springframework.cloud.gateway.filter.GatewayMetricsFilter: INFO
  org.springframework.security.web.server.util.matcher.OrServerWebExchangeMatcher: INFO

```