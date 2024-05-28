## Scenarios for Security Design:
### Scenario 1: Pseudo-Code for Authentication System

#### Pseudo-Code Example:
```
FUNCTION authenticateUser(username, password):
  QUERY database WITH username AND password
  IF found RETURN True
  ELSE RETURN False
```
**Analisis**: El fragmento anterior carece de un mecanismo de ocultamiento de información sensible (hasheo del password) y en caso de que la autenticación sea exitosa podría modelarse una respuesta que contenga un token y su tiempo de expiración.

```
FUNCTION authenticateUser(username, password):
  DECRYPT pasword
  QUERY database WITH username AND password
  IF found RETURN TOKEN
  ELSE RETURN BadRequest
```

### Scenario 2: JWT Authentication Schema

#### Design Outline:
```
DEFINE FUNCTION generateJWT(userCredentials):
  IF validateCredentials(userCredentials):
    SET tokenExpiration = currentTime + 3600 // Token expires in one hour
    RETURN encrypt(userCredentials + tokenExpiration, secretKey)
  ELSE:
    RETURN error
```
**Analisis**: Este pseudocódigo necesita firmar el token generado, determina correctamente el tiempo de expiración, tal vez utilizar el identificador para generar el token y utilizar en lugar del encrypt() una función de jwt para firmar el token con el secreto que elegimos 

```
DEFINE FUNCTION generateJWT(userCredentials):
  DECRYPT userCredentials.password
  IF validateCredentials(userCredentials):
    QUERY database WITH username
    SET tokenExpiration = currentTime + 3600 // Token expires in one hour
    RETURN jwt.sign(id + tokenExpiration, secretKey)
  ELSE:
    RETURN error
```

### Scenario 3: Secure Data Communication Plan

#### Outline for Data Protection:

```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols
```

**Analisis**: Dado que ya se está implementando SSL/TLS, podemos añadir el uso de Cookie Security Configuration para garantizar el uso de HTTPS, uso de cookie en el mismo sitio y evitar el acceso a la misma.

```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  SET cookie configuration Set-Cookie: SID=12345; Secure; HttpOnly; SameSite=Strict
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols
```
