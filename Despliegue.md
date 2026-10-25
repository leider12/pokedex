# 🚀 Guía Detallada de Despliegue - Pokédex en Azure App Service

Este documento explica de forma detallada el proceso técnico, comandos y configuraciones especiales implementadas para desplegar la aplicación web de la Pokédex en la nube pública de Azure.

---

## 🛠️ 1. Compilación del Código Fuente (Local)
Antes de enviar los artefactos a la nube, se preparó la aplicación desarrollada en **Angular** ejecutando la compilación optimizada para producción:
\`\`\`bash
npm run build
\`\`\`
Este comando genera la carpeta de distribución `dist/pokedex-angular`, conteniendo los archivos estáticos listos para ejecutarse en el servidor web.

---

## 🔒 2. Configuración Especial de Seguridad y Enrutamiento (`web.config`)
Para asegurar la compatibilidad con el servidor IIS de Windows en Azure y cumplir con los estándares de seguridad web, se creó un archivo **`web.config`** en la raíz del proyecto y se incorporó al directorio de producción. Este archivo incluye:
* **Regla de Reescritura (URL Rewrite):** Vital para las aplicaciones de una sola página (SPA) en Angular, permitiendo que las rutas internas funcionen correctamente al recargar la página en el navegador.
* **Cabeceras HTTP de Seguridad:** Inyección de políticas estrictas (`Strict-Transport-Security`, `X-Content-Type-Options`, `X-Frame-Options`, `Content-Security-Policy`, `Referrer-Policy` y `Permissions-Policy`).

---

## 📦 3. Proceso de Despliegue mediante Kudu (Zip Push Deploy)
El despliegue hacia la infraestructura en la nube se completó siguiendo estos pasos:
1. Se comprimieron todos los archivos compilados de la carpeta `dist/pokedex-angular` (junto al archivo `web.config`) en un archivo en formato **`.zip`**.
2. Se accedió al panel de gestión avanzada del App Service a través de Kudu en la URL institucional asignada:
   `https://pokedex-app-leider.scm.azurewebsites.net`
3. En el menú superior, se seleccionó la herramienta **Tools > Zip Push Deploy**.
4. Se arrastró y soltó el archivo `.zip` en el recuadro de despliegue, permitiendo que el servidor web de Azure descomprima, reemplace y ponga en marcha la aplicación de forma automática.

---

## 🌐 4. Verificación y Enlaces del Proyecto
* **Repositorio del Código Fuente (GitHub):** [github.com/leider12/pokedex](https://github.com/leider12/pokedex)
* **URL Pública Oficial de Producción en Azure:** [pokedex-app-leider-e6hwgqafaphsd6d5.eastus2-01.azurewebsites.net](https://pokedex-app-leider-e6hwgqafaphsd6d5.eastus2-01.azurewebsites.net/)
