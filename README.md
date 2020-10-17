# SpringCloudGateway-Oauth2-Keylocke

https://piotrminkowski.com/2020/10/09/spring-cloud-gateway-oauth2-with-keycloak/

We are running Keycloak on a Docker container. By default, Keycloak exposes API and a web console on port 8080. However, that port number must be different than the Spring Cloud Gateway application port, so we are overriding it with 8888. We also need to set a username and password to the admin console.

$ docker run -d --name keycloak -p 8888:8080 \
   -e KEYCLOAK_USER=spring \
   -e KEYCLOAK_PASSWORD=spring123 \
   jboss/keycloak
Then we need to create two clients with the same names as defined inside the gateway configuration. Both of them need to have confidential in the “Access Type” section, a valid redirection URI set. We may use a simple wildcard while setting the redirection address as shown below.
The client spring-with-test-scope will have the scope TEST assigned. In contrast, the second client spring-without-test-scope will not have the scope TEST assigned.

you need to change both application.yml according to KEYCLOAK clients like 
client-secret: 3e352297-4788-4669-be56-185c2194c826,
issuer-uri: http://localhost:8888/auth/realms/master etc.
