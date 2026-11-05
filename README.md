# Easy RIPS

Aplicación de escritorio para Windows con la que los prestadores de servicios de salud registran sus atenciones y generan los **RIPS** (Registro Individual de Prestación de Servicios de Salud) en formato JSON. Los RIPS se generan como pide la **Resolución 948 de 2026** y su Documento técnico 1. La app los envía al validador del Ministerio de Salud (**MUV**) y guarda el **CUV** que este devuelve.

Este repositorio solo publica los instaladores y las actualizaciones. El código está en un repositorio privado.

> Hasta la versión 2.5 se llamaba **RIPS Laboratorio Clínico**. Las copias ya instaladas se actualizan solas, sin reinstalar.

## Para quién es

- **Laboratorios clínicos:** registran los exámenes de cada paciente.
- **Consultorios odontológicos:** registran consultas y procedimientos.

Sirve tanto a quien factura electrónicamente como a la persona natural no obligada a facturar.

Cada laboratorio o consultorio trabaja con sus propios usuarios, pacientes, facturas y catálogo de procedimientos, y no ve los datos de los demás. La app se muestra con su nombre, color, logo e icono, y con sus palabras: «exámenes» en el laboratorio, «procedimientos» en el consultorio.

## Qué hace

- **Registro de la atención:** paciente, factura y servicios se guardan juntos. Los procedimientos se buscan en la tabla CUPSRips y los diagnósticos en la CIE10, ambas de SISPRO. Se elige el profesional de la salud que atendió, inscrito en el RETHUS.
- **Consultas y procedimientos:** las consultas se reportan aparte, con la causa que las motiva, el tipo de diagnóstico y los diagnósticos relacionados.
- **Revisión antes de exportar:** la app avisa de los datos que el MUV rechazaría y no genera el archivo hasta que se corrijan. Por ejemplo:
  - códigos no habilitados en CUPSRips;
  - diagnósticos que no aplican al sexo o a la edad del paciente;
  - profesionales no habilitados;
  - fechas fuera del periodo de la factura.
- **Facturación:** tres formas de trabajar, a elegir según cada prestador:
  - **Numeración de la app:** con la resolución de la DIAN.
  - **Factura emitida en otro programa:** un proveedor tecnológico, un software contable o la solución gratuita de la DIAN. Al enviar al MUV se carga su XML.
  - **Sin factura electrónica:** para quien no está obligado a facturar.
- **Envío al MUV:** se envía cada factura con su RIPS. La app guarda el CUV y arma el paquete para radicar ante el pagador. También envía las notas de ajuste, crédito y débito.
- **Historial y correcciones:** pacientes, facturas y servicios. Toda corrección exige un motivo.
- **Gobernanza:** bitácora de auditoría que no se puede modificar, y solicitudes de cambio entre los usuarios y su administrador.

## Seguridad y datos

- Cada usuario entra con su contraseña y un código de la aplicación de autenticación del celular: es la verificación en dos pasos, obligatoria para todos.
- La sesión se cierra sola tras 15 minutos sin uso.
- Cada prestador ve únicamente sus datos. Las reglas las aplica el servidor, no solo la app.
- Los archivos que se exportan solo los puede abrir el usuario de Windows que los guardó. La app avisa si se guardan en una USB, en la red o en una carpeta que se sincroniza con la nube.
- Los datos de salud son datos sensibles según la **Ley 1581 de 2012**: su tratamiento debe estar contemplado en la política de datos de cada prestador.

## Requisitos

- Windows 10 u 11, de 32 o 64 bits. No hay que instalar .NET ni nada más.
- Conexión a internet: los datos se guardan en la nube.
- Un usuario, que crea el administrador de la plataforma, y una aplicación de autenticación en el celular (Google Authenticator, Microsoft Authenticator u otra).
- Para enviar al MUV: el usuario del prestador en SISPRO, con permiso para el MUV.

## Instalación

Descargue la última versión en [Releases](https://github.com/JuanAvendan/EasyRIPS-versiones/releases/latest):

| Archivo | Para qué |
|---|---|
| `RIPSLaboratorioClinico-win-Setup.exe` | **Instalador (recomendado).** Instala solo para su usuario de Windows, sin pedir permisos de administrador, y crea accesos directos en el escritorio y en el menú Inicio. Se desinstala desde *Configuración › Aplicaciones* |
| `RIPSLaboratorioClinico-win-Portable.zip` | **Versión portable.** Se descomprime en cualquier carpeta (o en una USB) y se abre desde ahí, sin instalar |
| `SHA256SUMS.txt` | La huella de cada archivo, para comprobar que no se alteró |
| `*.nupkg`, `releases.win.json`, `RELEASES` | Paquetes que usa la app para actualizarse. No hay que descargarlos |

Los archivos conservan el nombre anterior de la app (`RIPSLaboratorioClinico`). Así las copias instaladas siguen reconociendo sus actualizaciones.

### Comprobar la descarga

Si Windows muestra un aviso al abrir el instalador, compruebe antes su huella. En PowerShell, en la carpeta donde lo descargó:

```powershell
Get-FileHash .\RIPSLaboratorioClinico-win-Setup.exe -Algorithm SHA256
```

El resultado debe ser igual al que aparece para ese archivo en `SHA256SUMS.txt` del mismo release. Si no coincide, no lo ejecute.

## Actualizaciones

- **Automáticas:** al abrirse, la app busca una versión nueva y la descarga en segundo plano. Luego ofrece reiniciar para instalarla; si no se reinicia, se instala la próxima vez que se abra.
- **A mano:** con «Buscar actualizaciones», al pie de la pantalla de inicio de sesión o en el menú de usuario.
- **Versión mínima:** cuando una actualización es obligatoria, la app la instala antes de dejar entrar.

La instalada y la portable se actualizan igual. Cada paquete se verifica con su huella antes de instalarse.

## Soporte

Para crear usuarios, cambiar los datos de su laboratorio o consultorio o resolver un problema, contacte al administrador de su laboratorio o consultorio, o a quien le entregó la app. Las novedades de cada versión están en sus [Releases](https://github.com/JuanAvendan/EasyRIPS-versiones/releases).
