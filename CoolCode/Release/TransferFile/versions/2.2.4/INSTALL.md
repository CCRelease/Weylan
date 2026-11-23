# TransferFile 2.2.4 · instalación y verificación

TransferFile 2.2.4 reúne el envío, la recepción y la sincronización en la misma interfaz para Windows y Linux. La ventana muestra la versión del ejecutable. Los paquetes incluyen .NET.

## Windows x64

Descarga [el instalador](TransferFile-2.2.4-win-x64-setup.exe), comprueba su hash según [SHA256SUMS.txt](SHA256SUMS.txt) y ejecútalo. Instala para tu usuario y crea accesos en el escritorio y en el menú Inicio. Para desinstalar, cierra TransferFile —incluido su icono de bandeja— y usa **Aplicaciones instaladas**.

Para la edición portable, descarga [el ZIP](TransferFile-2.2.4-win-x64-portable.zip), comprueba el hash, extrae todo su contenido y ejecuta `TransferFile.exe`. Mantén juntos todos los archivos extraídos. Para añadir un acceso directo, usa el menú contextual de TransferFile.exe y elige Enviar a → Escritorio. Al retirarla, las preferencias guardadas en el perfil del usuario permanecen.

El ejecutable y el instalador están firmados con Authenticode por **CoolCode Sentinel Private Publisher**. Al ser un certificado privado, Windows puede mostrar un aviso de editor desconocido.

## Debian/Ubuntu x64

Descarga [el DEB](TransferFile-2.2.4-linux-x64-setup.deb), comprueba su hash e instálalo con el gestor de paquetes o con `sudo apt install ./TransferFile-2.2.4-linux-x64-setup.deb`. La instalación con sudo desde la cuenta de escritorio añade el icono de la aplicación y un lanzador en ese escritorio. Abre TransferFile desde el menú de aplicaciones o ejecuta `transferfile`. Para desinstalar: `sudo apt remove transferfile`.

Para la edición portable, descarga [el TAR.GZ](TransferFile-2.2.4-linux-x64-portable.tar.gz), comprueba su hash, extráelo y ejecuta `./TransferFile.Linux`. Conserva todos los archivos juntos. Para añadir un acceso al escritorio, crea un lanzador que apunte a la ruta absoluta de TransferFile.Linux y selecciona el icono PNG incluido. El permiso de ejecución y el acceso a los directorios están incluidos en el paquete.

## Comprobar firmas e integridad

Los cuatro paquetes figuran en [SHA256SUMS.txt](SHA256SUMS.txt), con [firma CMS separada](SHA256SUMS.p7s) y [certificado público](CoolCode-Publisher.cer). Huella SHA-1 esperada: `2AD77786E39ED19E6A5A72BB9A7752B10822CE62`.

En Linux, desde esta carpeta:

```sh
openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
sha256sum -c SHA256SUMS.txt
```

Compara la huella con un canal oficial de CoolCode. `-noverify` comprueba la firma criptográfica, no establece por sí solo la confianza en el editor. En Windows, usa `Get-FileHash <archivo> -Algorithm SHA256` y `Get-AuthenticodeSignature <instalador-o-ejecutable>`.
