# Plan de Implementación - Gestión Global de Sesión y Fix Error 403

Este plan describe cómo implementar un sistema de cierre de sesión global y automático cuando el servidor rechaza el acceso (Error 403), evitando que el usuario quede atrapado en pantallas de error dentro del menú principal.

## Proposed Changes

### [Component Name] Núcleo y Red

---

#### [MODIFY] [main.dart](file:///D:/MOVILES/front/lib/main.dart)
- Crear una `GlobalKey<NavigatorState> navigatorKey` global.
- Configurar el `MaterialApp` para usar esta llave. Esto permite navegar desde archivos que no son widgets (como el cliente de API).

#### [MODIFY] [api_client.dart](file:///D:/MOVILES/front/lib/core/api_client.dart)
- **Detección de 403**: Si una petición devuelve `403 Forbidden`, invocar un método de "Logout Forzado".
- **Logout Forzado**:
    - Limpiar `TokenStorage`.
    - Cerrar sesiones de chat.
    - Redirigir inmediatamente a la pantalla `/welcome` usando la `navigatorKey`.

### [Component Name] Pantallas

---

#### [MODIFY] [welcome_screen.dart](file:///D:/MOVILES/front/lib/screens/welcome/welcome_screen.dart)
- Reforzar el auto-login para que sea más silencioso y no cause parpadeos si la sesión es inválida.

## Verification Plan

### Manual Verification
1. **Simulación de 403**: Forzar una respuesta 403 desde el backend o usar un token expirado manualmente.
2. **Auto-Redirección**: La app debe detectar el 403 en la primera petición (usualmente la de cargar el perfil) y sacar al usuario automáticamente a la pantalla de bienvenida.
3. **Persistencia**: Verificar que tras ser expulsado, el almacenamiento quede limpio y no intente re-ingresar solo.
