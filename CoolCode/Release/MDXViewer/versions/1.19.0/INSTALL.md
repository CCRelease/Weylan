# MDX Viewer Windows 1.19.0 · 4 de noviembre de 2026

Editor local Markdown/MDX con vista previa, pestañas, imágenes con recorte y anotación, explorador de varias carpetas, búsqueda global y exportación PDF, HTML, ZIP y DOCX. Idiomas EN/ES/CA/FR/DE/IT/PT.

## Instalar

Windows 10/11 x64. .NET 10 está incluido; se necesita Microsoft Edge WebView2 Runtime. Descargarlo desde https://developer.microsoft.com/microsoft-edge/webview2/ si falta.

Verificar las firmas y hashes. Ejecutar MDXViewer-1.19.0-win-x64-setup.exe. Instala por usuario y crea accesos con icono en el escritorio y el menú Inicio. Al actualizar, cerrar MDX Viewer mediante Salir en la bandeja antes de instalar. Los documentos se conservan.

## Portable

Extraer todo MDXViewer-1.19.0-win-x64-portable.zip en una carpeta nueva y ejecutar MDXViewer.exe. Crear un acceso directo al ejecutable y seleccionar Assets/MDXViewer.ico como icono. Extraer el ZIP no registra una instalación. No mezclar archivos de distintas versiones.

## Usar y desinstalar

Abrir un MD/MDX o una carpeta. El botón de vista alterna preview/código/ambos. Ctrl +/− y Ctrl + rueda amplían texto e imágenes. El menú Exportar utiliza las ediciones actuales. Manual completo en Documentation/Manual-es.md y guía inglesa en Documentation/Quick-start-en.md.

Cerrar la ventana puede dejar la app en la bandeja: elegir Salir para terminar. Para desinstalar usar Aplicaciones instaladas; se retiran accesos de escritorio e Inicio. Las preferencias y los documentos se conservan. Para retirar el portable, cerrar la app y eliminar su carpeta y acceso directo.

## Cambios

Incluye manual de usuario y guía rápida; actualiza el instalador en siete idiomas y verifica DOCX editable en Microsoft Word y prepara la distribución firmada con las mejoras de edición, GFM y DOCX.

Incluye las mejoras desde 1.6.16: zoom completo, edición de imágenes, componentes MDX, explorador multirraíz, búsqueda por contenido, gestión revisada de enlaces y exportaciones. Los componentes MDX son extensiones compatibles con DocPortal; no se ejecutan JSX/imports arbitrarios. El DOCX conserva contenido editable; Mermaid/SVG son imágenes. La paginación depende de las fuentes y del procesador de textos.
## Integridad y firmas

El instalador, el desinstalador y los binarios propios Windows tienen firma Authenticode. Los paquetes completos se verifican con SHA256SUMS.txt y su firma CMS separada SHA256SUMS.p7s. CoolCode-Publisher.cer es únicamente el certificado público.

Huella SHA-1 esperada del editor: **2AD77786E39ED19E6A5A72BB9A7752B10822CE62**. El certificado es privado, CN=CoolCode Sentinel Private Publisher, O=CoolCode; Windows puede mostrar editor desconocido. Su vigencia termina el 2 de agosto de 2031; las firmas no llevan sello de tiempo.

Con OpenSSL, verificar la firma criptográfica y después los paquetes:

```sh
openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
sha256sum -c SHA256SUMS.txt
```

`-noverify` no establece confianza en el editor. La huella del firmante debe coincidir con la indicada; extraer el certificado firmante con `openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -signer signer.pem -out /dev/null` y consultar `openssl x509 -in signer.pem -noout -fingerprint -sha1`.

En Windows, `Get-FileHash -Algorithm SHA256` permite contrastar el manifiesto y `Get-AuthenticodeSignature` inspecciona el instalador y MDXViewer.exe. El firmante debe tener la misma huella. No importar certificados ni cambiar seguridad para omitir la comprobación.
