### Keycloak Integration with Spring Security

Tutorial article > https://medium.com/javarevisited/keycloak-integration-with-spring-security-6-37999f43ec85

1. Create realm
REALM_NAME = MySuperApplicationRealm
2. Create client
CLIENT_ID = my-super-client (In the next screens, keep the default configurations and save. Now the client was successfully created.)
3. Clients > my-super-client > Settings: Valid redirect URIs = http://localhost:8080/* (Spring Boot App on port 8080)
4. Creating Roles
Clients > my-super-client > Roles: Create role : admin, user ->>
Role name   Composite
admin       False
user        False
5. Realm roles > Create role : app_admin, app_user
app_admin > Action--Add associated roles > Filter by clients: my-super-client:admin
app_user > Action--Add associated roles > Filter by clients: my-super-client:user
If you added those correctly, Realm roles will be composite.
Role name   Composite
admin       True
user        True
6. Creating Users > Users:

username    email                       email verified
user1       user1@myapplication.com     yes
user2       user2@myapplication.com     yes
user3       user3@myapplication.com     yes

user1:Credentials >> Set password (Temporary -> On)
user2:Credentials >> Set password (Temporary -> On)
user3:Credentials >> Set password (Temporary -> On)

user1:Role mapping -> Assign role -> app_admin
user2:Role mapping -> Assign role -> app_user
user3:Role mapping -> Assign role -> app_admin, app_user

7. Realm settings -> Endponts:OpenID Endpoint Configuration -> token_endpoint
Postman ->
POST http://keycloak.local:8181/realms/MySuperApplicationRealm/protocol/openid-connect/token
Body -> x-www-form-urlencoded
grant_type:password
client_id:my-super-client
username:user2
password:******

