# MDX Viewer Linux 1.3.0 · 4 de noviembre de 2026

Editor local Markdown/MDX con GTK3 y WebKitGTK. .NET 10 incluido. Probado en Ubuntu 24.04 x64 (X11) y Debian 12 x64 (X11 y Wayland con Weston anidado). No se declara soporte ARM64 ni validación de todas las distribuciones/escritorios.

## Instalar y actualizar

Verificar firmas y hashes. Cerrar la app antes de actualizar. Desde la carpeta descargada:

```sh
sudo apt install ./coolcode-mdxviewer-linux_1.3.0_amd64.deb
```

APT instala las dependencias GTK3/WebKitGTK 4.1, ICU, OpenSSL y bibliotecas gráficas requeridas. El paquete incluye icono, lanzador en el menú y acceso ejecutable en el escritorio de los usuarios con carpeta de escritorio. Algunos escritorios requieren marcar manualmente el lanzador como de confianza. La bandeja depende del soporte AppIndicator del escritorio; sin bandeja, cerrar termina la app.

## Portable

Extraer todo el TAR.GZ y ejecutar:

```sh
tar -xzf mdxviewer-linux-1.3.0-linux-x64.tar.gz
cd mdxviewer-linux-1.3.0
./MDXViewer.Linux
```

El portable necesita las mismas bibliotecas del sistema que el DEB; .NET está incluido. Para crear un acceso, copiar Packaging/coolcode-mdxviewer.desktop al escritorio, ajustar Exec e Icon a las rutas absolutas de MDXViewer.Linux y Packaging/mdxviewer.svg y hacerlo ejecutable con chmod +x. Extraer el TAR no registra una instalación.

## Usar y desinstalar

Manual en Documentation/Manual-es.md y guía inglesa en Documentation/Quick-start-en.md. La interfaz dispone de siete idiomas, vista preview/código/ambos, zoom, recorte/anotación, búsqueda global, explorador multirraíz y exportaciones PDF/HTML/fragmento/ZIP/DOCX.

Elegir Salir en la bandeja y ejecutar:

```sh
sudo apt remove coolcode-mdxviewer-linux
```

Se retiran menú, icono y acceso de escritorio creado por el paquete. Documentos y preferencias se conservan. Para retirar el portable, cerrar la app y eliminar su carpeta y acceso. Preferencias en ~/.config/coolcode/MDXViewer.Linux (o XDG_CONFIG_HOME).

## Cambios

Incluye documentación de usuario y paquetes compatibles con Debian 12 y Ubuntu 24.04; amplía la validación gráfica a X11 y Wayland y documenta la revisión DOCX en Microsoft Word.
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
