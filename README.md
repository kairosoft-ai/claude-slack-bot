# Operar el bot de Slack

El bot permite trabajar sobre los repositorios autorizados desde conversaciones
de Slack. Selecciona la instancia, zona y proyecto vigentes desde el inventario
operativo antes de conectar a la VM.

## Preparación

Instala las dependencias y completa `.env` a partir del ejemplo con la app de Slack
y el directorio de trabajo autorizado.

```sh
npm ci
npm run build
npm start
```

Usa la identidad del ambiente para Firestore. En desarrollo, prepara credenciales
de Application Default Credentials para ese proyecto.

## Autenticación

Renueva la credencial de Claude Code con `claude setup-token`, completa la
autorización del operador en el navegador y guarda el token en el entorno privado
del servicio. Reinícialo y comprueba una consulta desde Slack.

Para diagnosticar un fallo de autenticación, prueba desde el directorio de la
instalación para conservar la resolución del SDK. Mantén tokens y respuestas
de autorización fuera de logs y artefactos públicos.

Sigue los procedimientos de [Atlassian](docs/atlassian-auth.md) y
[NotebookLM](docs/notebooklm-auth.md) para renovar esas integraciones.

## Publicar y comprobar

En la instalación de la VM, actualiza al commit revisado, instala con `npm ci`,
compila y reinicia el servicio `claude-slack-bot`. Conserva el commit anterior para
revertir y revisa el journal después del reinicio.

Prueba una conversación existente y otra nueva con un usuario autorizado y
comprueba los accesos del bot al directorio e integraciones esperados.
Usa permisos de IAM y sudo limitados a esas operaciones.

Consulta [AGENTS.md](AGENTS.md) para mantener el repositorio.
