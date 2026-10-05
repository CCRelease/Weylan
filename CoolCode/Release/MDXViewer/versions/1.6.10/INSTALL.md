# MDX Viewer Windows 1.6.10 · 5 de octubre de 2026

Windows 10/11 x64, .NET 10 incluido. Necesita Microsoft Edge WebView2 Runtime: https://developer.microsoft.com/microsoft-edge/webview2/ .
La aplicación permite editar Markdown/MDX, abrir pestañas, exportar PDF con Mermaid, alternar código y preview y cambiar entre EN/ES/CA/FR/DE/IT/PT.

## Instalación y uso

Descarga MDXViewer-1.6.10-win-x64-setup.exe y verifica su integridad. El instalador por usuario crea los accesos del escritorio y del menú Inicio con el icono propio. Abre MDX Viewer desde cualquiera de ellos. Para desinstalar, elige Salir en la bandeja y usa Aplicaciones instaladas; se retiran ambos accesos.

Para la edición portable, extrae todo MDXViewer-1.6.10-win-x64-portable.zip en una carpeta nueva y ejecuta MDXViewer.exe. Puedes crear un acceso del escritorio apuntando a ese ejecutable y asignarle Assets/MDXViewer.ico. Extraer el ZIP no registra una instalación; para retirarlo basta borrar su carpeta, después de salir.

Cerrar la ventana la oculta en la bandeja. Desde la bandeja se puede seleccionar un documento o salir. La búsqueda aparece a la derecha bajo la lupa. Preferencias y documentos del usuario se conservan al desinstalar.

## Cambios

Publica instalador y portable Windows firmados, con accesos de escritorio e Inicio; conserva el buscador bajo la lupa y Release en bin/Release.
## Integridad y firmas

Comprueba SHA256SUMS.txt antes de ejecutar o instalar. El manifiesto tiene firma CMS separada en SHA256SUMS.p7s, válida para los paquetes completos; no es un simple archivo de hashes. CoolCode-Publisher.cer contiene únicamente el certificado público. Huella SHA-1 esperada: 2AD77786E39ED19E6A5A72BB9A7752B10822CE62. Confirma la huella por un canal oficial de CoolCode.

En Linux con OpenSSL, verifica la firma y compara los hashes:
    openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
    openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
    sha256sum -c SHA256SUMS.txt

La opción -noverify verifica la firma criptográfica sin establecer confianza en el editor: la huella debe coincidir con la esperada. En Windows usa Get-FileHash -Algorithm SHA256 y Get-AuthenticodeSignature sobre el instalador y el ejecutable extraído; la firma Authenticode debe corresponder a la misma huella. El certificado es privado y Windows puede mostrar un aviso de editor desconocido. Su vigencia termina el 2 de agosto de 2031; estas firmas no tienen sello de tiempo.