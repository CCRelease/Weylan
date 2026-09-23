# TransferFile 2.0.0 · instalación y verificación

## Windows x64

**Instalador:** descarga `TransferFile-2.0.0-win-x64-setup.exe`, comprueba su hash y ejecútalo. Instala la aplicación para tu usuario y crea un acceso en el menú Inicio. Puedes elegir un acceso de Escritorio. Para desinstalarla, cierra TransferFile —incluido el icono de la bandeja— y utiliza **Aplicaciones instaladas** de Windows.

**Portable:** descarga el ZIP, comprueba su hash, extrae **todo** su contenido en una carpeta y ejecuta `TransferFile.exe`. Mantén juntos el ejecutable y sus DLL. Para quitar esta edición, cierra la aplicación y elimina la carpeta. Las preferencias del usuario se guardan en el perfil de Windows y no se borran al eliminar la carpeta.

El ejecutable y el instalador están firmados con Authenticode por **CoolCode Sentinel Private Publisher**. Es un certificado privado de CoolCode; un Windows sin ese certificado de confianza puede mostrar un aviso de editor desconocido. No aceptes el aviso si la huella o el hash difieren de los publicados.

## Debian/Ubuntu x64

**Instalador:** descarga `TransferFile-2.0.0-linux-x64-setup.deb`, comprueba su hash e instálalo con el gestor de paquetes o con `sudo apt install ./TransferFile-2.0.0-linux-x64-setup.deb`. Abre **TransferFile** desde el menú de aplicaciones o ejecuta `transferfile`. Para desinstalarlo: `sudo apt remove transferfile`.

**Portable:** descarga el TAR.GZ, comprueba su hash, extráelo y ejecuta `./TransferFile.Linux` desde la carpeta extraída. El permiso de ejecución ya está incluido. Conserva todo el contenido en la misma carpeta.

## Comprobar los archivos

Los cuatro paquetes figuran en [SHA256SUMS.txt](SHA256SUMS.txt). Ese archivo tiene una firma CMS separada en [SHA256SUMS.p7s](SHA256SUMS.p7s), creada con la misma identidad de firma de código que el instalador Windows. El certificado público está en [CoolCode-Publisher.cer](CoolCode-Publisher.cer). Huella SHA-1 esperada del certificado:

`2AD77786E39ED19E6A5A72BB9A7752B10822CE62`

En Linux, desde esta carpeta:

```sh
openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
sha256sum -c SHA256SUMS.txt
```

Compara la huella mostrada con la indicada arriba. En Windows, usa `Get-FileHash <archivo> -Algorithm SHA256` y `Get-AuthenticodeSignature <instalador-o-ejecutable>`; la huella del certificado firmante debe coincidir. La firma Authenticode privada no elimina necesariamente el aviso inicial de Windows.

La firma de los hashes comprueba su autenticidad criptográfica; la confianza inicial en la huella publicada depende del canal por el que la obtienes. Contrástala con un canal oficial de CoolCode si es la primera instalación.
