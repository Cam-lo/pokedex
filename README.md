PokéDex
Aplicación web desarrollada en Angular que permite explorar diferentes especies de Pokémon y consultar información detallada sobre sus características y habilidades. Consume la PokéAPI como fuente de datos.
Este repositorio corresponde al despliegue de la aplicación en Microsoft Azure Static Web Apps,

Escaneo de seguridad
Herramienta: securityheaders.com

pokedex/
├── src/
│   ├── app/                          # Componentes y servicios Angular
│   ├── assets/                       # Recursos estáticos
│   ├── staticwebapp.config.json      # Configuración de seguridad HTTP
│   └── ...
├── angular.json                      # Configuración del build Angular
├── package.json                      # Dependencias del proyecto
├── Despliegue.md                     # Documentación técnica de despliegue
└── README.md                         # Este archivo

Tecnologías utilizadas
Categoría
Herramienta
Framework frontendAngularLenguajeTypeScriptAPI de datosPokéAPIHostingAzure Static Web AppsCI/CDGitHub ActionsControl de versionesGit + GitHubAnálisis de seguridadsecurityheaders.com



1. ¿Qué vulnerabilidades previenen los encabezados implementados?
Los headers HTTP configurados en staticwebapp.config.json mitigan vulnerabilidades reales documentadas en el OWASP Top 10:

Strict-Transport-Security: previene ataques de downgrade y man-in-the-middle forzando al navegador a usar siempre HTTPS. Sin este header, un atacante en la red podría interceptar la primera conexión HTTP y redirigir al usuario a un sitio falso.
Content-Security-Policy: limita los orígenes desde los cuales se pueden cargar scripts, estilos e imágenes. Es la principal defensa contra Cross-Site Scripting (XSS), que permitiría a un atacante ejecutar código malicioso en el navegador de los usuarios.
X-Content-Type-Options: nosniff: evita que el navegador interprete archivos con un tipo MIME distinto al declarado por el servidor, previniendo ataques de MIME confusion donde un archivo supuestamente inofensivo (una imagen) se ejecuta como script.
X-Frame-Options: DENY: impide que la aplicación sea embebida en un <iframe> dentro de otro sitio. Bloquea ataques de clickjacking, donde un atacante superpone la aplicación sobre una página fraudulenta para engañar al usuario.
Referrer-Policy: no-referrer: evita que el navegador envíe la URL de origen al navegar a otros sitios, reduciendo la fuga de información sensible (como tokens o identificadores en la URL).
Permissions-Policy: bloquea el acceso a APIs sensibles del navegador (cámara, micrófono, geolocalización, métodos de pago) que la aplicación no necesita. Reduce la superficie de ataque en caso de que un XSS logre ejecutarse.

2. ¿Qué aprendí sobre la relación entre despliegue y seguridad web?
Desplegar una aplicación no es solo "subirla a internet". Un despliegue sin consideraciones de seguridad convierte a la aplicación en un blanco fácil: sin HTTPS forzado, sin CSP y sin protección contra clickjacking, incluso una aplicación con código impecable queda expuesta. La seguridad en el despliegue es una capa adicional a la seguridad del código y debe configurarse explícitamente; por defecto los servidores no incluyen estos headers. Azure Static Web Apps simplifica la gestión mediante staticwebapp.config.json, pero la responsabilidad de definir correctamente las políticas sigue siendo del desarrollador.



Autor

Estudiante: Cristian Fuentes

https://github.com/Cam-lo