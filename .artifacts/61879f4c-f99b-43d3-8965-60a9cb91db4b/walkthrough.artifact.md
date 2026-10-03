# Walkthrough - Solución a Bloqueo de Sesión y Error 403

Se ha implementado un mecanismo de seguridad global que detecta cuando la sesión del usuario ha expirado o ha sido rechazada por el servidor (Error 403), redirigiendo automáticamente a la pantalla de inicio y limpiando los datos locales.

## Cambios Realizados

### 🛡️ Redirección Global de Seguridad
- **Navegador Independiente**: Se configuró una `navigatorKey` en [main.dart](file:///D:/MOVILES/front/lib/main.dart). Esto permite que la aplicación cambie de pantalla desde cualquier lugar del código, incluso si no estamos dentro de un widget (como en el cliente de red).
- **Controlador de Errores Críticos**: El [api_client.dart](file:///D:/MOVILES/front/lib/core/api_client.dart) ahora vigila todas las respuestas del servidor. Si detecta un error **401 (Unauthorized)** que no se puede refrescar o un **403 (Forbidden)**:
    1. Imprime un log de emergencia: `🚨 SESSION EXPIRED`.
    2. Borra instantáneamente todos los tokens del dispositivo.
    3. Expulsa al usuario hacia la pantalla de **Welcome**, bloqueando el acceso al menú principal.

### 🔄 Rompiendo el Bucle de Error
Anteriormente, si la sesión era inválida, la app intentaba cargar el perfil y mostraba un mensaje de error 403, pero se quedaba en la misma pantalla. Con este cambio, el primer fallo de autenticación disparará la salida automática, garantizando que el usuario siempre vea la pantalla de login/registro si su sesión ya no sirve.

## Verificación

1. Realiza un **Hot Restart (`R`)**.
2. Si tenías un error 403 persistente, notarás que la app ahora te llevará de inmediato a la pantalla de **Welcome**.
3. Al intentar ingresar de nuevo con tus credenciales correctas, la sesión se restablecerá y el error desaparecerá.

> [!CAUTION]
> Este cambio es fundamental para la seguridad: evita que la app intente usar tokens viejos o corruptos infinitamente contra el servidor.
