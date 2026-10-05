# MDX Viewer Linux 1.0.3 · 5 de octubre de 2026

Ubuntu 24.04 x64. .NET 10 incluido. GTK3/WebKitGTK 4.1 y otras bibliotecas se instalan mediante las dependencias del paquete .deb. Bandeja X11/Xfce probada: al pasar el puntero aparecen los documentos; el clic derecho ofrece la lista y la selección abre el documento inmediatamente. En otros escritorios puede utilizar AppIndicator; GNOME puede necesitar su extensión. Wayland y otras distribuciones no se han certificado.

## Instalación y uso

Descarga coolcode-mdxviewer-linux_1.0.3_amd64.deb y verifica su integridad. Instala:
    sudo apt install ./coolcode-mdxviewer-linux_1.0.3_amd64.deb

Se instala en /opt/coolcode/mdxviewer-linux. Crea la entrada del menú de aplicaciones y el acceso ejecutable MDXViewer.desktop con icono en los escritorios de usuarios locales existentes. Si el escritorio solicita confiar en el lanzador, confirma después de verificar el paquete. Abre desde el menú o el escritorio. No modifica la aplicación predeterminada para Markdown. Para desinstalar, sal de la bandeja y ejecuta:
    sudo apt remove coolcode-mdxviewer-linux

Se retiran el lanzador del menú, el acceso del escritorio y el icono. Preferencias en ~/.config/coolcode/MDXViewer.Linux y documentos del usuario se conservan.

Para la edición portable:
    tar -xzf mdxviewer-linux-1.0.3-linux-x64.tar.gz
    ./mdxviewer-linux-1.0.3/MDXViewer.Linux documento.mdx

Necesita las mismas bibliotecas GTK/WebKitGTK declaradas por el paquete .deb. Para crear un acceso, copia Packaging/coolcode-mdxviewer.desktop al escritorio, cambia Exec a la ruta absoluta del ejecutable extraído e Icon a la ruta absoluta de Packaging/mdxviewer.svg y hazlo ejecutable. Para retirarlo elimina el acceso y la carpeta extraída.

## Cambios

Añade creación y retirada automáticas del acceso de escritorio al instalar y desinstalar; publica instalador y portable con manifiesto firmado, conservando iconos, buscador y bandeja X11.
## Integridad y firmas

Comprueba SHA256SUMS.txt antes de ejecutar o instalar. El manifiesto tiene firma CMS separada en SHA256SUMS.p7s, válida para los paquetes completos; no es un simple archivo de hashes. CoolCode-Publisher.cer contiene únicamente el certificado público. Huella SHA-1 esperada: 2AD77786E39ED19E6A5A72BB9A7752B10822CE62. Confirma la huella por un canal oficial de CoolCode.

En Linux con OpenSSL, verifica la firma y compara los hashes:
    openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
    openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
    sha256sum -c SHA256SUMS.txt

La opción -noverify verifica la firma criptográfica sin establecer confianza en el editor: la huella debe coincidir con la esperada. En Windows usa Get-FileHash -Algorithm SHA256 y Get-AuthenticodeSignature sobre el instalador y el ejecutable extraído; la firma Authenticode debe corresponder a la misma huella. El certificado es privado y Windows puede mostrar un aviso de editor desconocido. Su vigencia termina el 2 de agosto de 2031; estas firmas no tienen sello de tiempo.