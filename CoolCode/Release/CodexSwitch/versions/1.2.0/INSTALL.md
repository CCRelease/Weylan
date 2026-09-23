# CodexSwitch 1.2.0

Windows x64; instalación por usuario. El instalador y la edición portable incluyen .NET y muestran la interfaz en EN, ES, CA, FR, DE, IT y PT.

## Instalación

Descarga [el instalador](CodexSwitch-1.2.0-win-x64-setup.exe), comprueba su SHA-256 según [SHA256SUMS.txt](SHA256SUMS.txt) y ejecútalo. Crea un acceso en el menú Inicio; el acceso de Escritorio es opcional. Para desinstalar, cierra la aplicación y su icono de bandeja y usa **Aplicaciones instaladas** de Windows.

Para la edición portable, descarga [el ZIP](CodexSwitch-1.2.0-win-x64-portable.zip), comprueba el hash, extrae todo su contenido y ejecuta `CodexSwitch.exe`. Elimina la carpeta extraída para retirar esa edición. La configuración personal permanece en el perfil del usuario.

## Firmas e integridad

El ejecutable y el instalador tienen firma Authenticode de **CoolCode Sentinel Private Publisher**. Es un certificado privado, por lo que Windows puede mostrar un aviso de editor desconocido. Comprueba el hash y la firma antes de aceptarlo.

La lista de hashes tiene una [firma CMS separada](SHA256SUMS.p7s) y el [certificado público](CoolCode-Publisher.cer). Huella SHA-1 esperada: `2AD77786E39ED19E6A5A72BB9A7752B10822CE62`.

En Windows, usa `Get-FileHash <archivo> -Algorithm SHA256` y `Get-AuthenticodeSignature <instalador-o-ejecutable>`. La firma del manifiesto puede comprobarse con OpenSSL: `openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out NUL`. Compara la huella del certificado con un canal oficial de CoolCode: `-noverify` comprueba la firma criptográfica, no establece por sí solo la confianza en el editor.
