#### Descripción 
Proper session timeout controls are critical for securing user accounts. If a user logs in on a public or shared computer but doesn’t explicitly log out (instead simply closing the browser tab), and session expiration dates are misconfigured, the session may remain active indefinitely.This then allows an attacker using the same browser later to access the user’s account without needing credentials, exploiting the fact that sessions never expire and remain authenticated.

Additional details will be available after launching your challenge instance.
#### Solución
El análisis del sistema reveló que la aplicación web implementa un manejo inseguro de sesiones. Al interactuar con el endpoint `/sessions`, se observó que el servidor exponía información de sesiones activas, incluyendo identificadores de sesión (`session ID`) junto con los usuarios asociados.
```
session:HL-yYvYHIxTmkr0ALRQSg9PplW7FRVWpnTHTgyjwKkM, {'_permanent': True, 'key': 'admin'}
```
Esto indica que el identificador de sesión pertenece al usuario **admin**.

Dado que las sesiones estaban configuradas como permanentes (`_permanent: True`) y no existía control de expiración, fue posible reutilizar directamente este identificador de sesión sin necesidad de autenticarse como administrador.

El procedimiento fue el siguiente:

1. Acceder al endpoint `/sessions` para obtener un `session ID` válido del usuario administrador.
    
2. Interceptar una petición HTTP utilizando Burp Suite o las herramientas de desarrollador del navegador.
    
3. Reemplazar el valor de la cookie `session` por el `session ID` correspondiente al usuario admin.
    
4. Enviar la petición modificada al servidor.
    
5. Acceder a rutas restringidas (por ejemplo `/admin` o `/`) ya autenticado como administrador.
    

Como resultado, se obtuvo acceso privilegiado y se pudo visualizar la bandera (flag) del reto.
#### Notas
- **Exposición de sesiones activas**  
    El endpoint `/sessions` permite visualizar identificadores de sesión junto con los usuarios asociados, lo cual no debería ser accesible públicamente.
    
- **Falta de expiración de sesión**  
    Las sesiones están marcadas como permanentes (`_permanent: True`), lo que permite reutilizarlas indefinidamente.
    
- **Ausencia de validación adicional**  
    El servidor confía únicamente en el `session ID` para autenticar al usuario, sin validaciones adicionales como IP, User-Agent o regeneración de sesión.
#### Referencias