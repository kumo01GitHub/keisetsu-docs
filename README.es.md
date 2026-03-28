# keisetsu Documentación

Este es el centro de documentación para la intención de diseño y la política operativa general de keisetsu.

`keisetsu-docs` es un lugar central para gestionar especificaciones, reglas operativas y procedimientos de actualización entre todos los repositorios de keisetsu (publisher / database / mobile).

- Aclara las responsabilidades de cada repositorio
- Documenta los flujos de distribución y validación independientemente de la implementación
- Mantiene criterios comunes para cambios de especificación

## Concepto

keisetsu es una aplicación de tarjetas de memoria de código abierto que hace públicos el almacenamiento de datos de aprendizaje y las rutas de distribución, permitiendo a los usuarios poseer y usar su propio material de aprendizaje.

- Objetivo
  - Crear un entorno donde cualquiera pueda aprender solo con un smartphone
- Motivación
  - Resolver problemas existentes como la privatización de datos, la dependencia en línea y rutas de actualización poco claras
- Ventajas
  - Todas las especificaciones, datos y flujos de distribución son públicos y transparentes
  - OSS: cualquiera puede actualizar y usar los datos de forma gratuita
- Enfoque
  - Separar la creación (publisher), distribución (database) y uso (mobile) para facilitar actualizaciones y reutilización
  - Usar un esquema público para la estructura de datos, un catálogo público para las rutas de distribución y una app compatible offline para el aprendizaje

## Guía para usuarios

### Cómo usar la app móvil de keisetsu

1. Instala la app Expo Go en tu smartphone.
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. Escanea el código QR para iniciar la app keisetsu.

![Expo QR](assets/eas-update.svg)

Puedes empezar a usar la app keisetsu de inmediato.

### Cómo usar el editor web de barajas de keisetsu

1. Accede a la [página pública de keisetsu-publisher](https://keisetsu-publisher.vercel.app)
2. Crea una nueva baraja o importa un CSV / kdb existente
3. Edita las tarjetas y la información de la baraja (ID, título, idioma, etc.)
4. Descarga el archivo ZIP
5. Extrae el ZIP descargado y coloca los archivos generados en keisetsu-database, luego [envía una solicitud de adición/edición](https://github.com/kumo01GitHub/keisetsu-database/issues)

### Idiomas soportados

- Inglés (`en`)
- Japonés (`ja`)
- Español (`es`)
- Portugués (`pt`)
- Chino (`zh`)
- Coreano (`ko`)

## Guía para desarrolladores

Para información detallada sobre la estructura del repositorio, reglas operativas e información técnica, consulta [DEVELOPER.md](./DEVELOPER.md).
