# Claude Slack Bot

Bot de Slack que integra Claude Code para interactuar con repositorios, Jira, Supabase y NotebookLM directamente desde Slack.

## Setup

### Requisitos

- Node.js 20+
- Claude Code CLI instalado con OAuth token
- Slack App con Socket Mode habilitado
- (Opcional) Groq API key para transcripcion de audio

### Variables de entorno

```bash
cp .env.example .env
```

Configura los valores de la app de Slack y el directorio que el bot puede usar
para trabajar. La credencial de Claude Code se configura en la VM según
[las instrucciones de autenticación](CLAUDE.md#auth-de-claude-code-la-del-bot-no-la-de-los-mcp).

### Instalar y correr

```bash
npm ci
npm run build
npm start
```

### Desarrollo

```bash
npm run dev
```

### Systemd (produccion)

```ini
[Unit]
Description=Claude Code Slack Bot
After=network.target

[Service]
Type=simple
User=<usuario>
WorkingDirectory=/home/<usuario>/claude-slack-bot
ExecStart=/usr/bin/node dist/index.js
Restart=always
RestartSec=10
EnvironmentFile=/home/<usuario>/claude-slack-bot/.env
Environment=PATH=/home/<usuario>/.local/bin:/usr/local/bin:/usr/bin:/bin
Environment=HOME=/home/<usuario>

[Install]
WantedBy=multi-user.target
```

## Uso en Slack

### Comandos

| Comando | Descripcion |
|---|---|
| `cwd` | Ver directorio de trabajo actual |
| `cwd <repo>` | Cambiar a un repo (relativo a BASE_DIRECTORY) |
| `cwd /ruta/absoluta` | Cambiar a ruta absoluta |

### Interaccion

- **DM**: Escribe directamente al bot
- **Canales**: Menciona `@Claude Code` en un mensaje o hilo
- **Archivos**: Arrastra un archivo al chat junto con tu mensaje
- **Audio**: Envia una nota de voz y se transcribe automaticamente

### Integraciones

Renueva el acceso a [Jira y Confluence](docs/atlassian-auth.md) o
[NotebookLM](docs/notebooklm-auth.md) con el procedimiento de cada integración.

## Persistencia (Firestore)

Firestore permite retomar una conversación después de reiniciar el servicio. Usa el proyecto autorizado del ambiente.

- En la VM GCP: usa Application Default Credentials via metadata server (sin keys).
- En local: ejecutar `gcloud auth application-default login` una vez.

## Sudoers para self-deploy

Para que el bot pueda redeployarse a si mismo, agregar a `/etc/sudoers.d/claude-slack-bot`:

```
nicolas ALL=(root) NOPASSWD: /bin/systemctl restart claude-slack-bot, /bin/systemctl status claude-slack-bot, /bin/journalctl -u claude-slack-bot *
```

## Permisos en Google Cloud

Limita los permisos de la cuenta de servicio a las operaciones del bot. Las
restricciones de herramientas del SDK complementan los permisos de IAM.
