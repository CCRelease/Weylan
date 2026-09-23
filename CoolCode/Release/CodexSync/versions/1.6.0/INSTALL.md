# CodexSync 1.6.0

Windows x64; instalación por usuario. El instalador y la edición portable incluyen .NET y ofrecen interfaz en EN, ES, CA, FR, DE, IT y PT.

## Instalación

Descarga [el instalador](CodexSync-1.6.0-win-x64-setup.exe), verifica su SHA-256 mediante [SHA256SUMS.txt](SHA256SUMS.txt) y ejecútalo. Se crea un acceso en el menú Inicio; el del escritorio es opcional. Desinstala desde **Aplicaciones instaladas** de Windows.

Para la edición portable, descarga [el ZIP](CodexSync-1.6.0-win-x64-portable.zip), verifica su hash, extrae todo el contenido y ejecuta `CodexSync.exe`. Para retirarla, elimina la carpeta extraída. Las preferencias y datos personales, si los hay, permanecen en el perfil del usuario.

## Firma e integridad

El ejecutable y el instalador están firmados con Authenticode por **CoolCode Sentinel Private Publisher**. Al ser un certificado privado, Windows puede mostrar un aviso de editor desconocido. Comprueba los hashes y la firma antes de continuar.

La lista de hashes tiene una [firma CMS separada](SHA256SUMS.p7s) y se incluye el [certificado público](CoolCode-Publisher.cer). Huella SHA-1 esperada: `2AD77786E39ED19E6A5A72BB9A7752B10822CE62`.

En Windows, usa `Get-FileHash <archivo> -Algorithm SHA256` y `Get-AuthenticodeSignature <instalador-o-ejecutable>`. La firma del manifiesto se verifica con OpenSSL: `openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out NUL`. Compara la huella del certificado por un canal oficial de CoolCode: `-noverify` verifica la firma criptográfica, pero no establece por sí solo la confianza en el editor.
