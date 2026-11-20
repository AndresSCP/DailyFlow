# DailyFlow

DailyFlow es una aplicación móvil híbrida para organizar tareas diarias de casa, estudios, trabajo y entrenamiento. Está desarrollada con Ionic y Angular y se ejecuta en Android mediante Capacitor.

## Funcionalidades

- **Organización de tareas.** El menú principal da acceso a las cuatro categorías de tareas.
- **Registro e inicio de sesión local.** Las cuentas se guardan en SQLite. Un `AuthGuard` controla el acceso al menú principal y a las pantallas internas.
- **Cámara y ubicación.** La app incluye pantallas para tomar fotos y mostrar la ubicación actual en un mapa. El mapa usa Google Maps y requiere conexión.
- **Integración REST de demostración.** Un servicio Angular consume [JSONPlaceholder](https://jsonplaceholder.typicode.com/) para consultar y simular operaciones sobre publicaciones.

## Tecnologías

| Área | Herramientas |
| --- | --- |
| Interfaz y navegación | Ionic 8, Angular 20 e Ionicons |
| Lenguaje y datos reactivos | TypeScript 5.8 y RxJS 7.8 |
| Integración con Android | Capacitor 7, Camera y Geolocation |
| Almacenamiento de usuarios | SQLite mediante `cordova-sqlite-storage` |
| Pruebas unitarias | Jasmine y Karma |

## Puesta en marcha

Necesitas Git, Node.js 22.12 o superior dentro de la rama 22 y npm. Para ejecutar la app en Android, instala también Android Studio con el SDK de Android 35.

```bash
git clone https://github.com/AndresSCP/DailyFlow.git
cd DailyFlow
npm ci
```

### Vista de desarrollo en el navegador

```bash
npm start
```

Abre [http://localhost:4200](http://localhost:4200). Esta vista sirve para revisar la interfaz. Para probar el registro y el inicio de sesión, usa Android, ya que el flujo depende del plugin nativo de SQLite.

### Ejecutar en Android

```bash
npm run build
npx cap sync android
npx cap open android
```

En Android Studio, elige un emulador o conecta un dispositivo físico y presiona **Run**. El proyecto está configurado con Android API 23 como mínimo y SDK 35 para la compilación. Después de modificar el código web, vuelve a compilar y sincronizar antes de ejecutar la app.

El repositorio también incluye un [APK de demostración](./app-release.apk). Para probar el flujo local, registra una cuenta con datos ficticios y accede desde la pantalla de inicio de sesión. Para probar la cámara y el mapa, concede los permisos correspondientes cuando la app los solicite.

## Estructura del proyecto

| Ruta | Contenido |
| --- | --- |
| [`src/app/app-routing.module.ts`](src/app/app-routing.module.ts) | Rutas públicas y protegidas con carga diferida |
| [`src/app/services/`](src/app/services/) | Autenticación, acceso a SQLite e integración REST |
| [`src/app/pages/`](src/app/pages/) | Pantallas de cámara y mapa |
| [`src/app/`](src/app/) | Menú principal, registro y pantallas por categoría |
| [`android/`](android/) | Proyecto nativo de Android |
| [`capacitor.config.ts`](capacitor.config.ts) | Configuración de Capacitor y carpeta web `www` |

## Alcance de la versión actual

SQLite almacena las cuentas locales. La pantalla de tareas de casa mantiene sus tareas en memoria. La autenticación es de demostración y guarda las contraseñas en texto plano, así que usa datos ficticios. El servicio REST y el mapa requieren acceso a Internet.
