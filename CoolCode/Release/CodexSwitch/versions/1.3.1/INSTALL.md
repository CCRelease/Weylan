# CodexSwitch 1.3.1 · 23 de octubre de 2026

Gestión local de cuentas Codex y consulta de uso. Incluye .NET 10. Interfaz en EN, ES, CA, FR, DE, IT y PT.

## Windows x64

Windows 10 1809 o posterior, Windows 11. Ejecuta `CodexSwitch-1.3.1-win-x64-setup.exe`: instala para el usuario y crea por defecto accesos con icono en Escritorio e Inicio. Desinstala desde Aplicaciones instaladas; se retiran los accesos y se conservan los datos personales.

Portable: extrae todo `CodexSwitch-1.3.1-win-x64-portable.zip` en una carpeta nueva y ejecuta `CodexSwitch.exe`. Para un acceso de escritorio, crea un acceso directo a ese ejecutable, que contiene el icono. Para retirarlo, cierra desde la bandeja y elimina el acceso y la carpeta extraída.

Para añadir cuentas se necesita Codex CLI o una instalación compatible de Codex Desktop. La sincronización manual del plan utiliza WebView2 Runtime. Las cuotas dependen de los datos que facilite el servicio.

## Linux x64

Validado en Ubuntu 24.04 x64 con X11 virtual en canaryx1. Otras distribuciones y Wayland no se han certificado. Instala Codex CLI y comprueba que `codex --version` funcione en PATH. La autenticación se realiza en el navegador mediante `codex login`.

Instalador: abre `CodexSwitch-1.3.1-linux-x64.deb` con el gestor gráfico de paquetes o ejecuta:

```sh
sudo apt install ./CodexSwitch-1.3.1-linux-x64.deb
```

Instala en `/opt/coolcode/codexswitch` y crea una entrada de menú y un lanzador ejecutable con icono en el escritorio de los usuarios locales. Si tu escritorio solicita confiar en el lanzador, hazlo después de verificar el paquete.

```sh
sudo apt remove coolcode-codexswitch
```

La desinstalación elimina el programa, el icono y ambos lanzadores. Conserva las cuentas y preferencias en `~/.config/CodexSwitch`.

Portable:

```sh
tar -xzf CodexSwitch-1.3.1-linux-x64-portable.tar.gz
./codexswitch/CodexSwitch.Linux
```

Requiere las bibliotecas nativas indicadas por el paquete Debian (X11, ICU 74, OpenSSL 3, fontconfig y OpenGL); el runtime .NET va incluido. Para un acceso de escritorio crea un archivo `.desktop` con `Type=Application`, `Name=CodexSwitch`, `Exec=` seguido de la ruta absoluta a `CodexSwitch.Linux` e `Icon=` seguido de la ruta absoluta a `codexswitch.png`; hazlo ejecutable. Para retirar la edición portable, cierra la ventana y elimina el acceso y la carpeta extraída.

La edición Linux gestiona las credenciales del CLI: cierra las sesiones Codex abiertas antes de cambiar y abre una sesión nueva después. No reinicia Codex Desktop ni incluye la bandeja o la sincronización manual de facturación con WebView2 de Windows. La renovación automática se muestra cuando el servicio la proporciona. No se incluye ni se solicita una cuenta adicional de CoolCode.

## Cambios

Ajusta automáticamente la ventana al alternar entre tarjetas y tabla y conserva el tamaño de cada vista. Añade edición de escritorio Linux con gestión de cuentas, consulta de cuotas y siete idiomas.

Esta publicación incorpora también las mejoras anteriores a 1.3.1 que aún no estaban en Weylan: cuentas desactivables y recuperables, cuotas Free de 30 días, renovación separada de las cuotas y tratamiento de datos ausentes.

## Integridad y firma

Los ejecutables propios de Windows y su instalador tienen firma Authenticode. Los cuatro paquetes completos están cubiertos por `SHA256SUMS.txt` y su firma CMS separada `SHA256SUMS.p7s`. `CoolCode-Publisher.cer` contiene solo el certificado público.

Huella SHA-1 del editor: `2AD77786E39ED19E6A5A72BB9A7752B10822CE62`. Contrástala por un canal oficial de CoolCode. Es un certificado privado, vigente hasta el 2 de agosto de 2031; estas firmas no tienen sello de tiempo y Windows puede mostrar un aviso de confianza.

```sh
openssl cms -verify -binary -inform DER -in SHA256SUMS.p7s -content SHA256SUMS.txt -noverify -out /dev/null
openssl x509 -inform DER -in CoolCode-Publisher.cer -noout -fingerprint -sha1
sha256sum -c SHA256SUMS.txt
```

`-noverify` verifica la firma criptográfica sin establecer confianza en el editor; comprueba también la huella. En Windows usa `Get-FileHash -Algorithm SHA256` y `Get-AuthenticodeSignature` sobre el instalador y el ejecutable extraído.
